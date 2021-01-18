# uso

La declaración `use` se puede usar para que no sea necesario el ámbito manual:

```rust,editable
// Un atributo para ocultar advertencias de código no utilizado.
#![allow(dead_code)]

enum Estatus {
    Rico,
    Pobre,
}

enum Trabajo {
    Civil,
    Soldado,
}

fn main() {
    // `use` explícitamente cada nombre para que estén disponibles sin ámbito
    // manual.
    use crate::Estatus::{Pobre, Rico};
    // Automáticamente `use` cada nombre dentro de `Trabajo`.
    use crate::Trabajo::*;

    // Equivalente a `Estatus::Pobre`.
    let estatus = Pobre;
    // Equivalente a `Trabajo::Civil`.
    let trabajo = Civil;

    match estatus {
        // Ten en cuenta la falta de ámbito debido al `use` explícito anterior.
        Rico => println!("¡Los ricos tienen mucho dinero!"),
        Pobre => println!("Los pobres no tienen dinero ..."),
    }

    match trabajo {
        // Ten en cuenta nuevamente la falta de ámbito.
        Civil => println!("¡Los civiles trabajan!"),
        Soldado  => println!("¡Los soldados luchan!"),
    }
}
```

<!--
### See also:

[`match`][match] and [`use`][use] 
-->

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md
