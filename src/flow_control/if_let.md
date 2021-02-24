# if let

Para algunos casos de uso, al hacer coincidir enumeraciones, `match` es
incómodo. Por ejemplo:

```rust
// Haz `opcional` de tipo `Option<i32>`
let opcional = Some(7);

match opcional {
    Some(i) => {
        println!("Esta es una cadena muy larga y `{:?}`", i);
        // ^ Necesitamos 2 sangrías solo para poder desestructurar
        // `i` de la opción.
    },
    _ => {},
    // ^ Obligatorio porque `match` es exhaustivo. No parece
    // como espacio desperdiciado?
};

```

`if let` es más limpio para este caso de uso y además permite especificar
varias opciones de falla:

```rust,editable
fn main() {
    // Todos tienen el tipo `Option<i32>`
    let numero = Some(7);
    let letra: Option<i32> = None;
    let emoticon: Option<i32> = None;

    // La construcción `if let` dice: if `let` desestructura `numero` en
    // `Some(i)`, evalúa el bloque (`{}`).
    // The `if let` construct reads: "if `let` destructures `number` into
    if let Some(i) = numero {
        println!("Coincidencia {:?}!", i);
    }

    // Si necesitas especificar una falla, usa un else:
    if let Some(i) = letra {
        println!("Coincidencia {:?}!", i);
    } else {
        // La desestructuración falló. Cambia al caso de falla.
        println!("No coincide con un número. ¡Vamos con una letra!");
    }

    // Proporciona una condición de falla alterada.
    let me_gustan_las_letras = false;

    if let Some(i) = emoticon {
        println!("Coincidencia {:?}!", i);
    // Falló la desestructuración. Evalúa una condición `else if` para ver si
    // se debe tomar una rama de falla alternativa:
    } else if me_gustan_las_letras {
        println!("No coincide con un número. ¡Vamos con una letra!");
    } else {
        // La condición evaluada como falsa. Esta rama es la predeterminada:
        println!("No me gustan las letras. ¡Vamos con un emoticón :)!");
    }
}
```

De la misma manera, `if let` puede usarse para coincidir con cualquier valor de
enumeración:

```rust,editable
// Our example enum
enum Foo {
    Bar,
    Baz,
    Qux(u32)
}

fn main() {
    // Crea variables ejemplo
    let a = Foo::Bar;
    let b = Foo::Baz;
    let c = Foo::Qux(100);
    
    // La variable a coincide con Foo::Bar
    if let Foo::Bar = a {
        println!("a es foobar");
    }
    
    // La variable b no coincide con Foo::Bar
    // Entonces esto no imprimirá nada
    if let Foo::Bar = b {
        println!("b es foobar");
    }
    
    // La variable c coincide con Foo::Qux que tiene un valor
    // Similar a Some() en el ejemplo anterior
    if let Foo::Qux(valor) = c {
        println!("c es {}", valor);
    }

    // El enlace también funciona con `if let`
    if let Foo::Qux(valor @ 100) = c {
        println!("c es cien");
    }
}
```

Otro beneficio es que `if let` nos permite hacer coincidir variantes de
enumeración no parametrizadas. Esto es cierto incluso en los casos en que la
enumeración no implementa o deriva `PartialEq`. En tales casos, `if Foo::Bar ==
a` fallaría en la compilación, porque las instancias de la enumeración no se
pueden equiparar, sin embargo, `if let` continuará funcionando.

¿Quieres un desafío? Corrige el siguiente ejemplo para usar `if let`:

```rust,editable,ignore,mdbook-runnable
// This enum purposely neither implements nor derives PartialEq.
// That is why comparing Foo::Bar == a fails below.
enum Foo {Bar}

fn main() {
    let a = Foo::Bar;

    // La variable a coincide con Foo::Bar
    if Foo::Bar == a {
    // ^-- esto provoca un error en tiempo de compilación. Utiliza `if let` en su lugar.
        println!("a es foobar");
    }
}
```

### Ve también:

[`enum`][enum] <!--, [`Option`][option], --> y el [RFC][if_let_rfc]

[enum]: ../custom_types/enum.md
[if_let_rfc]: https://github.com/rust-lang/rfcs/pull/160
[option]: ../std/option.md
