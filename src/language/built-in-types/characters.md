# Character

Characters should be an Extended Grapheme Cluster, corresponding to a single display character.

Chars are “Extended Grapheme Clusters”. (A codepoint is some bytes that implement unicode characters, a grapheme is some codepoints forming a unicode entity, such as an emoji; an EGC is some graphemes, used to handle things like emojis which combine to form a single emoji).

## Dark v1 problems

### Can't create characters

**Problem:** Characters were implemented, but you couldn't create one.

**Solution:** implement characters creation

### No character stdlib

**Problem**: Characters were implemented but there were no functions on characters (they were on strings instead)

**Solution**: Add functions the use characters



## v2 spec

### v2 Language definition

```fsharp
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

```fsharp
// New
Character::toString(Char: c) -> String
String::map(String: s, (Char -> Char)) -> String
String::toList(String: s) -> List Char
String::fromList(l : List Char) -> String


```

### v2 Editor changes

* allow entering characters
  * `'` creates a partial showing `''`
  * entering a character turns the partial into an ECharacter (eg `'a'`)
  * entering another character turns it into a Partial with both characters (eg `'ab'`)
  * converting it back into a properly formed character turns it into one
  * typing `'` when when your cursor is on the closing quote skips over it
* escaping should be supported
  * common expected escapes: \n, \r, \t
  * escapes that are needed for the text to work \\\\, \\'
  * allow a specific byte: \xhh (hex escaping)
  * could possibly allow octal escaping too
  * escape sequences should be clear to the user (a different color)
  * escape sequence should have a clear doc explaining how it works and what the user is looking at
  * the expr should be a partial while the `\` is not followed by a valid character
