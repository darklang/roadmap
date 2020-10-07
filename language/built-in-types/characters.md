# Character

Characters should be an Extended Grapheme Cluster, corresponding to a single display character.

## Dark v1 problems

**Problem:** Characters were implemented, but you couldn't create one. 

**Solution:** implement characters



**Problem**: Characters were implemented but there were no functions on characters \(they were on strings instead\)

Solution: Add functions the use characters



## v2 spec

### v2 Language definition

```text
type egcChar = // type suitable to hold an EGC

type Expr = 
  | EChar { val = egcChar }
  | ...

type Pattern =
  | PChar { val : egcChar }
  | ...
  
type Dval = 
  | DChar { val = egcChar }
  | ...

type DType = 
  | TChar
  | ...
```

### v2 Standard library: dark/stdlib/Char

```text
// New
Character::toString(Char: c) -> String
String::map(String: s, (Char -> Char)) -> String
String::toList(String: s) -> List Char
String::fromList(l : List Char) -> String


```

### v2 Editor changes

* allow entering characters
  * `'` creates a partial showing `''`
  * entering a character turns the partial into an ECharacter \(eg `'a'`\)
  * entering another character turns it into a Partial with both characters \(eg `'ab'`\)
  * converting it back into a properly formed character turns it into one
  * typing `'` when when your cursor is on the closing quote skips over it
* TODO escaping



