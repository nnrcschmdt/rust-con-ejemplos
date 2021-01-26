# Congelación

Cuando los datos están enlazados por el mismo nombre de manera inmutable,
también *se congelan*. Los datos *congelados* no se pueden modificar hasta que el
enlace inmutable se salga del ámbito:

```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _entero_mutable = 7i32;

    {
        // Sombreado por inmutable `_entero_mutable`
        let _entero_mutable = _entero_mutable;

        // ¡Error! `_entero_mutable` está congelado en este ámbito
        _entero_mutable = 50;
        // FIXME ^ Comenta esta línea

        // `_entero_mutable` sale de ámbito
    }

    // ¡Ok! `_entero_mutable` no está congelado en este ámbito
    _entero_mutable = 3;
}
```
