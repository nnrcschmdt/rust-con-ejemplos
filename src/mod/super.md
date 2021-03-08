# `super` y `self`

Las palabras clave `super` y `self` se pueden utilizar en la ruta para eliminar
la ambigüedad al acceder a los elementos y evitar la codificación innecesaria
de las rutas.

```rust,editable
fn funcion() {
    println!("`funcion()` llamada");
}

mod genial {
    pub fn funcion() {
        println!("`genial::funcion()` llamada");
    }
}

mod mi {
    fn funcion() {
        println!("`mi::funcion()` llamada");
    }
    
    mod genial {
        pub fn funcion() {
            println!("`mi::genial::funcion()` llamada");
        }
    }
    
    pub fn llamada_indirecta() {
        // ¡Accedamos a todas las funciones llamadas `función` desde este alcance!
        print!("`mi::llamada_indirecta()` llamada,\n> ");
        
        // La palabra clave `self` se refiere al alcance del módulo actual, en este
        // caso, `mi`. Llamar a `self::funcion()` y llamar a `funcion()` directamente
        // dan el mismo resultado, porque se refieren a la misma función.
        self::funcion();
        funcion();
        
        // También podemos usar `self` para acceder a otro módulo dentro de `mi`:
        self::genial::funcion();
        
        // La palabra clave `super` se refiere al ámbito principal (fuera del módulo
        // `mi`).
        super::funcion();
        
        // Esto enlazará a la `genial::funcion` en el alcance *crate*. En este caso, el
        // alcance del crate es el alcance más externo.
        {
            use crate::genial::funcion as funcion_raiz;
            funcion_raiz();
        }
    }
}

fn main() {
    mi::llamada_indirecta();
}
```
