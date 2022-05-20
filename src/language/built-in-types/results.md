# Result

Description

## Dark v1 Problems

### Results are not polymorphic

**Problem:** The result type is `TResult`, and doesn't have parameters for its contents

**Solution:** Replace `TResult` with `TResult(successType, errorType)`

**Status: Not spec'ed**

### Results are **a special type**

**Problem:** Results should be a regular type in the standard library, not one built into the implementation

**Solution:**

* remove `DResult`
  * replace with `DEnum(name : ConstructorName, args : Dval list`)

* remove `TResult` from types
  * add type definitions to standard library
  * replace with instance of enum type

**Status: Not spec'ed**

## v2 Spec

### v2 Language definition

```fsharp

type Dval =
  DEnum(ConstructorName, args : List<Dval>)
  ...
```

### v2 Standard library

```fsharp
let builtinTypes =
  [

  ]
```

### v2 Editor changes

