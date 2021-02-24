# estructuras

De manera similar, una `estructura` se puede desestructurar como se muestra:

```rust,editable
fn main() {
    struct Foo {
        x: (u32, u32),
        y: u32,
    }

    // Intenta cambiar los valores en la estructura para ver qué sucede
    let foo = Foo { x: (1, 2), y: 3 };

    match foo {
        Foo { x: (1, b), y } => println!("Primero de x es 1, b = {},  y = {} ", b, y),

        // puedes desestructurar estructuras y cambiar el nombre de las variables,
        // el orden no es importante
        Foo { y: 2, x: i } => println!("y es 2, i = {:?}", i),

        // y también puedes ignorar algunas variables:
        Foo { y, .. } => println!("y = {}, no nos importa x", y),
        // esto dará un error: el patrón no menciona el campo `x`
        //Foo { y } => println!("y = {}", y),
    }
}
```

### Ve también:

[Estructuras](../../../custom_types/structs.md)
