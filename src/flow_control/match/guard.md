# Guardias

Un `match` *guard* se puede agregar para filtrar el brazo.

```rust,editable
fn main() {
    let par = (2, -2);
    // TODO ^ Prueba diferentes valores para `par`

    println!("Háblame de {:?}", par);
    match par {
        (x, y) if x == y => println!("Estos son mellizos"),
        // La parte ^ `if condition` es un guardia
        (x, y) if x + y == 0 => println!("¡Antimateria, kaboom!"),
        (x, _) if x % 2 == 1 => println!("El primero es impar"),
        _ => println!("Sin correlación..."),
    }
}
```

Tenga en cuenta que el compilador no comprueba las expresiones arbitrarias para
comprobar si se han comprobado todas las condiciones posibles. Por lo tanto,
debes utilizar el patrón `_` al final.

```rust,editable
fn main() {
    let numero: u8 = 4;

    match numero {
        i if i == 0 => println!("Cero"),
        i if i > 0 => println!("Mayor que cero"),
        _ => println!("Se cayó"), // Esto no debería ser posible de alcanzar
    }
}
```

### Ve también:

[Tuplas](../../primitives/tuples.md)
