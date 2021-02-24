# Anidamiento y etiquetas

Es posible "romper" o "continuar" los bucles externos cuando se trata de bucles
anidados. En estos casos, los bucles deben anotarse con alguna etiqueta y la
etiqueta debe pasarse a la declaración `break`/`continue`.

```rust,editable
#![allow(unreachable_code)]

fn main() {
    'externo: loop {
        println!("Entró en el bucle externo");

        'interno: loop {
            println!("Entró en el bucle interno");

            // Esto rompería solo el bucle interno
            //break;

            // Esto rompe el bucle externo
            break 'externo;
        }

        println!("Este punto nunca se alcanzará");
    }

    println!("Salió del bucle exterior");
}
```
