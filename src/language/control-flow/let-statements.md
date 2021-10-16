# Let

## Dark v1

Dark v1 had this defintiion of `let`:

```
type Expr = 
  | Let { lhs : string, rhs : expr, body : expr }
  | ...

// No pattern, dval, or dtype
```

This had a number of problems:

* no support for destructuring
* users expected Dark to be a list of statements followed by an expr, but they got a single expr with unexpected semantics
  * esp due to refactoring tools, which didn't necessarily handle this well.

#### **Problem**

Users expect Dark to be a list of statements followed by an expr. The actual semantics (a single expr, which allows nested expressions) confuses users. One particular manifestation is that the refactoring tooling does not have expected behaviour.

#### **Solution**

* much more testing for refactoring functions, especially in the presence of nesting
* TODO: more needed here



## V2 definition

```
type Expr = 
  | Let { lhs : pattern, rhs : expr, body : expr }
  | ...

// No pattern, dval, or dtype
```
