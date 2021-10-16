# Modules and Namespacing

Modules and namespaces are used to separate functions and types so that they can have the same names without treading on each other.

## Dark v1 Problems

### Package manager function names are ugly

**Problem: **

**Solution: TODO**

**Status: Design needed**

### **Built-in types have no module**

**Problem:** Ok, Error, Just and Nothing are not in any namespace

**Solution: **Ok should be

**Status: Design needed**

### **Built-in types have no module**

**Problem:** Ok, Error, Just and Nothing are not in any namespace

**Solution: **

**Status: Spec'ed or not spec'ed**

****

##

## v2 Spec

### v2 Language definition

```
type FQFnName =
  | Stdlib { module = string, name = string, version = int }
  | PackageManager
      { owner = UserID,
        package = string,
        module = string,
        name = string,
        version = int
      }
```

### v2 Standard library

```
```

### v2 Editor changes

###
