# Anonimato de tipo

Las clausuras capturan de forma sucinta las variables de los ámbitos adjuntos. 
¿Tiene esto alguna consecuencia? Seguramente lo hace. Observa cómo el uso de
una clausura como parámetro de función requiere `genéricos`, lo cual es
necesario debido a cómo se definen:

```rust
// `F` debe ser genérico
fn apply<F>(f: F) where
    F: FnOnce() {
    f();
}
```

Cuando se define una clausura, el compilador crea implícitamente una nueva
estructura anónima para almacenar las variables capturadas en el interior,
mientras tanto implementa la funcionalidad a través de uno de los `rasgos`:
`Fn`, `FnMut` o `FnOnce` para este tipo desconocido. Este tipo se asigna a la
variable que se almacena hasta la llamada.

Dado que este nuevo tipo es de tipo desconocido, cualquier uso en una función
requerirá genéricos. Sin embargo, un parámetro de tipo ilimitado `<T>` aún
sería ambiguo y no estaría permitido. Por lo tanto, limitarse a uno de los
`rasgos`:` Fn`, `FnMut` o `FnOnce` (que implementa) es suficiente para
especificar su tipo.

```rust,editable
// `F` debe implementar `Fn` para una clausura que no requiere entradas y no
// devuelve nada, exactamente lo que se requiere para `imprimir`.
fn apply<F>(f: F) where
    F: Fn() {
    f();
}

fn main() {
    let x = 7;

    // Captura `x` en un tipo anónimo e implementa `Fn` para ello.
    // Guárdalo en `imprimir`.
    let imprimir = || println!("{}", x);

    apply(imprimir);
}
```

### Ve también:

[Un análisis completo][thorough_analysis], [`Fn`][fn], [`FnMut`][fn_mut],
and [`FnOnce`][fn_once]

[generics]: ../../generics.md
[fn]: https://doc.rust-lang.org/std/ops/trait.Fn.html
[fn_mut]: https://doc.rust-lang.org/std/ops/trait.FnMut.html
[fn_once]: https://doc.rust-lang.org/std/ops/trait.FnOnce.html
[thorough_analysis]: https://huonw.github.io/blog/2015/05/finding-closure-in-rust/
