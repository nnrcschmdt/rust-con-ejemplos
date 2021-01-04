# Para mostrar

`fmt::Debug` apenas parece compacto y limpio, por lo que a menudo es ventajoso
personalizar la apariencia de salida. Esto se hace implementando manualmente
[`fmt::Display`][fmt], que usa el marcador de impresión `{}`. Implementarlo se
ve así:

```rust
// Importa (a través de `use`) el módulo `fmt` para que esté disponible.
use std::fmt;

// Define una estructura para la cual se implementará `fmt::Display`. Esta es
// una estructura de tupla llamada `Estructura` que contiene un `i32`.
struct Estructura(i32);

// Para usar el marcador `{}`, se debe implementar el rasgo `fmt::Display`
// manualmente para el tipo.
impl fmt::Display for Estructura {
    // Este rasgo requiere `fmt` con esta firma exacta.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Escribe estrictamente el primer elemento en la secuencia de salida
        // proporcionada: `f`. Devuelve `fmt::Result` que indica si la
        // operación es exitosa o fallida. Ten en cuenta que `write!` usa una
        // sintaxis que es muy similar a `println!`. 
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display` puede ser más limpio que `fmt::Debug` pero esto presenta un
problema para la biblioteca `std`. ¿Cómo se deben mostrar los tipos ambiguos?
Por ejemplo, si la biblioteca `std` implementó un solo estilo para todos los
`Vec<T>`, ¿qué estilo debería ser? ¿Sería alguno de estos dos?

* `Vec <ruta>`: `/:/etc:/home/usuario:/bin` (dividido en `:`)
* `Vec <número>`: `1,2,3` (dividido en `,`)

No, porque no existe un estilo ideal para todos los tipos y la biblioteca `std`
no pretende imponer uno. `fmt::Display` no está implementado para `Vec<T>` ni
para ningún otro contenedor genérico. `fmt::Debug` debe usarse entonces para
estos casos genéricos.

Sin embargo, esto no es un problema porque para cualquier nuevo tipo
*contenedor* que *no* sea genérico, se puede implementar `fmt::Display`.

```rust,editable
use std::fmt; // Importa `fmt`

// Una estructura con dos números. `Debug` se derivará para que los resultados
// puedan contrastarse con `Display`.
#[derive(Debug)]
struct MinMax(i64, i64);

// Implementa `Display` para `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Utiliza `self.number` para referirse a cada punto de datos posicionales.
        write!(f, "({}, {})", self.0, self.1)
    }
}

// Define una estructura en la que los campos se puedan nombrar para comparar.
#[derive(Debug)]
struct Punto2D {
    x: f64,
    y: f64,
}

// De manera similar, implementa `Display` para `Punto2D`
impl fmt::Display for Punto2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Personalice de modo que solo se denoten `x` y `y`.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Compara estructuras:");
    println!("Para mostrar: {}", minmax);
    println!("Para depurar: {:?}", minmax);

    let rango_grande = MinMax(-300, 300);
    let rango_pequeno = MinMax(-3, 3);

    println!("El rango grande es {grande} y el pequeño es {pequeño}",
             pequeño = rango_pequeno,
             grande = rango_grande);

    let punto = Punto2D { x: 3.3, y: 7.2 };

    println!("Compara puntos:");
    println!("Para mostrar: {}", punto);
    println!("Para depurar: {:?}", punto);

    // Error. Se implementaron tanto `Debug` como` Display`, pero `{:b}`
    // requiere que se implemente `fmt::Binary`. Esto no funcionará.
    // println!("¿Cómo se ve Punto2D en binario: {:b}?", punto);
}
```

Entonces, `fmt::Display` se ha implementado pero `fmt::Binary` no, y por lo
tanto no se puede usar. `std :: fmt` tiene muchos de esos `rasgos`
<!--[`rasgos`][traits] --> y cada uno requiere su propia implementación. Esto
se detalla más en [`std::fmt`][fmt].

### Actividades

Después de verificar el resultado del ejemplo anterior, use la estructura
`Punto2D` como guía para agregar una estructura compleja al ejemplo. Cuando se
imprime de la misma manera, la salida debe ser:

```txt
Para mostrar: 3.3 + 7.2i
Para depurar: Complex { real: 3.3, imag: 7.2 }
```

### Ve también

<!-- [`derive`][derive], --> [`std::fmt`][fmt] <!--, [`macros`][macros],
  [`struct`][structs], [`trait`][traits], y [`use`][use] -->

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: ../../trait.md
[use]: ../../mod/use.md
