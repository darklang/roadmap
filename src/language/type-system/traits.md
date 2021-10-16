# Traits

Traits are one way to provide generics or ad-hoc polymorphism.

## Dark v1 Problems

Many of the things that relied on "magic" in v1 could be solved with Traits. Thoughts:

* Trait for how to pretty-print for users
* Trait for hooking a value into a visualization system in the editor
* Trait for the SQL query compiler?
* Trait for addition, subtraction, etc
  * maybe there's a set of known binops and they have traits defined for each of them
* fromJSON, toJSON
* Should implementations be implicitly derived, or explicitly derived and editable?

Open questions:

* support we have a type A, and users are using type A. Can we add trait B to type A? Probably not, that would change its behaviour. So we'd have to make type A1, with that trait.
* This could cause type explosion, so we'll need to automatically generate ways to convert types to/from different versions that are structurally the same

## v2 Spec

### v2 Language definition

```fsharp
```

### v2 Standard library

```fsharp
```

### v2 Editor changes

###
