# Null

As a temporary hack, Dark supports `null`. This allows us handle JSON while we build out enough type-system support to allow them to be replaced by `Option`.

Null is mostly useful for comparing against incoming JSON and results of HttpClient calls. When returning JSON or making HttpClient calls, you can use Options instead and they will be converted properly to `null` in the JSON output.

## Dark v1 Problems

### Nulls can appear in JSON

**Problem:** Nulls shouldn't really exist, but they do because

**Solution:** Add a way to have types in HTTP handlers, and when retrieving data over Http APIs.

**Status: TODO**

### Nulls can appear in the database

**Problem:** It is technically possible to add nulls to the database, though it shouldn't really be allowed.

**Solution:** We need some sort of way to migrate this to a newly typed world. A good way to start would be to determine how common null values are in the database, and to go from there.

**Status: TODO**

### **What to do with existing uses of **Null?

**Problem:** When we've identified how to not require null anymore, we still have to do something with existing code that uses Null

**Solution:** Probably make a new version of the dark language without null and deprecate the old one. Another alternative is to convert null into `()` (unit, or empty tuple).

**Alternative solution: **convert all uses of null into Json::Null_v0, which would be deprecated

**Status: TODO**

## v2 Spec

### v2 Language definition

Remove nulls

### v2 Standard library

```fsharp
// remove
Bool::isNull
```

###

###
