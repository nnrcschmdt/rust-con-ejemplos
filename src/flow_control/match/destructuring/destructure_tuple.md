# tuplas

Las tuplas se pueden desestructurar en una `match` de la siguiente manera:

```rust,editable
fn main() {
    let triple = (0, -2, 3);
    // TODO ^ Prueba diferentes valores para `triple`

    println!("Háblame de {:?}", triple);
    // Match se puede utilizar para desestructurar una tupla
    match triple {
        // Desestructurar el segundo y tercer elemento
        (0, y, z) => println!("Primero es `0`, `y` es {:?}, y `z` es {:?}", y, z),
        (1, ..)   => println!("Primero es `1` y el resto no importa"),
        // `..` puede ser usado ignorar el resto de la tupla
        _         => println!("No importa lo que sean"),
        // `_` significa no vincular el valor a una variable
    }
}
```

### Ve también

[Tuplas](../../../primitives/tuples.md)
