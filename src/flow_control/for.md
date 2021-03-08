# bucles for

## for y range

La construcción `for in` se puede utilizar para iterar a través de un
`Iterator`. Una de las formas más sencillas de crear un iterador es utilizar la
notación de rango `a..b`. Esto produce valores de `a` (inclusive) a `b`
(exclusivo) en pasos de uno.

Escribamos FizzBuzz usando `for` en lugar de `while`.

```rust,editable
fn main() {
    // `n` tomará los valores: 1, 2, ..., 100 en cada iteración
    for n in 1..101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

Alternativamente, `a..=b` puede usarse para un rango que sea inclusivo en ambos
extremos. Lo anterior se puede escribir como:

```rust,editable
fn main() {
    // `n` tomará los valores: 1, 2, ..., 100 en cada iteración
    for n in 1..=100 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

## for e iteradores

La construcción `for in` puede interactuar con un `Iterator` de varias formas.
Como se discutió en la sección sobre el rasgo <!--[Iterator][iter],-->
`Iterator`, de forma predeterminada el bucle `for` aplicará la función
`into_iter` a la colección. Sin embargo, este no es el único medio de convertir
colecciones en iteradores.

`into_iter`, `iter` e `iter_mut` manejan la conversión de una colección en un
iterador de diferentes maneras, proporcionando diferentes vistas de los datos
que contiene.

* `iter`: toma prestado cada elemento de la colección durante de cada
  iteración. Dejando así la colección intacta y disponible para su
  reutilización después del bucle.

```rust, editable
fn main() {
    let nombres = vec!["Bob", "Frank", "Ferris"];

    for nombre in nombres.iter() {
        match nombre {
            &"Ferris" => println!("¡Hay un rustáceo entre nosotros!"),
            // TODO ^ Intenta eliminar el & y hacer coincidir solo "Ferris"
            _ => println!("Hola {}", nombre),
        }
    }
    
    println!("nombres: {:?}", nombres);
}
```

* `into_iter` - Esto consume la colección de modo que en cada iteración se
  proporcionan los datos exactos. Una vez que la colección se ha consumido, ya
  no está disponible para su reutilización, ya que se ha "movido" dentro del
  bucle.

```rust, editable, ignore
fn main() {
    let nombres = vec!["Bob", "Frank", "Ferris"];

    for nombre in nombres.into_iter() {
        match nombre {
            "Ferris" => println!("¡Hay un rustáceo entre nosotros!");
            _ => println!("Hola {}", nombre),
        }
    }
    
    println!("nombres: {:?}", nombres);
    // FIXME ^ Commenta estas línea
}
```

* `iter_mut` - Esto toma prestado de manera mutable cada elemento de la
  colección, lo que permite que la colección se modifique en su lugar.

```rust, editable
fn main() {
    let mut nombres = vec!["Bob", "Frank", "Ferris"];

    for nombre in nombres.iter_mut() {
        *nombre = match nombre {
            &mut "Ferris" => "¡Hay un rustáceo entre nosotros!",
            _ => "Hola",
        }
    }

    println!("nombres: {:?}", nombres);
}
```

En los fragmentos anteriores, observa el tipo de rama `match`, que es la
diferencia clave en los tipos de iteración. La diferencia de tipo, por
supuesto, implica acciones diferentes que se pueden realizar.

<!--
### See also:

[Iterator][iter]
-->

[iter]: ../trait/iter.md
