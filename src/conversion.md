# Conversión

Los tipos elementales se pueden convertir entre sí mediante [conversión
explícita].

Rust aborda la conversión entre tipos personalizados (es decir, `struct` y
`enum`) mediante el uso de <!--[rasgos]--> rasgos. Las conversiones genéricas
usarán los rasgos [`From`] y [`Into`]. Sin embargo, hay otros más específicos
para los casos más comunes, en particular cuando se convierte desde y hacia
`String`s.

[conversión explícita]: types/cast.md
[rasgos]: trait.md
[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html
