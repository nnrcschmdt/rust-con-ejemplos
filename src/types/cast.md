# Conversión explícita

Rust no proporciona conversión de tipo implícita (coerción) entre tipos
elementales. Pero, la conversión de tipo explícita (*casting*) se puede realizar
usando la palabra clave `as`.

Las reglas para convertir entre tipos integrales siguen las convenciones de C
en general, excepto en los casos en que C tiene un comportamiento indefinido.
El comportamiento de todas las conversiones explícitas entre tipos integrales
está bien definido en Rust.

```rust,editable,ignore,mdbook-runnable
// Suprime todas las advertencias de las conversiones que se desbordan.
#![allow(overflowing_literals)]

fn main() {
    let decimal = 65.4321_f32;

    // ¡Error! Sin conversión implícita
    let entero: u8 = decimal;
    // FIXME ^ Comenta esta línea

    // Conversión explícita
    let entero = decimal as u8;
    let caracter = entero as char;

    // ¡Error! Existen limitaciones en las reglas de conversión. Un número de
    // coma flotate no se puede convertir directamente en un char.
    let caracter = decimal as char;
    // FIXME ^ Comenta esta línea

    println!("Convirtiendo: {} -> {} -> {}", decimal, entero, caracter);

    // al convertir cualquier valor a un tipo sin signo, T, T::MAX + 1 se suma
    // o resta hasta que el valor encaje en el nuevo tipo

    // 1000 ya encaja en un u16
    println!("1000 como un u16 es: {}", 1000 as u16);

    // 1000 - 256 - 256 - 256 = 232
    // Por debajo, se guardan los primeros 8 bits menos significativos (LSB),
    // mientras que el resto hacia el bit más significativo (MSB) se trunca.
    println!("1000 como un u8 es : {}", 1000 as u8);
    // -1 + 256 = 255
    println!("  -1 como un u8 es : {}", (-1i8) as u8);

    // Para números positivos, esto es lo mismo que el módulo
    println!("1000 módulo 256 es : {}", 1000 % 256);

    // Al convertir a un tipo con signo, el resultado (bit a bit) es el mismo
    // que al convertir primero al tipo sin signo correspondiente. Si el bit
    // más significativo de ese valor es 1, entonces el valor es negativo.

    // A menos que ya encaje, por supuesto.
    println!(" 128 como un i16 es: {}", 128 as i16);
    // 128 as u8 -> 128, cuyo complemento de dos en ocho bits es:
    println!(" 128 como un i8 es : {}", 128 as i8);

    // repitiendo el ejemplo anterior
    // 1000 as u8 -> 232
    println!("1000 como un u8 es : {}", 1000 as u8);
    // y el complemento de dos de 232 es -24
    println!(" 232 como un i8 es : {}", 232 as i8);
    
    // Desde Rust 1.45, la palabra clave `as` realiza una *conversión saturante*
    // cuando se convierte de coma flotante a entero.
    // Si el valor de la coma flotante excede el límite superior o es menor que
    // el límite inferior, el valor devuelto será igual al límite cruzado.
    
    // 300.0 es 255
    println!("300.0 es {}", 300.0_f32 as u8);
    // -100.0 as u8 es 0
    println!("-100.0 como u8 es {}", -100.0_f32 as u8);
    // nan as u8 es 0
    println!("nan como u8 es {}", f32::NAN as u8);
    
    // Este comportamiento incurre en un pequeño costo de tiempo de ejecución y
    // se puede evitar con métodos inseguros; sin embargo, los resultados
    // pueden desbordarse y devolver **valores incorrectos**. Utiliza estos
    // métodos con prudencia:
    unsafe {
        // 300.0 es 44
        println!("300.0 es {}", 300.0_f32.to_int_unchecked::<u8>());
        // -100.0 as u8 es 156
        println!("-100.0 como u8 es {}", (-100.0_f32).to_int_unchecked::<u8>());
        // nan as u8 es 0
        println!("nan como u8 es {}", f32::NAN.to_int_unchecked::<u8>());
    }
}
```
