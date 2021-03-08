# Vectores y segmentos

Un vector es una colección de objetos del mismo tipo `T`, almacenados en una
memoria contigua. Los vectores se crean usando corchetes `[]`, y su longitud,
que se conoce en tiempo de compilación, es parte de su signatura de tipo
`[T; longitud]`.

Los segmentos son similares a las matrices, pero su longitud no se conoce en el
momento de la compilación. En cambio, un segmento es un objeto de dos palabras,
la primera palabra es un puntero a los datos y la segunda palabra es la
longitud del segmento. El tamaño de la palabra es el mismo de usize,
determinado por la arquitectura del procesador, por ejemplo, 64 bits en un
x86-64. Los segmentos se pueden usar para tomar prestada una sección de un
vector y tienen la signatura de tipo `&[T]`.

```rust,editable,ignore,mdbook-runnable
use std::mem;

// Esta función toma prestado un segmento
fn analiza_segmento(segmento: &[i32]) {
    println!("primer elemento del segmento: {}", segmento[0]);
    println!("el segmento tiene {} elementos", segmento.len());
}

fn main() {
    // Vector de tamaño fijo (la signatura del tipo es superflua)
    let xs: [i32; 5] = [1, 2, 3, 4, 5];

    // Todos los elementos se pueden inicializar con el mismo valor
    let ys: [i32; 500] = [0; 500];

    // La indexación comienza en 0
    println!("primer elemento del vector: {}", xs[0]);
    println!("segundo elemento del vector: {}", xs[1]);

    // `len` devuelve el recuento de elementos en el vector 
    println!("número de elementos en el vector: {}", xs.len());

    // Los vectores se asignan en la pila
    println!("vector ocupa {} bytes", mem::size_of_val(&xs));

    // Los vectores se pueden tomar prestadas automáticamente como segmentos 
    println!("pidienedo prestado todo el vector como un segmento");
    analiza_segmento(&xs);

    // Los segmentos pueden apuntar a una sección de un vector
    // Tienen el formato [índice_inicial..índice_final]
    // índice_inicial es la primera posición en el segmento
    // índice_final es uno más que la última posición en el segmento
    println!("pidienedo prestada una sección del vector como un segmento");
    analiza_segmento(&ys[1 .. 4]);

    // La indexación fuera del límite provoca un error de compilación
    println!("{}", xs[5]);
}
```
