# Similares a C

`enum` también se puede usar como enumeraciones similares a C.

```rust,editable
// Un atributo para ocultar advertencias de código no utilizado.
#![allow(dead_code)]

// enum con discriminador implícito (comienza en 0)
enum Numero {
    Cero,
    Uno,
    Dos,
}

// enum con discriminator explícito
enum Color {
    Rojo = 0xff0000,
    Verder = 0x00ff00,
    Azul = 0x0000ff,
}

fn main() {
    // `enums` se puede convertir en números enteros.
    println!("cero is {}", Numero::Cero as i32);
    println!("uno is {}", Numero::Uno as i32);

    println!("las rosas son #{:06x}", Color::Rojo as i32);
    println!("las violetas son #{:06x}", Color::Azul as i32);
}
```
<!--
### See also:

[casting][cast]
-->

[cast]: ../../types/cast.md
