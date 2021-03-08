# La declaración `use`

La declaración `use` se puede utilizar para enlazar una ruta completa a un
nuevo nombre, para facilitar el acceso. A menudo se usa así:

```rust,editable,ignore
use crate::profundamente::anidado::{
    mi_primera_funcion,
    mi_segunda_funcion,
    YUnTipoRasgo
};

fn main() {
    mi_primera_funcion();
}
```

Puedes utilizar la palabra clave `as` para enlazar importaciones a un nombre
diferente:

```rust,editable
// Enlaza la ruta `profundamente::anidado::funcion` a `otra_funcion`.
use profundamente::anidado::funcion as otra_funcion;

fn funcion() {
    println!("`funcion()` llamada");
}

mod profundamente {
    pub mod anidado {
        pub fn funcion() {
            println!("`profundamente::anidado::funcion()` llamada");
        }
    }
}

fn main() {
    // Acceso más fácil a `profundamente::anidado::funcion`
    otra_funcion();

    println!("Ingresando al bloque");
    {
        // Esto es equivalente a `use profundamente::anidado::funcion as funcion`
        // Esta `funcion()` sombreará la externa.
        use crate::profundamente::anidado::funcion;

        // Los enlaces `use` tienen un alcance local. En este caso, el sombreado
        // de `funcion()` está solo en este bloque.
        funcion();

        println!("Dejando el bloque");
    }

    funcion();
}
```
