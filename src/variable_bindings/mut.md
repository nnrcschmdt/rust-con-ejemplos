# Mutabilidad

Los enlaces de variables son inmutables por defecto, pero esto se puede anular
usando el modificador `mut`.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _enlace_inmutable = 1;
    let mut enlace_mutable = 1;

    println!("Antes de la mutación: {}", enlace_mutable);

    // Ok
    enlace_mutable += 1;

    println!("Después de la mutation: {}", enlace_mutable);

    // Error!
    _enlace_inmutable += 1;
    // FIXME ^ Comenta esta línea
}
```

El compilador arrojará un diagnóstico detallado sobre errores de mutabilidad.
