# Visibilidad

De forma predeterminada, los elementos de un módulo tienen visibilidad privada,
pero esto se puede anular con el modificador `pub`. Solo se puede acceder a los
elementos públicos de un módulo desde fuera del alcance del módulo.

```rust,editable
// Un módulo llamado `mi_mod`
mod mi_mod {
    // Los elementos de los módulos tienen visibilidad privada de forma predeterminada.
    fn funcion_privada() {
        println!("`mi_mod::funcion_privada()` llamada");
    }

    // Utiliza el modificador `pub` para anular la visibilidad predeterminada.
    pub fn funcion() {
        println!("`mi_mod::funcion()` llamada");
    }

    // Los elementos pueden acceder a otros elementos en el mismo módulo, incluso cuando
    // son privados.
    pub fn acceso_inderecto() {
        print!("`mi_mod::acceso_inderecto()` llamada,\n> ");
        funcion_privada();
    }

    // Los módulos también se pueden anidar
    pub mod anidado {
        pub fn funcion() {
            println!("`mi_mod::anidado::funcion()` llamada");
        }

        #[allow(dead_code)]
        fn funcion_privada() {
            println!("`mi_mod::anidado::funcion_privada()` llamada");
        }

        // Las funciones declaradas usando la sintaxis `pub (in ruta)` solo son visibles
        // dentro de la ruta dada. `ruta` debe ser un módulo principal o antepasado
        pub(in crate::mi_mod) fn funcion_publica_en_mi_mod() {
            print!("`mi_mod::anidado::funcion_publica_en_mi_mod() llamada`,\n> ");
            funcion_publica_en_anidado();
        }

        // Las funciones declaradas usando la sintaxis `pub(self)` solo son visibles
        // dentro del módulo actual, que es lo mismo que dejarlas privadas
        pub(self) fn funcion_publica_en_anidado() {
            println!("`mi_mod::anidado::funcion_publica_en_anidado()` llamada");
        }

        // Las funciones declaradas usando la sintaxis `pub(super)` solo son visibles
        // dentro del módulo padre
        pub(super) fn funcion_publica_en_super_mod() {
            println!("`mi_mod::anidado::funcion_publica_en_super_mod()` llamada");
        }
    }

    pub fn llama_funcion_publica_en_mi_mod() {
        print!("`mi_mod::llama_funcion_publica_en_mi_mod()` llamada,\n> ");
        anidado::funcion_publica_en_mi_mod();
        print!("> ");
        anidado::funcion_publica_en_super_mod();
    }

    // pub(crate) hace que las funciones sean visibles solo dentro del crate actual
    pub(crate) fn funcion_publica_en_crate() {
        println!("`mi_mod::funcion_publica_en_crate()` llamada");
    }

    // Los módulos anidados siguen las mismas reglas de visibilidad
    mod anidado_privado {
        #[allow(dead_code)]
        pub fn funcion() {
            println!("`mi_mod::anidado_privado::funcion()` llamada");
        }

        // Los elementos principales privados seguirán restringiendo la visibilidad de
        // un elemento secundario, incluso si se declara como visible dentro de un
        // ámbito más amplio. 
        #[allow(dead_code)]
        pub(crate) fn funcion_restringida() {
            println!("`mi_mod::anidado_privado::funcion_restringida()` llamada");
        }
    }
}

fn funcion() {
    println!("`funcion()` llamada");
}

fn main() {
    // Los módulos permiten la desambiguación entre elementos que tienen el mismo nombre.
    funcion();
    mi_mod::funcion();

    // Se puede acceder a los elementos públicos, incluidos los que se encuentran dentro
    // de los módulos anidados, desde fuera del módulo principal. 
    mi_mod::acceso_inderecto();
    mi_mod::anidado::funcion();
    mi_mod::llama_funcion_publica_en_mi_mod();

    // Los elementos pub(crate) se pueden llamar desde cualquier lugar del mismo crate
    mi_mod::funcion_publica_en_crate();

    // Los elementos pub(in ruta) solo se pueden llamar desde el módulo especificado
    // ¡Error! la función `funcion_publica_en_mi_mod` es privada
    //mi_mod::anidado::funcion_publica_en_mi_mod();
    // TODO ^ Intenta descomentar esta línea

    // Private items of a module cannot be directly accessed, even if
    // anidado in a public module:

    // ¡Error! la función `funcion_privada` es privada
    //mi_mod::funcion_privada();
    // TODO ^ Intenta descomentar esta línea

    // ¡Error! la función `funcion_privada` es privada
    //mi_mod::anidado::funcion_privada();
    // TODO ^ Intenta descomentar esta línea

    // ¡Error! el módulo `anidado_privado` es un módulo privado
    //mi_mod::anidado_privado::funcion();
    // TODO ^ Intenta descomentar esta línea

    // ¡Error! el módulo `anidado_privado` es un módulo privado
    //mi_mod::anidado_privado::funcion_restringida;
    // TODO ^ Intenta descomentar esta línea
}
```
