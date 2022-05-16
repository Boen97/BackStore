# Static Import

> By following `import` with the keyword `static`, an `import` statement can be used to import static members of a class or interface.

> when using static import, it is possible to refer to static members directly by their names
> without having to qualify them with the name of their class.

`import static java.lang.Math.pow;`

- `import static pkg.type-name.*;`

> the reason that Java organizes its libraries into packages is to avoid namespace collisions.
> When you import static members, you are bringing those members into the current namespace.
> Thus, you are increasing the potential for namespace conflicts and inadvertent name hiding.
