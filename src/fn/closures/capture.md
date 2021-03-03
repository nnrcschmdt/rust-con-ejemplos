# Capturar

Las clausuras son inherentemente flexibles y harán lo que la funcionalidad
requiera para que la clausura funcione sin anotaciones. Esto permite que la
captura se adapte de manera flexible al caso de uso, a veces moviéndose y a
veces tomando prestado. Las clausuras pueden capturar variables:

* por referencia: `&T`
* por referencia mutable: `&mut T`
* por valor: `T`

Preferiblemente capturan variables por referencia y solo descienden cuando es
necesario.

```rust,editable
fn main() {
    use std::mem;
    
    let color = String::from("verde");

    // Una clausura para imprimir `color` que inmediatamente toma prestado (`&`)
    // a `color` y almacena el préstamo y la clausura en la variable `print`.
    // Permanecerá prestado hasta que se use `print` por última vez.
    //
    // `println!` solo requiere argumentos por referencia inmutable por lo que
    // no impone algo más restrictivo
    let print = || println!("`color`: {}", color);

    // Llama a la clausura usando el préstamo.
    print();

    // `color` se puede tomar prestado inmutablemente de nuevo, porque la
    // clausura solo mantiene una referencia inmutable a `color`.
    let _prestado_nuevamente = &color;
    print();

    // Se permite un movimiento o cambio después del uso final de `print`
    let _color_movido = color;


    let mut contador = 0;
    // Una clausura para incrementar `contador` podría tomar `&mut contador` o
    // `contador` pero `&mut contador` es menos restrictivo por lo que toma eso.
    // Inmediatamente toma prestado `contador`.
    //
    // Se requiere un `mut` en `inc` porque un `&mut` está almacenado dentro.
    // Por lo tanto, llamar a la clausura muta el cierre que requiere un `mut`.
    let mut inc = || {
        contador += 1;
        println!("`contador`: {}", contador);
    };

    // Llama a la clausura usando un préstamo mutable.
    inc();

    // La clausura todavía toma prestado `contador` de forma mutante porque se
    // llama más tarde.
    // Un intento de tomar prestado nuevamente dará lugar a un error.
    // let _prestado_nuevamente = &contador;
    // ^ TODO: intenta descomentar esta línea.
    inc();

    // La clausura ya no necesita pedir prestado `&mut contador`. Por lo tanto,
    // es posible pedir prestado nuevamente sin error
    let _contador_prestado_nuevamente = &mut contador; 

    
    // Un tipo sin copia.
    let movible = Box::new(3);

    // `mem::drop` requiere `T` por lo que debe tomarse por valor. Un tipo de
    // copia copiaría en la clausura dejando el original intacto.
    // Una no copia debe moverse y, por lo tanto, `movible` se mueve
    // inmediatamente a la clausura.
    let consume = || {
        println!("`movible`: {:?}", movible);
        mem::drop(movible);
    };

    // `consume` consume la variable, por lo que solo se puede llamar una vez.
    consume();
    // consume();
    // ^ TODO: Intenta descomentar esta línea.
}
```

El uso de `move` antes de las barras verticales obliga a la clausura a tomar
posesión de las variables capturadas:

```rust,editable
fn main() {
    // `Vec` tiene semántica sin copia.
    let pajar = vec![1, 2, 3];

    let contiene = move |aguja| pajar.contains(aguja);

    println!("{}", contiene(&1));
    println!("{}", contiene(&4));

    // println!("Hay {} elementos en vec", pajar.len());
    // ^ Descomentar la línea anterior resultará en un error en tiempo de
    // compilación porque el verificador de préstamo no permite reutilizar la
    // variable después de que ella ha sido movida.
    
    // Eliminar `move` de la firma de la clausura provocará que la clausura
    // tome prestada la variable _pajar_ inmutablemente, por lo tanto, _pajar_
    // sigue estando disponible y descomentar la línea anterior no provocará un
    // error.
}
```

### Ve también:

<!-- [`Box`][box] y -->
[`std::mem::drop`][drop]

[box]: ../../std/box.md
[drop]: https://doc.rust-lang.org/std/mem/fn.drop.html
