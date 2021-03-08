# Buscar a través de iteradores

`Iterator::find` es una función que itera sobre un iterador y busca el primer
valor que satisface alguna condición. Si ninguno de los valores satisface la
condición, devuelve `None`. Su signatura:

```rust,ignore
pub trait Iterator {
    // El tipo sobre el que se itera
    type Item;

    // `find` toma `&mut self`, lo que significa que la persona que llama puede
    // ser prestada y modificada, pero no consumida.
    fn find<P>(&mut self, predicate: P) -> Option<Self::Item> where
        // `FnMut` significa que cualquier variable capturada puede ser como
        // máximo modificada, no consumida. `&Self::Item` indica que se
        // necesita argumentos a la clausura por referencia.
        P: FnMut(&Self::Item) -> bool {}
}
```

```rust,editable
fn main() {
    let vec1 = vec![1, 2, 3];
    let vec2 = vec![4, 5, 6];

    // `iter()` para vecs produce `&i32`.
    let mut iter = vec1.iter();
    // `into_iter()` para vecs produce `i32`.
    let mut into_iter = vec2.into_iter();

    // `iter()` para vecs produce `&i32`, y queremos referenciar a uno de sus
    // elementos, así que tenemos que desestructurar `&&i32` a `i32`
    println!("Encuentra 2 en vec1: {:?}", iter     .find(|&&x| x == 2));
    // `into_iter()` para vecs produce `i32`, y queremos referenciar a uno de
    // sus elementos, así que tenemos que desestructurar `&i32` a `i32`
    println!("Encuentra 2 en vec2: {:?}", into_iter.find(| &x| x == 2));

    let array1 = [1, 2, 3];
    let array2 = [4, 5, 6];

    // `iter()` para matrices produce `&i32`
    println!("Encuentra 2 en array1: {:?}", array1.iter()     .find(|&&x| x == 2));
    // `into_iter()` para matrices inusualmente produce `&i32`
    println!("Encuentra 2 en array2: {:?}", array2.into_iter().find(|&&x| x == 2));
}
```

`Iterator::find` te da una referencia al elemento. Pero si deseas el _índice_ del
elemento, usa `Iterator::position`.

```rust,editable
fn main() {
    let vec = vec![1, 9, 3, 3, 13, 2];

    let indice_del_primer_numero_par = vec.iter().position(|x| x % 2 == 0);
    assert_eq!(indice_del_primer_numero_par, Some(5));
    
    
    let indice_del_primer_numero_negativo = vec.iter().position(|x| x < &0);
    assert_eq!(indice_del_primer_numero_negativo, None);
}
```

### Ve también:

[`std::iter::Iterator::find`][find]

[`std::iter::Iterator::find_map`][find_map]

[`std::iter::Iterator::position`][position]

[`std::iter::Iterator::rposition`][rposition]

[find]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find
[find_map]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.find_map
[position]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.position
[rposition]: https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.rposition
