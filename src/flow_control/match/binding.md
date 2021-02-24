# Enlace

Acceder indirectamente a una variable hace que sea imposible bifurcar y usar
esa variable sin volver a enlazar. `match` proporciona el sigilo `@` para
vincular valores a nombres:

```rust,editable
// Una función `edad` que devuelve un `u32`.
fn edad() -> u32 {
    15
}

fn main() {
    println!("Dime qué tipo de persona eres");

    match edad() {
        0             => println!("Aún no he celebrado mi primer cumpleaños"),
        // Podría coincidir 1 ..= 12 directamente pero entonces qué edad
        // ¿Sería el niño? En su lugar, enlaza con `n` para la
        // secuencia de 1 ..= 12. Ahora se puede informar la edad.
        n @ 1  ..= 12 => println!("Soy un niño de edad {:?}", n),
        n @ 13 ..= 19 => println!("Soy un adolescente de edad {:?}", n),
        // Nada enlazado. Devuelve el resultado.
        n             => println!("Soy una persona mayor de edad {:?}", n),
    }
}
```

También puedes utilizar el enlace para "desestructurar" variantes de `enum`,
como `Option`:

```rust,editable
fn algun_numero() -> Option<u32> {
    Some(42)
}

fn main() {
    match algun_numero() {
        // Obtuve la variante `Some`, coincide si su valor, vinculado a `n`,
        // es igual a 42.
        Some(n @ 42) => println!("La respuesta: {}!", n),
        // Match any other number.
        Some(n)      => println!("No es interesante... {}", n),
        // Coincide con cualquier otra cosa (variante `None`).
        _            => (),
    }
}
```

### Ve también:

[`enums`][enums]

<!--[`functions`][functions], [`enums`][enums] y [`Option`][option] -->

[functions]: ../../fn.md
[enums]: ../../custom_types/enum.md
[option]: ../../std/option.md
