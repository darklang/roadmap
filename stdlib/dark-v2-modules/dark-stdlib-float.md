# dark/stdlib/Float

Floats are 64-bit IEEE-754 arithmetic, with what I hope are improvements. Dark's floats were designed to not support infinity or overflow. Those are sentinel values which can sneak into logic, 

In Dark v1, it was possible to accidentally create Inf and NaN, but it was not really possible to use them. To avoid running into them:

* you cannot create Inf or NaN
* any functions which \(internally\) create invalid floats will return Results

TODO: what about negative 0.0?

```text
type Error =
  | Infinity
  | NaN
  
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


// different from v1
Float::add(Float: a, Float: b) -> Result (Float, Error)
Float::divide(Float a, Float b) -> Result (Float, Error)
Float::power(Float base, Float exponent) -> Result (Float, Error)
Float::multiply(Float: a, Float: b) -> Result (Float, Error)
Float::sum(List Float: a) -> Float

```

