# Let

## Dark v1

Dark v1 had this defintiion of `let`:

This had a number of problems:

* no support for destructuring
* users expected Dark to be a list of statements followed by an expr, but they got a single expr with unexpected semantics
  * esp in the editor, this led to some oddness

## V2 definition

```text
type Expr = 
  | Let { lhs : pattern, rhs : expr, body : expr }
  | ...

// No pattern, dval, or dtype
```

