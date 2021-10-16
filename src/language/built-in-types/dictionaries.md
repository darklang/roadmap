# Dictionary

Dicts are maps from a certain key type to a certain value type. The key must currently be a string. The value can be any type but all elements of the Dict are the same type (not currently enforced).

Dicts are different than records: dicts can have arbitrary keys.

## Dark v1 Problems

### Dictionaries are the same as records

**Problem:** Right now, both dictionaries and records are represented by a `DObj` and a `TObj`. We need to separate them.

**Subproblem**: the only way to update a "record" is with `Dict::set`.

**Solution**: add a syntax for updating records. In existing functional languages, they use `{ existingValue with fieldName1 = newValue1; fieldName2 = newValue2 }`

**Status: not speced**

**Subproblem: **The "syntax" to create dicts and records is overloaded. Both use `{ field : value }` (as both are the same thing right now. If we split them, we need a way to disambiguate which one you're creating.

**Solution option 1: **Add a new syntax for records. For example, we might do:

`Person {.`

The big advantage here is that the autocomplete would create a bunch of new fields to fill in the object, like so:

```
Person {
  name : ___ // "string" placeholder text)
  age : ___ // "int" placeholder text
}
```

**Solution option 2: **Add a new syntax for dictionaries. For example, we might do:

```
let myDict = dict{
    ___ : ___ // would be useful to have a prompt to tell you to use quotes here
}
```

This would have a number of other benefits

**Subproblem:** What do we do with existing records and objects? Do they become records or objects or a third legacy `DObj`?

****

**Solutions:**

*
* Add a new dictionary type, that is not compatible with DObj
  * It would need new functions that are type compatible
  * It would allow keys of any single type
  * The values would homogenous
  * dot syntax would not be supported (use `Dict::get` instead)
  * record syntax would not be supported
    * could support dot
* Remove hack where we allow hyphens in record names
  * Since people use maps for headers, switch headers to string pairs
* Add a type checker which distinguishes between Dicts and Record
* DObj would become just a record
  * old `Dict::` functions would be for records, and would be deprecated. They could even be renamed to `Record::` for now, until we add syntax for the new stuff. We could automatically transition them to the new stuff
  * dot access could instead be
* **Status: TODO**

### Dictionaries are **string only**

**Problem:** Right now, you can't have a dictionary of other things

**Solutions:**

* Add a syntax for updating records so that we don't have to use Dict::set
* Add a type checker which distinguishes between Dicts and Record
  * I wonder if we could use the same syntax for both?
* Stop using the DObj for both
  * will likely need a new version of the language for this

**Status: TODO**

### It's possible to have heterogenous dictionaries

**Problem:** If you have a dict of ints, you can add a string to it

**Solution:** This might be solved by having a type checker tell you what you're doing wrong. Or perhaps we actually track the type of a dict and raise an error if the wrong type is inserted

**Status**: **TODO**

## v2 Spec

### v2 Language definition

```
```

### v2 Standard library

```
Dict::filterMap(Dict 'k 'v, ('v -> Option 'b)) -> Dict 'k 'b
Dict::filter_v1(Dict 'k 'v, ('v -> bool)) -> Dict 'k 'v
Dict::isEmpty(Dict dict) -> Bool
Dict::keys(Dict dict) -> List
Dict::map(Dict dict, Block f) -> Dict
Dict::member(Dict dict, Str key) -> Bool
Dict::merge(Dict left, Dict right) -> Dict
Dict::remove(Dict dict, Str key) -> Dict
Dict::set(Dict dict, Str key, Any val) -> Dict
Dict::singleton(Str key, Any value) -> Dict
Dict::size(Dict dict) -> Int
Dict::toJSON(Dict dict) -> Str
Dict::toList(Dict dict) -> List
Dict::values(Dict dict) -> List

// Remove string-only
Dict::get_v2(Dict Str 'v, Str) -> Option 'v
Dict::get_v2(Dict Str 'v, Str) -> Option 'v


// TODO use tuples
Dict::fromList(List entries) -> Option
Dict::fromListOverwritingDuplicates(List entries) -> Dict

```

### v2 Editor changes

###
