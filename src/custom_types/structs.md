# Estructuras

Hay tres tipos de estructuras que se pueden crear usando la palabra clave
`struct`:

* Las estructuras de tuplas, que son, básicamente, tuplas con nombre.
* Las [estructuras C][c_struct] clásicas.
* Las estructuras de unidad, que no tienen campo, son útiles para genéricos.

```rust,editable
#[derive(Debug)]
struct Persona {
    nombre: String,
    edad: u8,
}

// Una estructura de unidad
struct Unidad;

// Una estructura de tupla
struct Par(i32, f32);

// Una estructura con dos campos
struct Punto {
    x: f32,
    y: f32,
}

// Las estructuras se pueden reutilizar como campos de otra estructura
#[allow(dead_code)]
struct Rectangulo {
    // Se puede especificar un rectángulo por el lugar en el que se encuentran
    // las esquinas superior izquierda e inferior derecha en el espacio.
    superior_izquierda: Punto,
    inferior_derecha: Punto,
}

fn main() {
    // Crear una estructura con inicialización de campo
    let nombre  = String::from("Pedro");
    let edad = 27;
    let pedro = Persona { nombre, edad };

    // Imprimir estructura de depuración
    println!("{:?}", pedro);

    // Crear una instancia de un `Punto`
    let punto: Punto = Punto { x: 10.3, y: 0.4 };

    // Acceder a los campos del punto
    println!("coordendas del punto: ({}, {})", punto.x, punto.y);

    // Crear un nuevo punto usando la sintaxis de actualización de estructura
    // para usar los campos de nuestro otro
    let inferior_derecha = Punto { x: 5.2, ..punto };

    // `inferior_derecha.y` será el mismo que `punto.y` porque usamos ese campo
    // de `punto`
    println!("segundo punto: ({}, {})", inferior_derecha.x, inferior_derecha.y);

    // Desestructurar el punto usando un enlace `let`
    let Punto { x: borde_superior, y: borde_izquierdo} = punto;

    let _rectangulo = Rectangulo {
        // Instanciar una estructura es una expresión también
        superior_izquierda: Punto { x: borde_izquierdo, y: borde_superior },
        inferior_derecha: inferior_derecha,
    };

    // Instanciar una estructura de unidad
    let unidad = Unidad;

    // Instanciar una estructura de tupla
    let par = Par(1, 0.1);

    // Acceder a los campos de una estructura de tupla
    println!("par contiene {:?} y {:?}", par.0, par.1);

    // Desestructurar una estructura de tupla
    let Par(entero, decimal) = par;

    println!("par contiene {:?} y {:?}", entero, decimal);
}
```

### Actividad

1. Agrega una función `area_rectangulo` que calcule el área de un rectángulo
   (intenta usar la desestructuración anidada).

2. Agrega una función `cuadrado` que toma un `Punto` y una `f32` como
   argumentos, y devuelve un `Rectangulo` con su esquina inferior izquierda en
   el punto, y un ancho y alto correspondientes a `f32`.

<!--
### See also

[`attributes`][attributes], y [destructuring][destructuring]
-->

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md
