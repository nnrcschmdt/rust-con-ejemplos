# loop

Rust proporciona una palabra clave `loop` para indicar un bucle infinito.

La instrucción `break` se puede usar para salir de un bucle en cualquier
momento, mientras que la instrucción `continue` se puede usar para omitir el
resto de la iteración y comenzar una nuevo.

```rust,editable
fn main() {
    let mut contador = 0u32;

    println!("¡Contemos hasta el infinito!");

    // Bucle infinito
    loop {
        contador += 1;

        if contador == 3 {
            println!("tres");

            // Omite el resto de esta iteración
            continue;
        }

        println!("{}", contador);

        if contador == 5 {
            println!("OK, es suficiente");

            // Salir de este bucle
            break;
        }
    }
}
```
