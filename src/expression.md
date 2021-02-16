# Expresiones

Un programa de Rust se compone (principalmente) de una serie de declaraciones:

```
fn main() {
    // declaración 
    // declaración
    // declaración
}
```

Hay varios tipos de declaraciones en Rust. Las dos más comunes son declarar un
enlace de variable y usar un `;` con una expresión:

```
fn main() {
    // enlace de variable
    let x = 5;

    // expresión;
    x;
    x + 1;
    15;
}
```

Los bloques también son expresiones, por lo que se pueden usar como valores en
las asignaciones. La última expresión del bloque se asignará a la expresión de
lugar, como una variable local. Sin embargo, si la última expresión del bloque
termina con un punto y coma, el valor de retorno será `()`.

```rust,editable
fn main() {
    let x = 5u32;

    let y = {
        let x_cuadrado = x * x;
        let x_cubo = x_cuadrado * x;

        // Esta expresión se asignará a `y`
        x_cubo + x_cuadrado + x
    };

    let z = {
        // El punto y coma suprime esta expresión y `()` se asigna a `z`
        2 * x;
    };

    println!("x es {:?}", x);
    println!("y es {:?}", y);
    println!("z es {:?}", z);
}
```
