# Como parámetros de salida

Las clausuras como parámetros de entrada son posibles, por lo que también
debería ser posible devolver clausuras como parámetros de salida. Sin embargo,
los tipos de clausuras anónimas son, por definición, desconocidos, por lo que
tenemos que usar `impl Trait` para devolverlos.

Los rasgos válidos para devolver un cierre son:

* `Fn`
* `FnMut`
* `FnOnce`

Más allá de esto, se debe usar la palabra clave `move`, que indica que todas
las capturas ocurren por valor. Esto es necesario porque cualquier captura por
referencia se eliminaría tan pronto como la función saliera, dejando
referencias no válidas en la clausura.

```rust,editable
fn crea_fn() -> impl Fn() {
    let texto = "Fn".to_owned();

    move || println!("Esta es una: {}", texto)
}

fn crea_fnmut() -> impl FnMut() {
    let texto = "FnMut".to_owned();

    move || println!("Esta es una: {}", texto)
}

fn crea_fnonce() -> impl FnOnce() {
    let texto = "FnOnce".to_owned();

    move || println!("Esta es una: {}", texto)
}

fn main() {
    let fn_simple = crea_fn();
    let mut fn_mut = crea_fnmut();
    let fn_once = crea_fnonce();

    fn_simple();
    fn_mut();
    fn_once();
}
```

### Ve también:

[`Fn`][fn], [`FnMut`][fnmut].
<!-- , [Generics][generics] and [impl Trait][impltrait]. -->

[fn]: https://doc.rust-lang.org/std/ops/trait.Fn.html
[fnmut]: https://doc.rust-lang.org/std/ops/trait.FnMut.html
[generics]: ../../generics.md
[impltrait]: ../../trait/impl_trait.md
