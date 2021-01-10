# Tipos elementales 

Rust proporciona acceso a una amplia variedad de `primitives`, tipos
elementales. Una muestra incluye:

### Escalares 

* enteros con signo: `i8`,` i16`, `i32`,` i64`, `i128` e `isize` (tamaño del
  puntero)
* enteros sin signo: `u8`,` u16`, `u32`,` u64`, `u128` y `usize` (tamaño del
  puntero)
* coma flotante: `f32`,` f64`
* `char` valores escalares Unicode como `'a'`, `'α'` y `'∞'` (4 bytes cada uno)
* `bool` ya sea `true` o `false`
* y el tipo de unidad `()`, cuyo único valor posible es una tupla vacía: `()`

A pesar de que el valor de un tipo de unidad es una tupla, no se considera un
tipo compuesto porque no contiene múltiples valores.

### Tipos compuestos

* vectores como `[1, 2, 3]`
* tuplas como `(1, true)`

El tipo de las variables siempre puede ser anotado. Los números también pueden
ser anotados mediante un *sufijo* o con un valor *predeterminado*.  Los números
enteros están predeterminados en `i32` y los números de coma flotante `f64`.
Ten en cuenta que Rust también puede inferir tipos a partir del contexto.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // El tipo de las variables puede ser anotado.
    let booleano: bool = true;

    let una_coma_flotante: f64 = 1.0;  // Anotación regular
    let un_entero              = 5i32; // Anotación mediante sufijo

    // O se utilizará un valor predeterminado.
    let coma_flotante_predeterminado = 3.0; // `f64`
    let entero_predeterminado        = 7;   // `i32`
    
    // Un tipo también se puede inferir del contexto
    let mut tipo_inferido = 12; // El tipo i64 se infiere de otra línea
    tipo_inferido = 4294967296i64;
    
    // Se puede cambiar el valor de una variable mutable.
    let mut mutable = 12; // `i32` mutable
    mutable = 21;
    
    // ¡Error! El tipo de una variable no se puede cambiar.
    mutable = true;
    
    // Las variables se pueden sobrescribir con sombreado (shadowing).
    let mutable = true;
}
```

### Ve también

[la biblioteca `std`][std]
<!--, [`mut`][mut], [`inference`][inference], and [`shadowing`][shadowing] -->

[std]: https://doc.rust-lang.org/std/
[mut]: variable_bindings/mut.md
[inference]: types/inference.md
[shadowing]: variable_bindings/scope.md
