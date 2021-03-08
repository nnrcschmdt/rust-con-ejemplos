# Visibilidad de estructuras

Las estructuras tienen un nivel extra de visibilidad con sus campos. La
visibilidad predeterminada es privada y se puede anular con el modificador
`pub`. Esta visibilidad solo importa cuando se accede a una estructura desde
fuera del módulo donde está definida y tiene el objetivo de ocultar información
(encapsulamiento).

```rust,editable
mod mi {
    // Una estructura pública con un campo público de tipo genérico `T`
    pub struct CajaAbierta<T> {
        pub contenidos: T,
    }

    // Una estructura pública con un campo privado de tipo genérico `T`
    #[allow(dead_code)]
    pub struct CajaCerrada<T> {
        contenidos: T,
    }

    impl<T> CajaCerrada<T> {
        // Un método constructor público
        pub fn new(contenidos: T) -> CajaCerrada<T> {
            CajaCerrada {
                contenidos: contenidos,
            }
        }
    }
}

fn main() {
    // Las estructuras públicas con campos públicos se pueden construir como de
    // costumbre
    let caja_abierta = mi::CajaAbierta { contenidos: "información pública" };

    // y se puede acceder a sus campos de manera normal.
    println!("La caja abierta contiene: {}", caja_abierta.contenidos);

    // Las estructuras públicas con campos privados no se pueden construir utilizando
    // nombres de campo. ¡Error! CajaCerrada tiene campos privados
    //let caja_cerrada = mi::CajaCerrada { contenidos: "información clasificada" };
    // TODO ^ Intenta descomentar esta línea

    // Sin embargo, las estructuras con campos privados se pueden crear utilizando
    // constructores públicos.
    let _caja_cerrada = mi::CajaCerrada::new("información clasificada");

    // y no se puede acceder a los campos privados de una estructura pública.
    // ¡Error! El campo `contenidos` es privado
    //println!("La caja cerrada contiene: {}", _caja_cerrada.contenidos);
    // TODO ^ Intenta descomentar esta línea
}
```

### Ve también:

<!--[genéricos][generics] y -->
[métodos][methods]

[generics]: ../generics.md
[methods]: ../fn/methods.md
