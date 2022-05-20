# Enums

Description: TODO

## Dark v1 Problems

### Built-in enums are not real types

**Problem:**

The existing built-in enum types (`Result` and `Option`) are partially hardcoded.
Expressions allow `EConstructor`, but `Dval`s use `DResult` and `DOption`, while
`DType` uses `DResult` and `DOption`.

**Solution:**
- Allow Enum types in the standard library
- Allow versioning and namespacing for constructors
- Reimplement DResult and DOption using the builtin enum type
  - migrate stored programs, stored values in the User DB, stored values in traces

**Status: TODO**

### Users cannot create their own enum types

**Problem:**
Once we have enums created in the standard library, we still need to allow users to create them.

**Solution:**

* UI work (piggyback off record work)
* versioning (piggyback off record work)
* namespaces (piggyback off record work)
* storage somewhere (piggyback off record work)

**Status: TODO**


### Cannot pipe to constructors

**Problem:** you can't pipe to a constructor

* account for constructors with multiple

**Status: Not designed**


## v2 Spec

### v2 Language definition

```fsharp

type StdlibTypeName =
  { module_ : string
    typeName : string
    version : int }

type PackageTypeName =
  { owner : string
    package : string
    module_ : string
    typeName : string
    version : int }

type UserTypeName = {
  typeName : string
  version : int
}

type TypeName =
  | StdlibTypeName of StdlibTypeName
  | PackageTypeName of StdlibTypeName
  | UserTypeName of UserTypeName

type Parameter =
  { name : string
    typ : DType
    description : string }

module Enum =
  type Variant = {
    constructorName : string
    parameters : Parameter list
    description : string
  }

  type T = {
    name : TypeName
    variants : List<Variant>
    description : string
  }

module Record =
  type T = {
    name : TypeName
    description : string
    fields : List<Parameter>
  }

type CompoundType =
  | RecordType of Record.T
  | EnumType of Enum.T

// existing type
type executionState = {
  ... // existing fields
  userTypes = Map<UserTypeName, CompoundType>
  builtinTypes = Map<StdlibTypeName, CompoundType>
  packageTypes = Map<PackageTypeName, CompoundType>
}

// existing type
type DType =
  ... // existing variants
  | CompoundType of CompoundType

// existing type
type Dval =
  ... // existing variants
  | DRecord of { typeName: typeName; fields : (string * Dval) list}
  | DEnum of { typeName: typeName; enumName of string; args of Dval list }
```

### v2 Standard library

```fsharp
let optionType : CompoundType =
  EnumType {
    name = StdlibTypeName { module_ = "Result", typeName = "Result", version = 0 }
    variants =
  }
```

### v2 Editor changes

###
