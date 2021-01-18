# constantes

Rust tiene dos tipos diferentes de constantes que pueden declararse en
cualquier ámbito, incluido el global. Ambos requieren una anotación de tipo
explícita:

* `const`: Un valor inmutable (el caso común).
* `static`: Una variable posiblemente `mut`able con una vida útil `'static`
  <!--[`'static`][static]-->. La vida útil estática se infiere y no es
  necesario especificarla. Acceder o modificar una variable estática mutable
  es una operacción `insegura`. <!-- [`inseguro`][unsafe] -->

```rust,editable,ignore,mdbook-runnable
// Los globales se declaran fuera de todos los demás ámbitos.
static LENGUAJE: &str = "Rust";
const UMBRAL: i32 = 10;

fn es_grande(n: i32) -> bool {
    // Acceso constante en alguna función
    n > UMBRAL 
}

fn main() {
    let n = 16;

    // Acceder a las constantes en el hilo principal
    println!("Esto es {}", LENGUAJE);
    println!("El umbral es {}", UMBRAL);
    println!("{} es {}", n, if es_grande(n) { "grande" } else { "pequeño" });

    // ¡Error! No se puede modificar una `const`.
    UMBRAL = 5;
    // FIXME ^ Commenta esta línea
}
```

### Ve también

[El RFC `const`/`static`](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md)
<!-- [`'static` lifetime][static] -->

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md
