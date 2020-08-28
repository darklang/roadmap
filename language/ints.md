# Ints

## Problems

* Dark integers should be infinite precision \(they are currently 63 bit\)
* How should ints that are larger than 53 bits \(or whatever the JSON size is\) interact with JSON.

### V2 Definition

```text
type Expr = 
  | EInt { val = BigInt }
  | ...

type Pattern =
  | PInt { val : BigInt }
  | ...
  
type Dval = 
  | DInt { val = BigInt }
  | ...

type DType = 
  | TInt
  | ...
```

