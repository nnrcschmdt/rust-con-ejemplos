# Tuplas

Una tupla es una colección de valores de diferentes tipos. Las tuplas se
construyen usando paréntesis `()`, y cada tupla en sí es un valor con signatura de
tipo `(T1, T2, ...)`, donde `T1`,`T2` son los tipos de sus miembros. Las
funciones pueden usar tuplas para devolver múltiples valores, ya que las tuplas
pueden contener cualquier número de valores.

```rust,editable
// Las tuplas se pueden utilizar como argumentos de función y como valores de retorno
fn invertir(par: (i32, bool)) -> (bool, i32) {
    // `let` se puede usar para vincular los miembros de una tupla a variables
    let (entero, booleano) = par;

    (booleano, entero)
}

// La siguiente estructura es para la actividad.
#[derive(Debug)]
struct Matriz(f32, f32, f32, f32);

fn main() {
    // Una tupla con muchos tipos diferentes.
    let tupla_larga = (1u8, 2u16, 3u32, 4u64,
                       -1i8, -2i16, -3i32, -4i64,
                       0.1f32, 0.2f64,
                       'a', true);

    // Los valores se pueden extraer de la tupla mediante la indexación de
    // tuplas
    println!("el primer valor de la tupla: {}", tupla_larga.0);
    println!("el segundo valor de la tuple: {}", tupla_larga.1);

    // Tuplas pueden ser miembros de tuplas
    let tupla_de_tuplas = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);

    // Las tuplas son imprimibles
    println!("tupla de tuplas: {:?}", tupla_de_tuplas);
    
    // Pero no se pueden imprimir tuplas largas 
    // let tupla_muy_larga = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13);
    // println!("tupla muy larga: {:?}", tupla_muy_larga);
    // TODO ^ Descomenta las 2 líneas anteriores para ver el error del
    // compilador

    let par = (1, true);
    println!("par is {:?}", par);

    println!("el par invertido es {:?}", invertir(par));

    // Para crear tuplas de un elemento, se requiere la coma para
    // diferenciarlas de un literal entre paréntesis
    println!("tupla de un elemento: {:?}", (5u32,));
    println!("solo un número entero: {:?}", (5u32));

    // las tuplas se pueden desestructurar para crear enlaces
    let tupla = (1, "hola", 4.5, true);

    let (a, b, c, d) = tupla;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);

    let matriz = Matriz(1.1, 1.2, 2.1, 2.2);
    println!("{:?}", matriz);

}
```

### Actividad

 1. *Recapitulación*: Agrega el rasgo `fmt::Display` a la estructura `struct`
    Matriz en el ejemplo anterior, de modo que si cambias de imprimir el
    formato de depuración `{:?}` al formato de visualización `{}`, verás la
    siguiente salida:

    ```text
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    ```
    
    Es posible que desees volver al ejemplo de [impresión para
    mostrar][print_display]

 2. Agrega una función `transponer` usando la función `invertir` como
    plantilla, que acepta una matriz como argumento y devuelve una matriz en la
    que se han intercambiado dos elementos. Por ejemplo:


    ```rust,ignore
    println!("Matriz:\n{}", matriz);
    println!("Transponer:\n{}", transponer(matriz));
    ```

    resulta en la salida:

    ```text
    Matriz:
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    Transponer:
    ( 1.1 2.1 )
    ( 1.2 2.2 )
    ```

[print_display]: ../hello/print/print_display.md
