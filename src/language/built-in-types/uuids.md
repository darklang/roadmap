# UUID

Dark supports UUIDs directly.

## Dark v1 Problems

### UUID is a special type in the runtime, not a type defined using the type system

**Problem:** There should be very few "special" types, and there's no reason that UUIDs should be one of them

**Solution:** Add a built-in UUID type, presumably an alias of binary or perhaps a record with a bunch of u8s

**Status: TODO**

### **String::toUUID is in the wrong module**

**Solution:** Rename `String::toUUID` to `UUID::parse`

**Status: TODO**

## v2 Spec

### v2 Language definition

```
TODO
```

### v2 Standard library

```
// Removed
String::toUUID_v1(Str uuid) -> Result

// Added
UUID::parse(String) -> Result UUID Unit

Uuid::generate() -> UUID
```

### v2 Editor changes

###
