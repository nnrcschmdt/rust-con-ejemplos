# Funciones divergentes

Las funciones divergentes nunca retornan. Están marcados con `!`, que es un
tipo vacío.

```rust
fn foo() -> ! {
    panic!("Esta llamada nunca retorna.");
}
```

A diferencia de todos los demás tipos, este no se puede instanciar, porque el
conjunto de todos los valores posibles que puede tener este tipo está vacío.
Ten en cuenta que es diferente del tipo `()`, que tiene exactamente un valor
posible.

Por ejemplo, esta función retorna como de costumbre, aunque no hay información
en el valor de retorno.

```rust
fn alguna_fn() {
    ()
}

fn main() {
    let a: () = alguna_fn();
    println!("Esta función retorna y puedes ver esta línea.")
}
```

A diferencia de esta función, que nunca devolverá el control a la persona que
llama.

```rust,ignore
#![feature(never_type)]

fn main() {
    let x: ! = panic!("Esta llamada nunca retorna.");
    println!("¡Nunca verás esta línea!");
}
```

Aunque esto pueda parecer un concepto abstracto, de hecho es muy útil y a
menudo útil. La principal ventaja de este tipo es que se puede convertir a
cualquier otro y, por lo tanto, se puede usar en lugares donde se requiere un
tipo exacto, por ejemplo, en las ramas `match`. Esto nos permite escribir
código como este:

```rust
fn main() {
    fn suma_numeros_impares(up_to: u32) -> u32 {
        let mut acc = 0;
        for i in 0..up_to {
            // Observa que el tipo de retorno de esta expresión coincidente debe
            // ser u32 debido al tipo de variable "suma".
            let adicion: u32 = match i%2 == 1 {
                // La variable "i" es de tipo u32, lo que está perfectamente bien.
                true => i,
                // Por otro lado, la expresión "continue" no retorna u32, pero
                // aún está bien, porque nunca retorna y por lo tanto no
                // infringe los requisitos de tipo de la expresión coincidente.
                false => continue,
            };
            acc += adicion;
        }
        acc
    }
    println!("Suma de números impares hasta 9 (excluyente): {}", suma_numeros_impares(9));
}
```

También es el tipo de retorno de funciones que se repiten para siempre (por
ejemplo, `loop {}`) como servidores de red o funciones que terminan el proceso
(por ejemplo, `exit()`).
