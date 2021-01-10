# Caso de prueba: Impresión de una lista

Implementar `fmt::Display` para una estructura donde los elementos deben
manejarse secuencialmente es complicado. El problema es que cada `write!`
genera un `fmt::Result`. El manejo adecuado de esto requiere lidiar con *todos*
los resultados. Rust proporciona el operador `?` exactamente para este
propósito.

Usar `?` en `write!` se ve así:

```rust,ignore
// Prueba `write!` para ver si hay errores. Si falla, regresa el error. De lo
// contrario, continúa.
write!(f, "{}", value)?;
```

Con `?` disponible, implementar `fmt::Display` para un `Vec` es sencillo:

```rust,editable
use std::fmt; // Importa el módulo `fmt`.

// Define una estructura llamada `Lista` que contenga un `Vec`.
struct Lista(Vec<i32>);

impl fmt::Display for Lista {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Extrae el valor usando la indexación de tuplas, y crea una
        // referencia a `vec`.
        let vec = &self.0;

        write!(f, "[")?;


        // Itera sobre `v` en `vec` mientras enumera el contador de iteración
        // en `count`.
        for (count, v) in vec.iter().enumerate() {
            // Para cada elemento excepto el primero, agrega una coma.
            // Utiliza el operador ? para devolver los errores.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // Cierra el corchete abierto y devuelve un valor fmt::Result.
        write!(f, "]")
    }
}

fn main() {
    let v = Lista(vec![1, 2, 3]);
    println!("{}", v);
}
```

### Actividad

Intenta cambiar el programa para que también se imprima el índice de cada
elemento en el vector. La nueva salida debería verse así:

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

<!--
### See also:

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], and [`vec!`][vec]
-->

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md
