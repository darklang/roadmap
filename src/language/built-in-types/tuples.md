# Tuple

Dark v1 does not have tuples. Dark v1 allowed different types in the same list, though, which was not a great experience as the rest of the language mostly expected the language to be typed.

## Goals

Tuples are useful for situations where you want to group information together but do:

* do not want a full blown record
* want heterogeneous types
* want destructuring

## V2 definition

```
type Expr = 
  | ETuple { exprs : List Expr }
  | ...

type Pattern =
  | PTuple { pats : List Pattern }
  | ...
  
type Dval = 
  | DTuple { vals = List Dval }
  | ...

type DType = 
  | TTuple { contents = List DTyple }
  | ...
```

### Interaction model

```
let (myString, myInt) = ("str", 6)
```

#### Creation:

```
'let ' =>
  let |___ = ___
( =>
  let (|) = ___
myString =>
  let (myString|) = ___
, =>
  let (myString, |___) = ___
'myInt) = ' => 
  let (myString, myInt) = |___
( =>
  let (myString, myInt) = (|)
'"str", ' =>
  let (myString, myInt) = ("str", |___)
5) =>
  let (myString, myInt) = ("str", 5)|
```

### Standard library

```
// Access
Tuple2::first ('a,'b) -> 'a
Tuple2::second ('a,'b) -> 'b

// Creation
Tuple2::pair ('a, 'b) -> ('a,'b)

// Manipulation
Tuple2::mapFirst (('a,'b), ('a -> 'c)) -> ('c, 'b) 
Tuple2::mapSecond (('a,'b), ('b -> 'c)) -> ('b, 'c) 
Tuple2::mapBoth (('a,'b), ('a -> 'c), ('b -> 'd)) -> ('c, 'd) 

Tuple2::swap (('a,'b)) -> ('b, 'a) 


// And all the equivalents for Tuple3
// Also possibly bonus functions from https://package.elm-lang.org/packages/TSFoster/elm-tuple-extra/latest/Tuple3

```

Changes in existing libraries:

```
List.zip_v1(List 'a, List 'b) -> Option (List ('a, 'b))
List.zipShortest_v1(List 'a, List 'b) -> List ('a, 'b)
List.unzip_v1(List ('a, 'b) -> (List 'a, List 'b)

Dict.fromList_v1(List ('a, 'b)) -> Option (Dict 'a 'b)
Dict.fromListOverwritingDuplicates_v1(List ('a, 'b)) -> Dict 'a 'b
Dict.toList_v1(Dict 'a 'b) -> List ('a, 'b)
```

There should be some version of a HttpClient function that takes tuples, as it is legal to have multiple headers of the same type and so tuples rather than dicts represent the **correct** type. Since we expect users to use built-ins for headers (such as `Http::jsonContentType`), this seems doable soon.

