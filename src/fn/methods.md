# Métodos

Los métodos son funciones adjuntas a objetos. Estos métodos tienen acceso a los
datos del objeto y sus otros métodos a través de la palabra clave `self`. Los
métodos se definen en un bloque `impl`.

```rust,editable
struct Punto {
    x: f64,
    y: f64,
}

// Bloque de implementación, todos los métodos de `Punto` van aquí
impl Punto {
    // Este es un método estático
    // Los métodos estáticos no necesitan ser llamados por una instancia
    // Estos métodos se utilizan generalmente como constructores
    // Static methods don't need to be called by an instance
    fn origen() -> Punto {
        Punto { x: 0.0, y: 0.0 }
    }

    // Otro método estático, que toma dos argumentos:
    fn new(x: f64, y: f64) -> Punto {
        Punto { x: x, y: y }
    }
}

struct Rectangulo {
    p1: Punto,
    p2: Punto,
}

impl Rectangulo {
    // Este es un método de instancia
    // `&self` es azúcar sintáctica para `self: &Self`, donde `Self` es el tipo
    // del objeto llamador. En este caso, `Self` = `Rectangulo`
    fn area(&self) -> f64 {
        // `self` da acceso a los campos de la estructura a través del operador
        // de punto
        let Punto { x: x1, y: y1 } = self.p1;
        let Punto { x: x2, y: y2 } = self.p2;

        // `abs` es un método de `f64` que devuelve el valor absoluto del
        // objeto llamador
        ((x1 - x2) * (y1 - y2)).abs()
    }

    fn perimetro(&self) -> f64 {
        let Punto { x: x1, y: y1 } = self.p1;
        let Punto { x: x2, y: y2 } = self.p2;

        2.0 * ((x1 - x2).abs() + (y1 - y2).abs())
    }

    // Este método requiere que el objeto de la llamada sea mutable
    // `&mut self` es azúcar sintáctica para `self: &mut Self`
    fn trasldar(&mut self, x: f64, y: f64) {
        self.p1.x += x;
        self.p2.x += x;

        self.p1.y += y;
        self.p2.y += y;
    }
}

// `Par` posee recursos: dos enteros asignados al montículo
struct Par(Box<i32>, Box<i32>);

impl Par {
    // Este método "consume" los recursos del objeto llamador
    // `self` es azúcar sintáctica para `self: Self`
    fn destruir(self) {
        // Desestructurar `self`
        let Par(primero, segundo) = self;

        println!("Destuyendo Par({}, {})", primero, segundo);

        // `primero` y `segundo` salen del alcance y se liberan
    }
}

fn main() {
    let rectangulo = Rectangulo {
        // Los métodos estáticos se llaman con dos puntos dobles
        p1: Punto::origen(),
        p2: Punto::new(3.0, 4.0),
    };

    // Los métodos de instancia se llaman usando el operador de punto
    // Ten en cuenta que el primer argumento `& self` se pasa implícitamente,
    // es decir, `rectangulo.perimetro()` === `Rectangulo::perimetro(&rectangulo)`
    println!("Rectangulo perimetro: {}", rectangulo.perimetro());
    println!("Rectangulo area: {}", rectangulo.area());

    let mut cuadrado = Rectangulo {
        p1: Punto::origen(),
        p2: Punto::new(1.0, 1.0),
    };

    // ¡Error! `rectangulo` es inmutable, pero este método requiere un objeto
    // mutable
    //rectangulo.trasldar(1.0, 0.0);
    // TODO ^ Intenta descomentar esta línea

    // ¡Okey! Los objetos mutables pueden llamar a métodos mutables
    cuadrado.trasldar(1.0, 1.0);

    let par = Par(Box::new(1), Box::new(2));

    par.destruir();

    // ¡Error! La llamda `destruir` anterior "consumió" `par`
    //par.destruir();
    // TODO ^ Intenta descomentar esta línea
}
```
