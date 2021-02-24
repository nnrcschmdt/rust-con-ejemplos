# punteros/referencias

Para los punteros, se debe hacer una distinción entre desestructuración y
desreferenciación, ya que son conceptos diferentes que se usan de manera
diferente a un lenguaje como `C`.

* Desreferenciación usa `*`
* Desestructuración usa `&`, `ref`, y `ref mut`

```rust,editable
fn main() {
    // Asigna una referencia de tipo `i32`. El `&` significa que hay una
    // referencia asignada.
    let referencia = &4;

    match referencia {
        // Si el patrón de `referencia` coincide con `&val`, el resultado es
        // una comparación como:
        // `&i32`
        // `&val`
        // ^ Vemos que si se eliminan los `&`s coincidentes, entonces el `i32`
        // debe asignarse a `val`.
        &val => println!("Obtuve un valor a través de la desestructuración: {:?}", val),
    }

    // Para evitar el `&`, elimina la referencia antes de hacer coincidir.
    match *referencia {
        val => println!("Obtuve un valor a través de la eliminación de referencias: {:?}", val),
    }

    // ¿Qué pasa si no empiezas con una referencia? `reference` era un `&` 
    // porque el lado derecho ya era una referencia. Esto no es una referencia
    // porque el lado derecho no es uno.

    let _no_es_una_referencia = 3;

    // Rust proporciona `ref` exactamente para este propósito. Modifica la
    // asignación para que se cree una referencia para el elemento; se asigna
    // esta referencia.

    let ref _es_una_referencia = 3;

    // En consecuencia, al definir 2 valores sin referencias, las referencias
    // se pueden recuperar mediante `ref` y `ref mut`.

    let valor = 5;
    let mut valor_mutable = 6;

    // Utiliza la palabra clave `ref` para crear una referencia.
    match valor {
        ref r => println!("Obtuve una referencia a un valor: {:?}", r),
    }

    // Usa `ref mut` de manera similar
    match valor_mutable {
        ref mut m => {
          // Obtuve una referencia. Tengo que eliminar la referencia antes de
          // que podamos agregarle algo.
            *m += 10;
            println!("Añadimos 10. `valor_mutable`: {:?}", m);
        },
    }
}
```
<!--
### See also:

[The ref pattern](../../../scope/borrow/ref.md)
-->
