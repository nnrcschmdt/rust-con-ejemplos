# Jerarquía de archivos

Los módulos se pueden asignar a una jerarquía de archivos/directorios.
Analicemos el [ejemplo de visibilidad][visibility] en archivos:

```shell
$ tree .
.
|-- mi
|   |-- inaccesible.rs
|   |-- mod.rs
|   `-- anidado.rs
`-- partido.rs
```

En `partido.rs`:

```rust,ignore
// Esta declaración buscará un archivo llamado `mi.rs` o `mi/mod.rs` e insertará su
// contenido dentro de un módulo llamado `mi` bajo este alcance
mod mi;

fn function() {
    println!("`function()` llamada");
}

fn main() {
    mi::function();

    function();

    mi::acceso_indirecto();

    mi::anidado::function();
}

```

En `mi/mod.rs`:

```rust,ignore
// De manera similar, `mod inaccesible` y `mod anidado` ubicarán los archivos
// `anidado.rs` e `inaccesible.rs` y los insertarán aquí debajo de sus respectivos
// módulos
mod inaccesible;
pub mod anidado;

pub fn function() {
    println!("`mi::function()` llamada");
}

fn funcion_privada() {
    println!("`mi::funcion_privada()` llamada");
}

pub fn acceso_indirecto() {
    print!("`mi::acceso_indirecto()` llamada,\n> ");

    funcion_privada();
}
```

En `mi/anidado.rs`:

```rust,ignore
pub fn function() {
    println!("`mi::anidado::function()` llamada");
}

#[allow(dead_code)]
fn funcion_privada() {
    println!("`mi::anidado::funcion_privada()` llamada");
}
```

En `mi/inaccesible.rs`:

```rust,ignore
#[allow(dead_code)]
pub fn funcion_publica() {
    println!("`mi::inaccesible::funcion_publica()` llamada");
}
```

Comprobemos que las cosas sigan funcionando como antes:

```shell
$ rustc partido.rs && ./partido
`mi::function()` llamada
`function()` llamada
`mi::acceso_indirecto()` llamada,
> `mi::funcion_privada()` llamada
`mi::anidado::function()` llamada
```

[visibility]: visibility.md
