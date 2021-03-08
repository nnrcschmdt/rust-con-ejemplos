# Iterator::any

`Iterator::any` es una función que, cuando se le pasa un iterador, devolverá
`true` si algún elemento satisface el predicado. De lo contrario, `false`. Su
signatura:

```rust,ignore
pub trait Iterator {
    // El tipo sobre el que se itera
    type Item;

    // `any` toma `&mut self`, lo que significa que la persona que llama puede
    // ser prestada y modificado, pero no consumido.
    fn any<F>(&mut self, f: F) -> bool where
        // `FnMut` significa que cualquier variable capturada puede ser como
        // máximo modificada, no consumido. `Self::Item` dice que se necesita
        // argumentos a la clausura por valor.
        F: FnMut(Self::Item) -> bool {}
}
```

```rust,editable
fn main() {
    let vec1 = vec![1, 2, 3];
    let vec2 = vec![4, 5, 6];

    // `iter()` para vecs produce `& i32`. Desestructurar a `i32`.
    println!("2 en vec1: {}", vec1.iter()     .any(|&x| x == 2));
    // `into_iter()` para vecs produce `i32`. No se requiere desestructuración.
    println!("2 en vec2: {}", vec2.into_iter().any(| x| x == 2));

    let array1 = [1, 2, 3];
    let array2 = [4, 5, 6];

    // `iter()` para matrices produce `&i32`.
    println!("2 en array1: {}", array1.iter()     .any(|&x| x == 2));
    // `into_iter()` para matrices inusualmente produce `&i32`.
    println!("2 en array2: {}", array2.into_iter().any(|&x| x == 2));
}
```

### Ve también:

[`std::iter::Iterator::any`][any]

[any]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.any
