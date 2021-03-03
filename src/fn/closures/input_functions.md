# Funciones de entrada

Dado que las clausuras pueden usarse como argumentos, es posible que tes
preguntes si se puede decir lo mismo de las funciones. ¡Y de hecho pueden! Si
declaras una función que toma una clausura como parámetro, entonces cualquier
función que satisfaga el límite de rasgo de esa clausura se puede pasar como
parámetro.

```rust,editable
// Define una función que tome un argumento `F` genérico delimitado por `Fn`,
// y lo llama
fn llamame<F: Fn()>(f: F) {
    f();
}

// Define una función contenedora que satisfaga el límite `Fn`
fn funcion() {
    println!("¡Soy una función!");
}

fn main() {
    // Define una clausura que satisfaga el límite `Fn`
    let clausura = || println!("¡Soy una clausura!");

    llamame(clausura);
    llamame(funcion);
}
```

Como nota adicional, los rasgos `Fn`, `FnMut` y `FnOnce` dictan cómo una
clausura captura las variables del alcance adjunto.

### Ve también:

[`Fn`][fn], [`FnMut`][fn_mut], y [`FnOnce`][fn_once]

[fn]: https://doc.rust-lang.org/std/ops/trait.Fn.html
[fn_mut]: https://doc.rust-lang.org/std/ops/trait.FnMut.html
[fn_once]: https://doc.rust-lang.org/std/ops/trait.FnOnce.html
