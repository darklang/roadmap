# Float

Floats are 64-bit IEEE-754 arithmetic, with what I hope are improvements. Dark's floats were designed to not support infinity or overflow. Those are sentinel values which can sneak into logic, and continue to propagate. Instead, we want to use results to handle these errors.

## Dark v1 problems

### Operators

**Problem:** Dark's operators (`+`, `-`, `*`, etc) work on integers. In Dark v1, we use `Float::+` instead, which doesn't suck but isn't great

**Non-solution: **We speculated that we could use the editor to simply hide the `Float::` part. However, that doesn't allow polymorphism, you can't have a library that takes numbers of any kind and (for example) sums them.

**Solution: **use traits to support reuse of common operators for different types

**Status**: Not spec'ed

### Float entry problems that convert to 0

TODO

**Status: **Problem not understood

### Inf and NaN

**Problem:** In Dark v1, it's possible to accidentally create `Inf` and `NaN`, but it was not really possible to use them.

**Solution: **prevent creating Inf or NaN. Any functions which (internally) create invalid floats will return Results instead.

**Status**: Spec'ed, not implemented

### Negative 0.0

**Problem:** it's possible to have negative 0.0. This is a confusing part of floats.

**Solution: **TODO

**Status: **problem not understood, solution unknown

### Support other representations

**Problem:** v1 only supports decimalized floats, like `5.6`. It should also support exponent style like `6.02e23`

**Solution: **Also support exponent format

**Status: **Representation is spec'ed. Interaction model not spec'ed.

### **Floats don't support negatives**

**Problem:** same as ints

**Solution: **copy the proposed interaction model from ints

**Status: **not spec'ed

## v2 spec

### v2 language definition

Same as V1, except we represent a float better.

```
type Sign =
  | Plus
  | Minus

type floatRep = {
      wholeNumberPart : Int64,
      fractionalPart : Int64
      exponentExists : Bool
      exponentSign : Sign
      exponentPower : Int64
    }

type Expr =
  | EFloat of floatRep
  | ...

type Pattern =
  | PFloat of floatRep
  | ...

type Dval =
  | DFloat of double
  | ...

type DType =
  | TFloat
  | ...
```

#### Examples

* `5.`
* `.6`
* `0.6`
* `-678.234`
* `-6.436E-567`

### Float stdlib functions

```
type Error =
  | FloatOverflowError

// same as v1
Float::absoluteValue(Float: a) -> Float
Float::ceiling(Float: a) -> Int
Float::clamp(Float: value, Float: limitA, Float: limitB) -> Float
Float::floor(Float: a) -> Int
Float::greaterThan(Float: a, Float: b) -> Bool
Float::greaterThanOrEqualTo(Float: a, Float: b) -> Bool
Float::lessThan(Float: a, Float: b) -> Bool
Float::lessThanOrEqualTo(Float: a, Float: b) -> Bool
Float::max(Float: a, Float: b) -> Float
Float::min(Float: a, Float: b) -> Float
Float::negate(Float: a) -> Float
Float::round(Float: a) -> Int
Float::roundDown(Float: a) -> Int
Float::roundTowardsZero(Float: a) -> Int
Float::roundUp(Float: a) -> Int
Float::sqrt(Float: a) -> Float
Float::subtract(Float: a, Float: b) -> Float
Float::truncate(Float: a) -> Int
Float::sum(List Float: a) -> Float

// different from v1
Float::add(Float: a, Float: b) -> Result (Float, Error)
Float::subtract(Float: a, Float: b) -> Result (Float, Error)
Float::divide(Float a, Float b) -> Result (Float, Error)
Float::power(Float base, Float exponent) -> Result (Float, Error)
Float::multiply(Float: a, Float: b) -> Result (Float, Error)


```
