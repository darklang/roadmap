# Dictionary

Dicts are maps from a certain key type to a certain value type. The key must currently be a string. The value can be any type but all elements of the Dict are the same type \(not currently enforced\).

Dicts are different than records: dicts can have arbitrary keys.

## Dark v1 Problems

### Dictionaries are the same as records

**Problem:** Right now, both are entangled and we need to separate them

**Solutions:**

* Add a syntax for updating records so that we don't have to use Dict::set
* Add a new dictionary type, that is not compatible with DObj
  * It would need new functions that are type compatible
  * It would allow keys of any single type
  * The values would homogenous
  * dot syntax would not be supported \(use `Dict::get` instead\)
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

\*\*\*\*

## v2 Spec

### v2 Language definition

```text

```

### v2 Standard library

```text
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

