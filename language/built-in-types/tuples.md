# Tuple

Dark v1 does not have tuples. Dark v1 allowed different types in the same list, though, which was not a great experience as the rest of the language mostly expected the language to be typed.

## Goals

Tuples are useful for situations where you want to group information together but do:

* do not want a full blown record
* want heterogeneous types
* want destructuring

## V2 definition

```text
type Expr = 
  | ETuple { exprs : List Expr }
  | ...

type Pattern =
  | PTuple { pats : List Pattern }
  | ...
  
type Dval = 
  | DTuple { vals = List Dval }
  | ...

type DType = 
  | TTuple { contents = List DTyple }
  | ...
```

### Interaction model

```text
let (myString, myInt) = ("str", 6)
```

#### Creation:

```text
'let ' =>
  let |___ = ___
( =>
  let (|) = ___
myString =>
  let (myString|) = ___
, =>
  let (myString, |___) = ___
'myInt) = ' => 
  let (myString, myInt) = |___
( =>
  let (myString, myInt) = (|)
'"str", ' =>
  let (myString, myInt) = ("str", |___)
5) =>
  let (myString, myInt) = ("str", 5)|
```

### Open questions:

* is the empty value `()` an empty tuple or it's own thing?

