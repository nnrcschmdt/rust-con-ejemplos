# while let

Similar a `if let`, `while let` puede hacer que las secuencias de `match`
incómodas sean más tolerables. Considera la siguiente secuencia que incrementa
`i`:

```rust
// Haz `opcional` del tipo `Option<i32>`
let mut opcional = Some(0);

// Intenta repetidamente esta prueba.
loop {
    match opcional {
        // Si `opcional` de desestructura, evalúa el bloque.
        Some(i) => {
            if i > 9 {
                println!("Mayor que 9, ¡abandona!");
                opcional = None;
            } else {
                println!("`i` es `{:?}`. Inténtalo de nuevo.", i);
                opcional = Some(i + 1);
            }
            // ^ ¡Requiere 3 sangrías!
        },
        // Sal del ciclo cuando falle la desestructuración:
        _ => { break; }
        // ^ ¿Por qué debería ser necesario? ¡Tiene que haber una mejor manera!
    }
}
```

El uso de `while let` hace que esta secuencia sea mucho más agradable:

```rust,editable
fn main() {
    // Haz `opcional` del tipo `Option<i32>`
    let mut opcional = Some(0);

    // Esto dice: mientras que `let` desestructura `opcional` en
    // `Some (i)`, evalúa el bloque (`{}`). De lo contrario, `break`.
    while let Some(i) = opcional {
        if i > 9 {
            println!("Mayor que 9, ¡abandona!");
            opcional = None;
        } else {
            println!("`i` es `{:?}`. Inténtalo de nuevo.", i);
            opcional = Some(i + 1);
        }
        // ^ Menos desviación hacia la derecha y no requiere
        // manejo explícito del caso fallido.
    }
    // ^ `if let` tenía clausulas cláusulas adicionales `else`/`else if`.
    // `while let` no tiene estas.
}
```

### Ve también:

[`enum`][enum]<!--, [`Option`][option], --> y el [RFC][while_let_rfc]

[enum]: ../custom_types/enum.md
[option]: ../std/option.md
[while_let_rfc]: https://github.com/rust-lang/rfcs/pull/214
