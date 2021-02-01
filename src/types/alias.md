# Aliasing

La instrucción `type` puede usarse para dar un nuevo nombre a un tipo
existente. Los tipos deben tener nombres `UpperCamelCase`, o el compilador
generará una advertencia. La excepción a esta regla son los tipos elementales:
`usize`, `f32`, etc.

```rust,editable
// `NanoSegundo` es un nuevo nombre para `u64`.
type NanoSegundo = u64;
type Pulgada = u64;

// Utiliza un atributo para silenciar la advertencia.
#[allow(non_camel_case_types)]
type u64_t = u64;
// TODO ^ Intenta eliminar el atributo

fn main() {
    // `NanoSegundo` = `Pulgada` = `u64_t` = `u64`.
    let nanosegundos: NanoSegundo = 5 as u64_t;
    let pulgadas: Pulgada = 2 as u64_t;

    // Ten en cuenta que los alias de tipo *no* proporcionan ninguna seguridad
    // de tipo adicional, porque los alias *no* son tipos nuevos
    println!("{} nanosegundos + {} pulgadas = {} unidad?",
             nanosegundos,
             pulgadas,
             nanosegundos + pulgadas);
}
```

El uso principal de los alias es reducir el texto repetitivo; por ejemplo, el
tipo `IoResult <T>` es un alias para el tipo `Result <T, IoError>`.

<!--
### See also:

[Attributes](../attribute.md)
-->
