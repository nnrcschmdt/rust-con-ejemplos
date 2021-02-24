# Devolver desde bucles

Uno de los usos de un `loop` es reintentar una operación hasta que tenga éxito.
Sin embargo, si la operación devuelve un valor, es posible que deba pasarlo al
resto del código: colócalo después del `break`, y la expresión ` loop` lo
devolverá

```rust,editable
fn main() {
    let mut contador = 0;

    let resultado = loop {
        contador += 1;

        if contador == 10 {
            break contador * 2;
        }
    };

    assert_eq!(resultado, 20);
}
```
