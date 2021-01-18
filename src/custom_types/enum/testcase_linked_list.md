# Caso de prueba: Lista enlazada

Un uso común de `enum`s es crear una lista enlazada:

```rust,editable
use crate::Lista::*;

enum Lista {
    // Cons: Estructura de tupla que envuelve un elemento y un puntero al
    // siguiente nodo
    Cons(u32, Box<Lista>),
    // Nil: Un nodo que significa el final de la lista enlazada 
    Nil,
}

// Los métodos se pueden adjuntar a una enumeración
impl Lista {
    // Crea una lista vacía
    fn new() -> Lista {
        // `Nil` tiene el tipo `Lista`
        Nil
    }

    // Consume una lista y devuelve la misma lista con un nuevo elemento al
    // frente
    fn prepend(self, elem: u32) -> Lista {
        // `Cons` también tiene el tipo `Lista`
        Cons(elem, Box::new(self))
    }

    // Devuelve la longitud de la lista
    fn len(&self) -> u32 {
        // `self` tiene que coincidir, porque el comportamiento de este método
        // depende de la variante de `self`
        // `self` tiene el tipo `&Lista` y `*self` tiene el tipo `Lista`, se
        // prefiere la coincidencia con un tipo concreto `T` sobre una
        // coincidencia con una referencia `&T`
        match *self {
            // No se puede tomar posesión de la cola, porque se toma prestado
            // `self`; en su lugar, se toma una referencia a la cola
            Cons(_, ref tail) => 1 + tail.len(),
            // Caso base: una lista vacía tiene una longitud cero
            Nil => 0
        }
    }

    // Devuelve la representación de la lista como una cadena (asignada al
    // montículo)
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!` es similar a `print!`, pero devuelve una cadena
                // asignada al montículo en lugar de imprimir en la consola
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // Crear una lista vinculada vacía
    let mut lista = Lista::new();

    // Anteponer algunos elementos
    lista = lista.prepend(1);
    lista = lista.prepend(2);
    lista = lista.prepend(3);

    // Mostrar el estado final de la lista.
    println!("la lista enlazada tiene longitud: {}", lista.len());
    println!("{}", lista.stringify());
}
```

<!--
### See also:

[`Box`][box] and [methods][methods]
-->

[box]: ../../std/box.md
[methods]: ../../fn/methods.md
