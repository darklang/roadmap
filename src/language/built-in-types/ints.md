# Int

Ints are infinite precision integer values.

## Dark v1 Problems

### Infinite precision

**Problem:** Dark v1 integers are 63-bit integers, they should be infinite precision.

**Solution:** make them infinite precision instead using a BigNum library

**Status: Spec'ed**

### JSON and integer size

**Problem:** when we automatically coerce integers to/from JSON, many JSON implementations do not support integers larger than 53 bits (for example, the Twitter API has "id" and "id_str" fields because sometimes the "id" is bigger than 53 bits)

**Solution**:

* Integer conversion into JSON should use a string if appropriate.
* Integer conversion from JSON should always be typed, and so if there's an int it can be parsed from a stringified integer literal if appropriate

**Status: Not spec'ed**

### Negative numbers

**Problem:** The fluid editor does not allow negative numbers.

**Solution:** a UX for negative numbers is described below, it was quite straightforward.

**Status: Spec'ed**

### Arithmetic errors

**Problem:** some arithmetic operations can lead to errors:

* division by 0
* modulus by 0

**Solution:** these should return `Result (Int, IntError)`. One problem here is how we can make the  error rail less cumbersome so that this isn't really irritating to handle.

**Status: spec'ed**

### Integers of other sizes

**Problem:** it can be useful to have integers of specific sizes, in order to better model specific values or enforce overflow

**Solution:** we should add `int8`, `int16`, `int32`, `int64`, `uint8`, `uint16`, `uint32`, `uint64`

**Status: not spec'ed**

## v2 Spec

### v2 Language definition

```fsharp
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

### v2 Standard library: Int

```fsharp
type Error =
  | DivideByZero

// the same as V1
Int::absoluteValue(Int: a) -> Int
Int::add(Int: a, Int: b) -> Int
Int::clamp(Int: value, Int: limitA, Int: limitB) -> Int
Int::greaterThan(Int: a, Int: b) -> Bool
Int::greaterThanOrEqualTo(Int: a, Int: b) -> Bool
Int::lessThan(Int: a, Int: b) -> Bool
Int::lessThanOrEqualTo(Int: a, Int: b) -> Bool
Int::max(Int: a, Int: b) -> Int
Int::min(Int: a, Int: b) -> Int
Int::multiply(Int: a, Int: b) -> Int
Int::negate(Int: a) -> Int
Int::power(Int: base, Int: exponent) -> Int
Int::random_v1(Int: start, Int: end) -> Int
Int::remainder(Int: value, Int: divisor) -> Result
Int::sqrt(Int: a) -> Float
Int::subtract(Int: a, Int: b) -> Int
Int::toFloat(Int: a) -> Float

// different from v1
Int::divide(Int: a, Int: b) -> Result (Int, Error)
Int::mod(Int: a, Int: b) -> Result (Int, Error)
Int::sum(List Int: a) -> Int

```

### v2 Editor changes

* support negative integers
  * allow entering `-` at the start of an integer to convert it to a negative number
  * allow deleting `-` from the start of an integer to convert it back to a positive
  * if typing `-` in a position that is not a binop, start a partial (already happens). Once a partial of `-`gets a number added, turn it into an integer
* remove the conversion when a number gets too big - no longer needed for infinite precision ints

### Json serialization changes

**TODO:** wait til we figure out how JSON serialization works in Dark v2
