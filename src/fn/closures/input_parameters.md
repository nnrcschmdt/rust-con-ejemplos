# Como parámetros de entrada

Si bien Rust elige cómo capturar variables sobre la marcha principalmente sin
anotaciones de tipo, esta ambigüedad no está permitida al escribir funciones.
Cuando se toma una clausura como parámetro de entrada, el tipo completo de la
clausura debe anotarse utilizando uno de los pocos `traits` (rasgos). En orden
de restricción decreciente, son:

* `Fn`: la clausura captura por referencia (`& T`)
* `FnMut`: la clausura captura por referencia mutable (`&mut T`)
* `FnOnce`: la clausura captura por valor (`T`)

Variable por variable, el compilador capturará las variables de la manera menos
restrictiva posible.

Por ejemplo, considera un parámetro anotado como `FnOnce`. Esto especifica que
la clausura *puede* ser capturada por `& T`, `&mut T` o `T`, pero el compilador
elegirá en última instancia en función de cómo se utilizan las variables
capturadas en la clausura.

Esto se debe a que si un movimiento es posible, entonces también debería ser
posible cualquier tipo de préstamo. Ten en cuenta que lo contrario no es
cierto.  Si el parámetro está anotado como `Fn`, no se permite la captura de
variables con `&mut T` o `T`.

En el siguiente ejemplo, intenta intercambiar el uso de `Fn`, `FnMut` y `FnOnce`
para ver qué sucede:

```rust,editable
// Una función que toma una clausura como argumento y la llama.
// <F> denota que F es un "parámetro de tipo genérico"
fn apply<F>(f: F) where
    // La clausura no tiene entrada y no devuelve nada.
    F: FnOnce() {
    // ^ TODO: Intenta cambiar esto a `Fn` o `FnMut`.

    f();
}

// Una función que toma una clausura y devuelve un `i32`.
fn apply_to_3<F>(f: F) -> i32 where
    // La clausura toma un `i32` y devuelve un `i32`.
    F: Fn(i32) -> i32 {

    f(3)
}

fn main() {
    use std::mem;

    let saludo = "hola";
    // Un tipo sin copia.
    // `to_owned` crea datos propios de los prestados
    let mut despedida = "adios".to_owned();

    // Captura 2 variables: `saludo` por referencia y
    // `despedida` por valor.
    let diario = || {
        // `saludo` es por referencia: requiere `Fn`.
        println!("Dije {}.", saludo);

        // La mutación obliga que `despedida` sea capturada por
        // referencia mutable. Ahora requiere `FnMut`.
        despedida.push_str("!!!");
        println!("Y luego grité {}.", despedida);
        println!("Ahora puedo dormir. zzzzz");

        // Llamar manualmente drop obliga a `despedida` a
        // ser capturada por valor. Ahora requiere `FnOnce`.
        mem::drop(despedida);
    };

    // Llame a la función que aplica la clausura.
    apply(diario);

    // `double` satisface el límite del rasgo de `apply_to_3`
    let doble = |x| 2 * x;

    println!("3 duplicado: {}", apply_to_3(doble));
}
```

### Ve también:

[`std::mem::drop`][drop], [`Fn`][fn], [`FnMut`][fnmut]
<!--, [Generics][generics], [where][where] and [`FnOnce`][fnonce] -->

[drop]: https://doc.rust-lang.org/std/mem/fn.drop.html
[fn]: https://doc.rust-lang.org/std/ops/trait.Fn.html
[fnmut]: https://doc.rust-lang.org/std/ops/trait.FnMut.html
[fnonce]: https://doc.rust-lang.org/std/ops/trait.FnOnce.html
[generics]: ../../generics.md
[where]: ../../generics/where.md
