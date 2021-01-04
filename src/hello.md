# Hola Mundo

Este es el código fuente del programa tradicional Hola Mundo.

```rust,editable

// Este es un comentario y el compilador lo ignora. Puedes probar este código
// haciendo clic en el botón "Ejecutar" que se encuentra allí -> o si prefieres
// usar su teclado, puedes usar el atajo "Ctrl + Enter"

// Este código es editable, ¡no dudes en hackearlo!
// Siempre puedes volver al código original haciendo clic en el botón
// "Restablecer" ->

// Esta es la función principal
fn main() {
    // Las declaraciones aquí se ejecutan cuando se llama al binario compilado

    // Imprimir texto en la consola
    println!("¡Hola, mundo!");
}
```

`println!` es un macro <!--[macro][macros]--> que imprime texto en la consola.

Se puede generar un binario usando el compilador Rust: `rustc`.

```bash
$ rustc hello.rs
```

`rustc` producirá un binario `hello` que se puede ejecutar.

```bash
$ ./hello
¡Hola, mundo!
```

### Actividad

Haz clic en 'Ejecutar' arriba para ver el resultado esperado. A continuación,
agrega una nueva línea con un segundo macro `println!` para que la salida
muestre:

```text
¡Hola, mundo!
¡Soy un Rustáceo!
```

[macros]: macros.md
