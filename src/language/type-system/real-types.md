# Real types

## Dark v1 problems



*
* Worker  `event` variables do not have types, and so they can receive types of any shape
* HTTPClient calls automatically convert JSON into objects of the right shape

Description

## Dark v1 Problems

### Datastores use a "schema"

**Problem:** Datastores use this totally custom thing called a "schema". It should obviously be a type instead.

**Solution:** Figure out how to migrate from schemas to types

**Status: TODO**

### HTTP handlers create types dynamically

**Problem:** HTTP's `request` variable are magically converted into JSON. The HTTP middleware does not have real types.

**Solution:**

* add a way of instantly creating a type from a trace
* allow adding types to the middleware so that they can be validated
  * return 400 if they're not the right shape, possibly with a nice error message

**Status: Spec'ed or not spec'ed**

### Title

**Problem:**

**Solution:**

**Status: Spec'ed or not spec'ed**

### Title

**Problem:**

**Solution:**

**Status: Spec'ed or not spec'ed**

##

## v2 Spec

### v2 Language definition

```fsharp
```

### v2 Standard library

```fsharp
```

### v2 Editor changes

###
