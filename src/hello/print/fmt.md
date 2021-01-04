# Formateo 

Hemos visto que el formato se especifica mediante una *cadena de formateo*:

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` -> [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

La misma variable (`foo`) se puede formatear de manera diferente dependiendo de
qué *tipo de argumento* se use: `X` vs `o` vs *no especificado*.

Esta funcionalidad de formateo se implementa a través de rasgos y hay un rasgo
para cada tipo de argumento. El rasgo de formato más común es `Display`, que
maneja casos donde el tipo de argumento se deja sin especificar: `{}` por
ejemplo.

```rust,editable
use std::fmt::{self, Formatter, Display};

struct Ciudad {
    nombre: &'static str,
    // Latitud
    lat: f32,
    // Longitud
    lon: f32,
}

impl Display for Ciudad {
    // `f` es un búfer, y este método debe escribir la cadena formateada en él
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!` es como `format!`, pero escribirá la cadena formateada en
        // un búfer (el primer argumento)
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.nombre, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Color {
    rojo: u8,
    verde: u8,
    azul: u8,
}

fn main() {
    for ciudad in [
        Ciudad { nombre: "Dublin", lat: 53.347778, lon: -6.259722 },
        Ciudad { nombre: "Oslo", lat: 59.95, lon: 10.75 },
        Ciudad { nombre: "Vancouver", lat: 49.25, lon: -123.1 },
    ].iter() {
        println!("{}", *ciudad);
    }
    for color in [
        Color { rojo: 128, verde: 255, azul: 90 },
        Color { rojo: 0, verde: 3, azul: 254 },
        Color { rojo: 0, verde: 0, azul: 0 },
    ].iter() {
        // Cambie esto para usar {} una vez que haya agregado una
        // implementación para fmt::Display.
        println!("{:?}", *color);
    }
}
```

Puedes ver una [lista completa de rasgos de formateo][fmt_traits] y sus tipos
de argumentos en la documentación de [`std::fmt`][fmt].

### Actividad

Agrega una implementación del rasgo `fmt::Display` para la estructura `Color`
anterior para que la salida se muestre como:

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

Dos pistas si te quedas atascado:
* Es posible que [tenga que enumerar cada color más de una
  vez][named_parameters],
* Puedes [rellenar con ceros hasta un ancho de 2][fmt_width] con `:02`.

### Ve también

[`std::fmt`][fmt]

[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width
