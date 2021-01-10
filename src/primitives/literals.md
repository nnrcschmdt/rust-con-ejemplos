# Literales y operadores

Los números enteros `1`, los de coma flotante `1.2`, los caracteres `'a'`, las
cadenas `"abc"`, los valores booleanos `true` y el tipo de unidad `()` se
pueden expresar utilizando literales.

Los números enteros pueden, alternativamente, expresarse usando notación
hexadecimal, octal o binaria usando estos prefijos respectivamente: `0x`,`0o` o
`0b`.

Los guiones bajos se pueden insertar en literales numéricos para mejorar la
legibilidad, por ejemplo `1_000` es lo mismo que `1000` y `0.000_001` es lo
mismo que `0.000001`.

Necesitamos decirle al compilador el tipo de literales que usamos. Por ahora,
usaremos el sufijo `u32` para indicar que el literal es un entero de 32 bits
sin signo, y el sufijo `i32` para indicar que es un entero de 32 bits con
signo.

Los operadores disponibles y su precedencia [en Rust][rust op-prec] son
similares a otros [lenguajes tipo C][op-prec].

```rust,editable
fn main() {
    // Adición de números enteros
    println!("1 + 2 = {}", 1u32 + 2);

    // Substracción de números enteros
    println!("1 - 2 = {}", 1i32 - 2);
    // TODO ^ Cambia `1i32` por `1u32`  para ver por qué el tipo es importante

    // Lógica booleana
    println!("true AND false es {}", true && false);
    println!("true OR false es {}", true || false);
    println!("NO true is {}", !true);

    // Operaciones bit a bit
    println!("0011 AND 0101 is {:04b}", 0b0011u32 & 0b0101);
    println!("0011 OR 0101 is {:04b}", 0b0011u32 | 0b0101);
    println!("0011 XOR 0101 is {:04b}", 0b0011u32 ^ 0b0101);
    println!("1 << 5 es {}", 1u32 << 5);
    println!("0x80 >> 2 es 0x{:x}", 0x80u32 >> 2);

    // ¡Utiliza guiones bajos para mejorar la legibilidad!
    println!("Un millón se escribe así {}", 1_000_000u32);
}
```

[rust op-prec]: https://doc.rust-lang.org/reference/expressions.html#expression-precedence
[op-prec]: https://en.wikipedia.org/wiki/Operator_precedence#Programming_languages
