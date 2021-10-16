# List

Lists and Arrays use the same datatype, called Lists. The Dark compiler will in the future optimize their implementation to support good algorithmic complexity and performance for whatever you use them for.

Lists should be used for all “I want a sequence of things” situations, including iterating across them, random access, push/pop, etc.

## Dark v1 Problems

### No pattern matching on lists

**Problem:** patterns don't support lists yet

**Solution:** implement

**Status: Spec'ed or not spec'ed**

### Fake values are sometimes in lists

**Problem:** errors, errorrails and incompletes can be put in lists, if we're not careful

**Solution:** Though we have mostly been careful, it would be useful to try and fuzz functions, or add logging, or something to ensure that this doesnt happen

**Status: **Unspeced

### It's possible to have heterogenous lists

**Problem:** If you have a list of ints, you can add a string to it

**Solution:** This might be solved by having a type checker tell you what you're doing wrong. Or perhaps we actually track the type of a list and raise an error if the wrong type is inserted

**Status**: still unclear on solution

## v2 Spec

### v2 Language definition

```
type Expr =
  | EList { list : List Expr }
  | ...

type Pattern =
  | PList { val : List Pattern }
  | ...

type Dval =
  | DList { val = List Dval }
  | ...

type DType =
  | TList of DType
  | ...
```

### v2 Standard library

```
List::append(List 'a, List 'a) -> List 'a
List::drop(List 'a, Int) -> List 'a
List::dropWhile(List 'a, ('a -> bool)) -> List 'a
List::empty() -> List 'a
List::filterMap(List 'a, ('a -> Option 'b)) -> List 'b
List::filter_v2(List list, ('a -> bool)) -> List 'a
List::findFirst_v2(List 'a, ('a -> bool)) -> Option 'a
List::flatten(List (List 'a)) -> List 'a
List::fold(List 'a, 'b, ('a -> 'b -> 'b)) -> 'b
List::getAt_v1(List 'a, Int) -> Option 'a
List::head_v2(List 'a) -> Option 'a
List::indexedMap(List 'a, (Int -> 'a -> 'b)) -> List 'b
List::interleave(List 'a, List 'a) -> List 'a
List::interpose(List 'a, 'a) -> List 'a
List::isEmpty(List 'a) -> Bool
List::last_v2(List 'a) -> Option 'a
List::length(List 'a) -> Int
List::map(List 'a, ('a -> 'b)) -> List 'b
List::map2(List 'a, List 'b, ('a -> 'b -> 'c)) -> Option (List 'c)
List::map2shortest(List 'a, List 'b, ('a -> 'b -> 'c)) -> List 'c
List::member(List 'a, 'a) -> Bool
List::push(List 'a, 'a) -> List 'a
List::pushBack(List 'a, 'a) -> List 'a
List::randomElement(List 'a ) -> Option 'a
List::range(Int, Int) -> List Int
List::repeat(Int, 'a) -> List 'a
List::reverse(List 'a) -> List 'a
List::singleton('a) -> List 'a
List::sort(List 'a) -> List ;a
List::sortBy(List 'a, ('a -> 'b)) -> List 'a
List::sortByComparator(List 'a, ('a -> Int)) -> Result (List 'a) String
List::tail(List 'a) -> Option (List 'a)
List::take(List 'a, Int count) -> List 'a
List::takeWhile(List 'a, ('a -> Bool)) -> List 'a
List::uniqueBy(List list, ('a -> 'b)) -> List 'a

// To remove, see Tuples
List::unzip(List) -> List
List::zip(List, List) -> Option
List::zipShortest(List, List) -> List
```

### v2 Editor changes

* support for list patterns
* support for cons perhaps?
