# if/else

La ramificación con `if`-`else` es similar a otros idiomas. A diferencia de
muchos de ellos, la condición booleana no necesita estar entre paréntesis y
cada condición va seguida de un bloque. Los condicionales `if`-`else` son
expresiones, y todas las ramas deben devolver el mismo tipo.

```rust,editable
fn main() {
    let n = 5;

    if n < 0 {
        print!("{} es negativo", n);
    } else if n > 0 {
        print!("{} es positivo", n);
    } else {
        print!("{} es zero", n);
    }

    let n_grande =
        if n < 10 && n > -10 {
            println!(", y es un número pequeño, aumentalo diez veces");

            // Esta expresión devuelve un `i32`.
            10 * n
        } else {
            println!(", y es un número grande, reducelo a la mitad");

            // Esta expresión debe devolver un `i32` también.
            n / 2
            // TODO ^ Intenta suprimir esta expresión con un punto y coma.
        };
    //   ^ ¡No olvides poner un punto y coma aquí! Todos los enlaces `let` lo
    //     necesitan.

    println!("{} -> {}", n, n_grande);
}
```
