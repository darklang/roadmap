# Strings

## Problems in v1

### Concatenation

Users currently have to do concatenation like so:

```text
"I am "
|> ++ user.name
|> ++ " and I am "
|> ++ (toString user.age)
|> ++ " years old"
```

Instead, we'd like to support string interpolation

```text
"I am ${user.name} and I am ${user.age} years old"
```

### Special characters

To enter a newline, carriage return, tab, or other special character, you have to paste them directly. You can't type any of them. Related to this, the display of these tokens in the editor is broken.

### Emoji

I think the editor does not support proper unicode - I'm not sure.

### String length

String length is determined in `O(n)` time. Using a better string implementation would help solve this.

### Characters

Characters are not implemented. Characters should be an Extended Grapheme Cluster, corresponding to a single display character.

### Shortened display

We wrap strings at 40 characters. We should do a better job of wrapping that takes into account the entire length of the line, and make 40 configurable.

## Solutions

```
type string = // unicode supporting type
```

```text
type stringSegment = 
  | Text of string 
  | InterpolatedExpr of expr

type Expr = 
  | EString of stringSegment list
  | ...

type Pattern = 
  | PString of string list
  | ...

type Dval =
  | DString of string
  | ...
  
type DType = 
  | TString
  | ...
```

Escaped characters can be stored as their actual values in the string, and displayed/entered differently in the editor.



