# A y desde String

## Convertir a String

Convertir cualquier tipo en un `String` es tan simple como implementar el rasgo
[`ToString`] para el tipo. En lugar de hacerlo directamente, debe implementar
el rasgo [`fmt::Display`][Display] que proporciona automáticamente [`ToString`]
y también permite imprimir el tipo como se explica en la sección sobre
[`print!`][Print].

```rust,editable
use std::fmt;

struct Circulo {
    radio: i32
}

impl fmt::Display for Circulo {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Circulo de radio {}", self.radio)
    }
}

fn main() {
    let circulo = Circulo { radio: 6 };
    println!("{}", circulo.to_string());
}
```

## Analizar un String

Uno de los tipos más comunes para convertir una cadena es un número. El enfoque
idiomático para esto es usar la función [`parse`] y arreglar la inferencia de
tipos o especificar el tipo a analizar usando la sintaxis 'turbofish'. Ambas
alternativas se muestran en el siguiente ejemplo.

Esto convertirá la cadena en el tipo especificado siempre que se implemente el
rasgo [`FromStr`] para ese tipo. Esto se implementa para numerosos tipos dentro
de la biblioteca estándar. Para obtener esta funcionalidad en un tipo definido
por el usuario, simplemente implemente el rasgo [`FromStr`] para ese tipo.

```rust,editable
fn main() {
    let analizado: i32 = "5".parse().unwrap();
    let turbo_analizado = "10".parse::<i32>().unwrap();

    let suma = analizado + turbo_analizado;
    println!("Suma: {:?}", suma);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html
