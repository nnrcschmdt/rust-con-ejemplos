# Declaración anticipada

Es posible declarar enlaces de variables primero e inicializarlos más tarde.
Sin embargo, esta forma se usa raras veces, ya que puede dar lugar al uso de
variables no inicializadas.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Declarar un enlace variable
    let un_enlace;

    {
        let x = 2;

        // Inicializar el enlace
        un_enlace = x * x;
    }

    println!("un enlace: {}", un_enlace);

    let otro_enlace;

    // ¡Error! Uso de enlace no inicializado
    println!("otro enlace: {}", otro_enlace);
    // FIXME ^ Comenta esta línea

    otro_enlace = 1;

    println!("otro enlace: {}", otro_enlace);
}
```

El compilador prohíbe el uso de variables no inicializadas, ya que esto
conduciría a un comportamiento indefinido.
