# Impresión formateada

La impresión es manejada por una serie de <!--[`macros`][macros]--> macros
definidos en [`std::fmt`][fmt] algunos de los cuales incluyen:

* `format!`: escribe texto formateado en `String` <!--[`String`][string] -->
* `print!`: es igual que `format!` pero el texto se imprime en la consola
  (io::stdout).
* `println!`: es igual que `print!` pero se añade una nueva línea.
* `eprint!`: es igual que `format!` pero el texto se imprime en error estándar
  (io::stderr).
* `eprintln!`: es igual que `eprint!` pero se añade una nueva línea.

Todos analizan el texto de la misma manera. Además, Rust comprueba que el
formato sea correcto en el momento de la compilación.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // En general, el `{}` se reemplazará automáticamente con cualquier
    // argumento. Estos serán convertidos en cadenas de texto.

    println!("{} días", 31);

    // Sin sufijo, 31 se convierte en i32. Puedes cambiar el tipo 31
    // proporcionando un sufijo. El número 31i64, por ejemplo, tiene el tipo
    // i64.

    // Hay varios patrones opcionales con los que funciona. Se pueden utilizar
    // argumentos posicionales.
    println!("{0}, este es {1}. {1}, esta es {0}", "Alice", "Bob");

    // También se pueden usar argumentos con nombre
    println!("{sujeto} {verbo} {objeto}",
             objeto="el perro flojo",
             subject="el veloz zorro marrón",
             verb="salta por encima");

    // Se puede especificar un formato especial después de un `:`.
    println!("{} de {:b} la gente sabe binario, la otra mitad no", 1, 2);

    // Puedes alinear a la derecha el texto con un ancho especificado. Esto
    // generará "     1". 5 espacios y un "1".
    println!("{número:>ancho$}", número=1, ancho=6);

    // Puedes rellenar números con ceros adicionales. Esto generará "000001".
    println!("{número:>0ancho$}", número=1, ancho=6);

    // Rust incluso verifica para asegurarse de que el número correcto de
    // argumentos sea usado.
    println!("Mi nombre es {0}, {1} {0}", "Bond");
    // FIXME ^ Agrega el argumento que falta: "James"

    // Crea una estructura llamada "Estructura" que contenga un "i32".
    #[allow(dead_code)]
    struct Estructura(i32);

    // Sin embargo, los tipos personalizados como esta estructura requieren un
    // manejo más complicado. Esto no funcionará.
    println!("Esta estructura` {} `no se imprimirá ...", Estructura(3));
    // FIXME ^ Comenta esta línea.
}
```

[`std::fmt`][fmt] contiene muchos [`rasgos`][traits] que gobiernan la
visualización del texto. El formateo base de dos importantes se enumeran a
continuación:

* `fmt::Debug`: Utiliza el marcador `{:?}`. Formatea el texto con fines de
  depuración.
* `fmt::Display`: Utiliza el marcador `{}`. Formatea el texto de una manera más
  elegante y fácil de usar.

Aquí, usamos `fmt::Display` porque la biblioteca estándar proporciona
implementaciones para estos tipos. Para imprimir texto para tipos
personalizados, se requieren más pasos.

Implementar del rasgo `fmt::Display` implementa automáticamente el rasgo
[`ToString`] que nos permite convertir <!-- [convert] --> el tipo a `String`.
<!-- [`String`][string]. -->

### Actividades

* Soluciona los dos problemas en el código anterior (consulta los FIXME) para
  que se ejecute sin errores.
* Agrega un macro `println!` que imprima: `Pi es aproximadamente 3.142`
  controlando el número de lugares decimales mostrados. Para los propósitos de
  este ejercicio, usa `let pi = 3.141592` como una estimación de pi. (Sugerencia:
  es posible que debas consultar la documentación [`std::fmt`][fmt] para
  configurar el número de decimales que se mostrarán)

### Ve también:
 
[`std::fmt`][fmt]<!--, [`macros`][macros], [`struct`][structs] --> y
[`traits`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
