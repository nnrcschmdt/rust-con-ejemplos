# Ámbito y sombreado

Los enlaces de variables tienen un ámbito y están limitados a vivir en un
*bloque*. Un bloque es una colección de declaraciones encerradas entre corchetes
`{}`.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Este enlace vive en la función principal
    let enlace_de_vida_larga = 1;

    // Este es un bloque y tiene un ámbito más pequeño que la función principal
    {
        // Este enlace solo existe en este bloque
        let enlace_de_vida_corta = 2;

        println!("Bloque interior, vida corta: {}", enlace_de_vida_corta);
    }
    // Fin del bloque

    // ¡Error! `enlace_de_vida_corta` no existe en este ámbito
    println!("Exterior del bloque, vida corta: {}", enlace_de_vida_corta);
    // FIXME ^ Comenta esta línea

    println!("Exterior del bloque, vida larga: {}", enlace_de_vida_larga);
}
```

Además, se permite [sombreado de variables][variable-shadow].

```rust,editable,ignore,mdbook-runnable
fn main() {
    let enlace_sombreado = 1;

    {
        println!("antes de ser sombreado: {}", enlace_sombreado);

        // Este enlace *sombrea* al exterior
        let enlace_sombreado = "abc";

        println!("sombreado en bloque interior: {}", enlace_sombreado);
    }
    println!("fuera del bloque interior: {}", enlace_sombreado);

    // Este enlace *sombrea* al anterior
    let enlace_sombreado = 2;
    println!("sombreado en el bloque exterior: {}", enlace_sombreado);
}
```

[variable-shadow]: https://en.wikipedia.org/wiki/Variable_shadowing
