# enums

Una `enum` se desestructura de manera similar:

```rust,editable
// Se requiere `allow` para silenciar las advertencias porque solo se usa una
// variante.
#[allow(dead_code)]
enum Color {
    // Estos 3 se especifican únicamente por su nombre.
    Rojo,
    Azul,
    Verde,
    // Estos vinculan las tuplas `u32` a diferentes nombres: modelos de color.
    RGB(u32, u32, u32),
    HSV(u32, u32, u32),
    HSL(u32, u32, u32),
    CMY(u32, u32, u32),
    CMYK(u32, u32, u32, u32),
}

fn main() {
    let color = Color::RGB(122, 17, 40);
    // TODO ^ Prueba diferentes variantes para `color`

    println!("¿Qué color es??");
    // Una `enum` se puede desestructurar usando una `match`
    match color {
        Color::Rojo  => println!("¡El color es Rojo!"),
        Color::Azul  => println!("¡El color es Azul!"),
        Color::Verde => println!("¡El color es Verde!"),
        Color::RGB(r, g, b) =>
            println!("rojo: {}, verde: {}, y azul: {}!", r, g, b),
        Color::HSV(h, s, v) =>
            println!("matiz: {}, saturación: {}, valor: {}!", h, s, v),
        Color::HSL(h, s, l) =>
            println!("matiz: {}, saturación: {}, luminosidad: {}!", h, s, l),
        Color::CMY(c, m, y) =>
            println!("cian: {}, magenta: {}, amarillo: {}!", c, m, y),
        Color::CMYK(c, m, y, k) =>
            println!("cian: {}, magenta: {}, amarillo: {}, clave (negro): {}!",
                c, m, y, k),
        // No necesito otro brazo porque se han examinado todas las variantes
    }
}
```

### Ve también:

<!--[`#[allow(...)]`][allow],-->
[modelo de colores][color_models] y [`enum`][enum]

[allow]: ../../../attribute/unused.md
[color_models]: https://es.wikipedia.org/wiki/Modelo_de_colores
[enum]: ../../../custom_types/enum.md
