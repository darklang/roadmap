# Records

## Dark v1 problems

* updating records
* confusion between records and dicts

You access records fields by:

```fsharp
myRecord.x
```

If the field doesn't exist: `DError`. But there will be a type checker to ensure the field exists

Description

## Dark v1 Problems

**Problem:** Records and dicts are the same thing.

In v1 of Dark, there are only `DObj`s, and both records and dictionaries use the same value type. This leads to significant confusion:
- It's unclear whether the `{}` syntax creates a record or a dict
- `Dict::` functions work on Records
- Record access syntax (`x.y`) works on Dictionaries


**Solution:**

A solution needs to hit the following notes:
- how do we create records and dictionaries
- what do we do with the current records and dictionaries

One possible solution that was considered was to have a type constructor, like in rust. This had the problem of what happens if you pass a record into something with another type but the same shape, when you have polymorphic traits on it (actually this problem might exist anyway).

Actual solution:
- existing things become records (`DObj becomes DRecord`)
  - existing `Dict::` values work on records, and are deprecated and replaced with syntax
- new dictionary type (`DDict`)

**Status: Spec'ed or not spec'ed**

## v2 Spec

### v2 Language definition

```fsharp
```

### v2 Standard library

```fsharp
```

### v2 Editor changes

###
