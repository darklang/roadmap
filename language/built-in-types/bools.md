# Bool

Booleans are `true` or `false`

## Dark v1 Problems

None

## v2 Spec

### v2 Language definition

```text
type Expr = 
  | EBool { val = bool }
  | ...

type Pattern =
  | PBool { val : bool }
  | ...
  
type Dval = 
  | DBool { val = bool }
  | ...

type DType = 
  | TBool
  | ...
```

### v2 Standard library

```text
// same as V1
Bool::and(Bool, Bool) -> Bool
Bool::not(Bool) -> Bool
Bool::or(Bool, Bool) -> Bool
Bool::xor(Bool, Bool) -> Bool

// removed
// no nulls anymore (also, shouldn't have been in the bool namespace)
Bool::isNull(Any check) -> Bool
Bool::isError(Any check) -> Bool


```

### v2 Editor changes

None





\`\`

