# Type System

## Dark v1 problems

Dark v1 didn't have great types. Though technically there existed some types under the hood, we didn't really expose them to users and they were only useful for checking the arguments and return values of functions.

### Lack of enums

### Input Validation

### DB schemas

**Problem:** Datastores used a custom schema. This meant that we couldn't use the same types to validate input

However, the lack of types caused problems:

* DBs use a custom schema
* no way to validate handlers, which types would be useful for
* no enums to represent complex data
* records and dictionaries are sorta the same, which is horrible
* dictionaries are just dynamic typing
* autocomplete didn't work when a trace is missing (no way to know field names)
  * we should be able to write code in the absence of traces
