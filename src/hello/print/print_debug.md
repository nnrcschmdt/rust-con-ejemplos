# Para depuración

Todos los tipos que quieran utilizar `rasgos` de formateo `std::fmt` requieren
una implementación para poder imprimir. Las implementaciones automáticas solo
se proporcionan para tipos de la biblioteca `std`. Todos los demás *deben*
implementarse manualmente de alguna manera.

El rasgo `fmt::Debug` hace que esto sea muy sencillo. Todos los tipos pueden
`derivar` (crear automáticamente) la implementación `fmt::Debug`. Esto no es
cierto para `fmt::Display` que debe implementarse manualmente.

```rust
// Esta estructura no se puede imprimir con `fmt::Display` o
// con `fmt::Debug`.
struct Inimprimible(i32);

// El atributo `derive` crea automáticamente la implementación
// requerida para hacer esta `estructura` imprimible con `fmt::Debug`.
#[derive(Debug)]
struct ImprimibleEnDepuracion(i32);
```

Todos los tipos de bibliotecas `std` también se pueden imprimir automáticamente
con `{:?}`:

```rust,editable

// Derive la implementación `fmt::Debug` para `Estructura`. `Estructura` es una
// estructura que contiene un solo `i32`.
#[derive(Debug)]
struct Estructura(i32);

// Ponga la `Estructura` dentro de la estructura `Deep`. Hágala además
// imprimible.
#[derive(Debug)]
struct Deep(Estructura);

fn main() {
    // Imprimir con `{:?}` Es similar a imprimir con `{}`.
    println!("{:?} meses en un año.", 12);
    println!("{1:?} {0:?} es el nombre {actor:?}.",
             "Slater",
             "Christian",
             actor="del actor");

    // ¡`Estructura` es imprimible!
    println!("Ahora {:?} imprimirá", Estructura(3));
    
    // El problema con `derivar` es que no hay control sobre cómo se ven los
    // resultados. ¿Qué pasa si quiero que esto solo muestre un "7"?

    println!("Ahora {:?} imprimirá!", Deep(Estructura(7)));
}
```

Así, `fmt::Debug` definitivamente lo hace imprimible, pero sacrifica algo de
elegancia. Rust también proporciona "impresión bonita" con `{:#?}`.

```rust,editable
#[derive(Debug)]
struct Persona<'a> {
    nombre: &'a str,
    edad: u8
}

fn main() {
    let nombre = "Pedro";
    let edad = 27;
    let pedro = Persona { nombre, edad };

    // Impresión bonita
    println!("{:#?}", pedro);
}
```

Uno puede implementar manualmente `fmt::Display` para controlar cómo se muestra.

### Ve también

[`attributes`][attributes]<!--, [`derive`][derive], --> y [`std::fmt`][fmt]
<!--, and [`struct`][structs] -->

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md

