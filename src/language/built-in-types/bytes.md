# Bytes

Non-unicode sequences of bytes are supported as the `Bytes` type.

## Dark v1 Problems

### **HTTP body is a string (if not json)**

**Problem:** We automatically convert HTTP bodies into strings, even if it's not valid Unicode

**Solution: **Use types to specify how to convert bytes to bodies, such that the logical code is as follows `body |> Bytes::toString |> Json.Deserialize<MyType>`

**Status: TODO**

### HTTP request raw values are strings but they might not be

**Problem:** HTTP request `raw` field is a string, but

**Solution: **

**Status: Spec'ed or not spec'ed**

### HTTP **client calls use Strings, so you can't send bytes**

**Problem:** We'd like to be able to make raw http calls

**Solution: **Add a type, or even middleware, to HTTP calls such that we can use more types

**Status: Spec'ed or not spec'ed**

##

## v2 Spec

### v2 Language definition

```
```

### v2 Standard library

```
```

### v2 Editor changes

###
