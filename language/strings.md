# Strings

## Dark v1 problems

### Concatenation

**Problem:** Users currently have to do concatenation like so:

```text
"I am "
|> ++ user.name
|> ++ " and I am "
|> ++ (toString user.age)
|> ++ " years old"
```

**Solution:** Instead, we'd like to support string interpolation

```text
"I am ${user.name} and I am ${user.age} years old"
```

### Special characters

**Problem:** To enter a newline, carriage return, tab, or other special character, you have to paste them directly. You can't type any of them. Related to this, the display of these tokens in the editor is broken.

**Solution:** support using escape characters \(`\`\) to support them \(`\n, \r, \t, \\, \", etc`\). Describe the complex UX for adding them, deleting, displaying, and editing them, in the spec below. 

### Emoji

**Problem:** I think the editor does not support proper unicode - I'm not sure.

**Solution:** the editor should support entering all LTR Unicode text \(RTL can wait until Dark v3\) - if you can type it into the browser, we should support it in the editor.

### String length

**Problem:** String length is determined in `O(n)` time.

**Solution:** String length should be cached as part of the string. Using a better string implementation would help solve this.

### Shortened display

**Problem:** We wrap strings at 40 characters to make lines not run on forever. This has a number of annoying problems:

* sometimes the string is only 41 character and it looks bad
* sometimes the line has more room than 40 characters and it looks dumb
* sometimes the line has builtin line breaks, but it breaks off length instead
* *  We should do a better job of wrapping that takes into account the entire length of the line, and make 40 configurable.

### Cursor affinity

**Problem:** the cursor can be in two different places which logically mean the same thing \(the end of a line, and the start of the subsequent line\). This leads to "cursor affinity" problems.

**Solution:** TODO: this was written down somewhere.

## v2 Language definition

```text
type string = // unicode supporting type

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

Strings should store their lengths.

## v2 Standard library

```text
// same as v1
String::append_v1(String: s1, String: s2) -> String
String::base64Decode(String: s) -> String
String::base64Encode(String: s) -> String
String::contains(String: lookingIn, String: searchingFor) -> Bool
String::digest(String: s) -> String
String::dropFirst(String: string, Int: characterCount) -> String
String::dropLast(String: string, Int: characterCount) -> String
String::endsWith(String: subject, String: suffix) -> Bool
String::first(String: string, Int: characterCount) -> String
String::fromChar_v1(Character: c) -> String
String::isEmpty(String: s) -> Bool
String::join(List l, String separator) -> String
String::last(String: string, Int: characterCount) -> String
String::length_v1(String: s) -> Int
String::padEnd(String: string, String: padWith, Int: goalLength) -> String
String::padStart(String: string, String: padWith, Int: goalLength) -> String
String::prepend(String: s1, String: s2) -> String
String::random_v2(Int: length) -> Result
String::replaceAll(String: s, String: searchFor, String: replaceWith) -> String
String::reverse(String: string) -> String
String::slice(String: string, Int: from, Int: to) -> String
String::slugify_v2(String string) -> String
String::split(String s, String separator) -> List
String::startsWith(String subject, String prefix) -> Bool
String::toBytes(String str) -> Bytes
String::toFloat_v1(String s) -> Result
String::toInt_v1(String s) -> Result
String::toList_v1(String s) -> List
String::toLowercase_v1(String s) -> String
String::toUUID_v1(String uuid) -> Result
String::toUppercase_v1(String s) -> String
String::trim(String str) -> String
String::trimEnd(String str) -> String
String::trimStart(String str) -> String

// Maybe could be better
String::htmlEscape(String html) -> String
String::newline() -> String



// Different in v2
String::foreach_v1(String: s, Block f) -> String
String::fromList_v1(List l) -> String


```

## v2 Editor fixes

* test whether we can enter emoji, if not fix it

### Support for string escaping

* TODO: write out how string escapes get displayed, entered, edited, and stored





