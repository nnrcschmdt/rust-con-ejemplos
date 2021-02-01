# Inferencia

El motor de inferencia de tipos es bastante inteligente. Hace más que mirar el
tipo de expresión de valor durante una inicialización. También analiza cómo se
usa la variable posteriormente para inferir su tipo. Aquí hay un ejemplo
avanzado de inferencia de tipos:

```rust,editable
fn main() {
    // Debido a la anotación, el compilador sabe que `elem` tiene el tipo u8.
    let elem = 5u8;

    // Crea un vector vacío (un vector ampliable).
    let mut vec = Vec::new();
    // En este punto, el compilador no conoce el tipo exacto de `vec`,
    // simplemente sabe que es un vector de algo (`Vec<_>`).

    // Inserta `elem` en el vector.
    vec.push(elem);
    // ¡Ajá! Ahora el compilador sabe que `vec` es un vector de `u8`s (`Vec<u8>`)
    // TODO ^ Intenta comentar la línea `vec.push(elem)`

    println!("{:?}", vec);
}
```

No se necesitó ninguna anotación de tipo de variables, ¡el compilador está
contento y también el programador!
