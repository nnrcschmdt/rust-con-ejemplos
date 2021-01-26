# Enlace de variables

Rust proporciona seguridad de tipo mediante escritura estática. Los enlaces de
variables se pueden anotar cuando se declaran. Sin embargo, en la mayoría de
los casos, el compilador podrá inferir el tipo de variable del contexto,
reduciendo considerablemente la carga de anotaciones.

Los valores (como los literales) se pueden vincular a variables, utilizando el
vínculo `let`.

```rust,editable
fn main() {
    let un_entero = 1u32;
    let un_booleano = true;
    let unidad = ();

    // copiar `un_entero` en `entero_copiado`
    let entero_copiado = un_entero;

    println!("Un número entero: {:?}", entero_copiado);
    println!("Un booleano: {:?}", un_booleano);
    println!("Conoce el valor unitario: {:?}", unidad);

    // El compilador advierte sobre los enlaces de variables no utilizados;
    // estas advertencias pueden ser silenciado prefijando el nombre de la
    // variable con un guión bajo
    let _variable_sin_usar = 3u32;

    let variable_ruidosa_sin_usar = 2u32;
    // FIXME ^ Prefija con un guión bajo para suprimir la advertencia
}
```
