# Literales

Los literales numéricos se pueden anotar el tipo agregando el tipo como sufijo.
Por ejemplo, para especificar que el literal `42` debe tener el tipo `i32`,
escribe `42i32`.

El tipo de literales numéricos sin sufijo dependerá de cómo se utilicen. Si no
existe ninguna restricción, el compilador usará `i32` para números enteros y
`f64` para números de coma flotante.

```rust,editable
fn main() {
    // Literales con sufijo, sus tipos se conocen en la inicialización
    let x = 1u8;
    let y = 2u32;
    let z = 3f32;

    // Literales sin sufijo, sus tipos dependen de cómo se usan
    let i = 1;
    let f = 1.0;

    // `size_of_val` devuelve el tamaño de una variable en bytes
    println!("tamaño de `x` en bytes: {}", std::mem::size_of_val(&x));
    println!("tamaño de `y` en bytes: {}", std::mem::size_of_val(&y));
    println!("tamaño de `z` en bytes: {}", std::mem::size_of_val(&z));
    println!("tamaño de `i` en bytes: {}", std::mem::size_of_val(&i));
    println!("tamaño de `f` en bytes: {}", std::mem::size_of_val(&f));
}
```

Hay algunos conceptos utilizados en el código anterior que aún no se han
explicado, aquí hay una breve explicación para los lectores impacientes:

* `std::mem::size_of_val` es una función, pero se llama con su *ruta completa*.
  El código se puede dividir en unidades lógicas llamadas *módulos*. En este
  caso, la función `size_of_val` se define en el módulo `mem`, y el módulo
  `mem` se define en el crate `std`. Para obtener más detalles, consulta
  `modulos` y `crates`.

<!--  [módulos][mod] y [cajas][caja]. -->

[mod]: ../mod.md
[crate]: ../crates.md
