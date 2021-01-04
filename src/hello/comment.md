# Comentarios

Cualquier programa requiere comentarios y Rust admite algunas variedades
diferentes:

* *Comentarios regulares* que son ignorados por el compilador:
   * `// Comentarios de línea que van hasta el final de la línea.`
   * `/* Comentarios en bloque que van hasta el delimitador de cierre. */`

* *Comentarios de documentación* que se analizan en la documentación <!-- [documentación][docs] -->
  HTML de la biblioteca:
   * `/// Genera documentación de biblioteca para el siguiente elemento.`
   * `//! Genera documentación de biblioteca para el elemento adjunto.`

```rust,editable
fn main() {
    // Este es un ejemplo de un comentario de línea
    // Hay dos barras al principio de la línea
    // Y nada escrito dentro de estas será leído por el compilador

    // println!("¡Hola, mundo!");

    // Ejecútalo. ¿Ves? Ahora intenta eliminar las dos barras y ejecútelo nuevamente.

    /* 
     * Este es otro tipo de comentario, un comentario de bloque. En general,
     * los comentarios de línea son el estilo de comentario recomendado. Pero
     * comentarios de bloque son extremadamente útiles para deshabilitar
     * temporalmente trozos de código. /* Los comentarios de bloque se pueden 
     * /* anidar, */*/ por lo que solo se necesitan algunas pulsaciones para
     * comentar todo en esta función main(). /*/*/* ¡Inténtalo tú mismo! */*/*/
     */

    /*
    Nota: La columna anterior de `*` fue enteramente por estilo. No hay
    necesidad real de ello.
    */

    // Puedes manipular expresiones más fácilmente con comentarios de bloque
    // que con comentarios de línea. Intenta eliminar los delimitadores de
    // comentarios para cambiar el resultado:
    let x = 5 + /* 90 + */ 5;
    println!("`x` es 10 o 100? x = {}", x);
}
```

<!--
### Ve también:

[Documentación de la biblioteca][docs]
-->

[docs]: ../meta/doc.md
