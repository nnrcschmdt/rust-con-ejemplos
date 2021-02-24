# match

Rust proporciona coincidencia de patrones a través de la palabra clave `match`,
que se puede usar como un `switch` en C. Se evalúa el primer brazo coincidente
y se deben cubrir todos los valores posibles.

```rust,editable
fn main() {
    let numero = 13;
    // TODO ^ Prueba diferentes valores para `numero`

    println!("Háblame de {}", numero);
    match numero {
        // Coincide con un solo valor
        1 => println!("¡Uno!"),
        // Coincide con varios valores
        2 | 3 | 5 | 7 | 11 => println!("Este es un primo"),
        // TODO ^ Intenta agregar 13 a la lista de valores primos
        // Coincide con un rango inclusivo
        13..=19 => println!("Un teen"),
        // Manejar el resto de casos
        _ => println!("No es especial"),
        // TODO ^ Intenta comentar este brazo general
    }

    let booleano = true;
    // Match es una expresión también
    let binario = match booleano {
        // Los brazos de un match deben cubrir todos los valores posibles
        false => 0,
        true => 1,
        // TODO ^ Intenta comentar uno de estos brazos
    };

    println!("{} -> {}", booleano, binario);
}
```
