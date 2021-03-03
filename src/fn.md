# Funciones

Las funciones se declaran utilizando la palabra clave `fn`. Sus argumentos
tienen anotaciones de tipo, al igual que las variables, y, si la función
devuelve un valor, el tipo de retorno debe especificarse después de una flecha
`->`.

La expresión final de la función se utilizará como valor de retorno.
Alternativamente, la declaración `return` puede usarse para devolver un valor
anterior desde dentro de la función, incluso desde dentro de bucles o
declaraciones` if`.

¡Reescribamos FizzBuzz usando funciones!

```rust,editable
// A diferencia de C/C++, no hay restricciones en el orden de las definiciones
// de funciones
fn main() {
    // Podemos usar esta función aquí y definirla en algún lugar más adelante.
    fizzbuzz_to(100);
}

// Función que devuelve un valor booleano
fn es_divisible_por(lhs: u32, rhs: u32) -> bool {
    // Caso patológico, devolución anticipada
    if rhs == 0 {
        return false;
    }

    // Esta es una expresión, la palabra clave `return` no es necesaria aquí
    lhs % rhs == 0
}

// Las funciones que "no" devuelven un valor, en realidad devuelven el tipo de
// unidad `()`
fn fizzbuzz(n: u32) -> () {
    if es_divisible_por(n, 15) {
        println!("fizzbuzz");
    } else if es_divisible_por(n, 3) {
        println!("fizz");
    } else if es_divisible_por(n, 5) {
        println!("buzz");
    } else {
        println!("{}", n);
    }
}

// Cuando una función devuelve `()`, el tipo de retorno se puede omitir de la
// firma
fn fizzbuzz_to(n: u32) {
    for n in 1..n + 1 {
        fizzbuzz(n);
    }
}
```
