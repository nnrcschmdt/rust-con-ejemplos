# Funciones de orden superior

Rust proporciona funciones de orden superior (HOF). Estas son funciones que
toman una o más funciones y/o producen una función más útil. Funciones de orden
superior y los iteradores perezosos le dan a Rust su sabor funcional.

```rust,editable
fn es_impar(n: u32) -> bool {
    n % 2 == 1
}

fn main() {
    println!("Encuentra la suma de los números impares al cuadrado por debajo de 1000");
    let superior = 1000;

    // Enfoque imperativo
    // Declarar variable acumuladora
    let mut acc = 0;
    // Iterar: 0, 1, 2, ... hasta el infinito
    for n in 0.. {
        // Cuadrar el número
        let n_cuadrado = n * n;

        if n_cuadrado >= superior {
            // Romper el bucle si se supera el límite superior
            break;
        } else if es_impar(n_cuadrado) {
            // Acumular valor, si es impar
            acc += n_cuadrado;
        }
    }
    println!("estilo imperativo: {}", acc);

    // Enfoque funcional
    let suma_de_numeros_impares_al_cuadrado: u32 =
        (0..).map(|n| n * n)                         // Todos los números naturales al cuadrado
             .take_while(|&n_cuadrado| n_cuadrado < superior) // Por debajo del límite superior
             .filter(|&n_cuadrado| es_impar(n_cuadrado))      // Que son impares
             .fold(0, |acc, n_cuadrado| acc + n_cuadrado);    // Sumados
    println!("functional style: {}", suma_de_numeros_impares_al_cuadrado);
}
```

[Option][option]
e 
[Iterator][iter]
implementan su parte justa de funciones de orden superior

[option]: https://doc.rust-lang.org/core/option/enum.Option.html
[iter]: https://doc.rust-lang.org/core/iter/trait.Iterator.html
