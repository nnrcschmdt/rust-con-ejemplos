# `From` e `Into`

Los rasgos [`From`] y [`Into`] están intrínsecamente vinculados, y esto es en
realidad parte de su implementación. Si puedes convertir el tipo A del tipo B,
entonces debería ser fácil creer que deberíamos poder convertir el tipo B en el
tipo A.

## `From`

El rasgo [`From`] permite que un tipo defina cómo crearse a sí mismo a partir
de otro tipo, por lo que proporciona un mecanismo muy simple para convertir
entre varios tipos. Existen numerosas implementaciones de este rasgo dentro de
la biblioteca estándar para la conversión de tipos elementales y comunes.

Por ejemplo, podemos convertir fácilmente un `str` en un `String`

```rust
let mi_str = "hola";
let mi_string = String::from(mi_str);
```

Podemos hacer algo similar para definir una conversión para nuestro propio tipo.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Numero {
    valor: i32,
}

impl From<i32> for Numero {
    fn from(item: i32) -> Self {
        Numero { valor: item }
    }
}

fn main() {
    let num = Numero::from(30);
    println!("Mi número es {:?}", num);
}
```

## `Into`

El rasgo [`Into`] es simplemente el recíproco del rasgo `From`. Es decir, si
has implementado el rasgo `From` para tu tipo, `Into` lo llamará cuando sea
necesario.

El uso del rasgo `Into` normalmente requerirá la especificación del tipo a
convertir, ya que el compilador no puede determinarlo la mayor parte del
tiempo.  Sin embargo, esta es una pequeña compensación considerando que
obtenemos la funcionalidad de forma gratuita.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Numero {
    valor: i32,
}

impl From<i32> for Numero {
    fn from(item: i32) -> Self {
        Numero { valor: item }
    }
}

fn main() {
    let entero = 5;
    // Intenta eliminar la declaración de tipo
    let numero: Numero = entero.into();
    println!("Mi numero es {:?}", numero);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
