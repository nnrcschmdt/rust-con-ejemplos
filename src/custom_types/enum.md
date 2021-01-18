# Enumeraciones

La palabra clave `enum` permite la creación de un tipo que puede ser una de las
muchas variantes diferentes. Cualquier variante que sea válida como una
`struct` también es válida como una `enum`.

```rust,editable
// Crea una `enum` para clasificar un evento web. Nota como los nombres y la
// información de tipo juntos especifican la variante:
// `PageLoad != PageUnload` y `KeyPress(char) != Paste(String)`.
// Cada uno es diferente e independiente.
enum EventoWeb {
    // Una `enum` puede ser `similar a una unidad`,
    PaginaCargada,
    PaginaDescargada,
    // estructuras de tupla,
    Presionada(char),
    Pegado(String),
    // o estructuras similares a C.
    Click { x: i64, y: i64 },
}

// Una función que toma una enumeración `WebEvent` como argumento y no
// devuelve nada.
fn inspecciona(event: EventoWeb) {
    match event {
        EventoWeb::PaginaCargada => println!("página cargada"),
        EventoWeb::PaginaDescargada=> println!("página descargada"),
        // Desestructurar `c` desde dentro de la `enum`.
        EventoWeb::Presionada(c) => println!("'{}' presionada.", c),
        EventoWeb::Pegado(s) => println!("\"{}\" pegado.", s),
        // Desestructurar `Click` en `x` e `y`.
        EventoWeb::Click { x, y } => {
            println!("click hecho en x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let presionado = EventoWeb::Presionada('x');
    // `to_owned()` crea un `String` propio de un segmento de una cadena.
    let pegado = EventoWeb::Pegado("mi texto".to_owned());
    let click   = EventoWeb::Click { x: 20, y: 80 };
    let cargada = EventoWeb::PaginaCargada;
    let descargada = EventoWeb::PaginaDescargada;

    inspecciona(presionado);
    inspecciona(pegado);
    inspecciona(click);
    inspecciona(cargada);
    inspecciona(descargada);
}

```

## Alias de tipo

Si usas un alias de tipo, puedes hacer referencia a cada variante de
enumeración a través de su alias. Esto puede resultar útil si el nombre de la
enumeración es demasiado largo o demasiado genérico y deseas cambiarle el
nombre.

```rust,editable
enum EnumeracionVerbosaDeCosasQueHacerConNumeros {
    Anadir,
    Substraer,
}

// Crear un alias de tipo
type Operations = EnumeracionVerbosaDeCosasQueHacerConNumeros;

fn main() {
    // Podemos referirnos a cada variante mediante su alias, no su nombre largo
    // e inconveniente. 
    let x = Operations::Anadir;
}
```

El lugar más común donde verás esto es en los bloques `impl` usando el alias
`Self`.

```rust,editable
enum EnumeracionVerbosaDeCosasQueHacerConNumeros {
    Anadir,
    Substraer,
}

impl EnumeracionVerbosaDeCosasQueHacerConNumeros {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Anadir => x + y,
            Self::Substraer => x - y,
        }
    }
}
```

Para obtener más información sobre las enumeraciones y los alias de tipos,
puedes leer el [informe de estabilización][aliasreport] de cuando esta función
se estabilizó en Rust.

### Ve también

<!--[`match`][match], [`fn`][fn], and [`String`][str], -->

["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html
