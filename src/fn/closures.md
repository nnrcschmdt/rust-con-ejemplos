# Clausuras

Las clausura son funciones que pueden capturar el entorno circundante. Por
ejemplo, una clausura que captura la variable x:

```Rust
|val| val + x
```

La sintaxis y las capacidades de las clausuras las hacen muy convenientes para
su uso sobre la marcha. Llamar a una clausura es exactamente como llamar a una
función. Sin embargo, tanto los tipos de entrada como los de retorno *pueden*
inferirse y los nombres de las variables de entrada *deben* especificarse.

Otras características de las clausuras incluyen:
* usar `||` en lugar de `()` alrededor de las variables de entrada.
* delimitación opcional de cuerpo (`{}`) para una sola expresión (obligatoria
  en caso contrario).
* la capacidad de capturar las variables del entorno exteriores.

```rust,editable
fn main() {
    // Incremento mediante clausuras y funciones.
    fn funcion(i: i32) -> i32 { i + 1 }

    // Las clausura son anónimas, aquí los vinculamos a referencias
    // La anotación es idéntica a la anotación de función pero es opcional
    // como son los `{}` envolviendo el cuerpo. Estas funciones sin nombre
    // se asignan a variables con nombres adecuados.
    let clausura_annotada = |i: i32| -> i32 { i + 1 };
    let clausura_inferida = |i     |          i + 1  ;

    let i = 1;
    // Llame a la función y las clausuras
    println!("función: {}", funcion(i));
    println!("clausura_annotada: {}", clausura_annotada(i));
    println!("clausura_inferida: {}", clausura_inferida(i));

    // Una clausura sin argumentos que devuelve un `i32`.
    // El tipo de retorno es inferido.
    let uno = || 1;
    println!("clausura que devuelve uno {}", uno());

}
```
