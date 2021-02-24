# while

La palabra clave `while` puede usarse para ejecutar un bucle mientras una
condición es verdadera.

Escribamos el infame [FizzBuzz][fizzbuzz] usando un bucle `while`.

```rust,editable
fn main() {
    // Una variable de contador
    let mut n = 1;

    // Repite el bucle mientras `n` es menor que 101
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // Incrementa el contador
        n += 1;
    }
}
```

[fizzbuzz]: https://en.wikipedia.org/wiki/Fizz_buzz
