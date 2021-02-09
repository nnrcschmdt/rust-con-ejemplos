# `TryFrom` y `TryInto`

Similar a [`From` e `Into`][from-into], [`TryFrom`] y [`TryInto`] son rasgos
genéricos para convertir entre tipos. A diferencia de `From`/`Into`, los rasgos
`TryFrom`/`TryInto` se utilizan para conversiones falibles y, como tales,
devuelven [`Result`]s.

[from-into]: from_into.html
[`TryFrom`]: https://doc.rust-lang.org/std/convert/trait.TryFrom.html
[`TryInto`]: https://doc.rust-lang.org/std/convert/trait.TryInto.html
[`Result`]: https://doc.rust-lang.org/std/result/enum.Result.html

```rust,editable
use std::convert::TryFrom;
use std::convert::TryInto;

#[derive(Debug, PartialEq)]
struct NumeroPar(i32);

impl TryFrom<i32> for NumeroPar {
    type Error = ();

    fn try_from(value: i32) -> Result<Self, Self::Error> {
        if value % 2 == 0 {
            Ok(NumeroPar(value))
        } else {
            Err(())
        }
    }
}

fn main() {
    // TryFrom

    assert_eq!(NumeroPar::try_from(8), Ok(NumeroPar(8)));
    assert_eq!(NumeroPar::try_from(5), Err(()));

    // TryInto

    let result: Result<NumeroPar, ()> = 8i32.try_into();
    assert_eq!(result, Ok(NumeroPar(8)));
    let result: Result<NumeroPar, ()> = 5i32.try_into();
    assert_eq!(result, Err(()));
}
```
