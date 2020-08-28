# HTTP middleware

## **Problem**

Dark v1 had an implicit HTTP framework that was limited, opaque, and inflexible.

### **Problems with the Dark v1**

Users could not change how we processed a HTTP request

* can't have union types in JSON
* other encodings aren't supported and can't be added
* validation is manual and really annoying
* empty request body was impossible to use
* Headers in HTTP should be allowed to be specified twice
* magic sending did not match the magic receiving

### 

## **Solution: middleware**

We want to support the creation of "middleware-stacks", collections of functions which transform HTTP requests and responses in a common way. These would allow:

* users to customize how input to HTTP handlers is created
* separate handling for authenticated and unauthenticated routes
* gradually adding support for partially implemented features \(for example, v1 Dark can read latin1 and utf8, but not other encodings\)
* potentially graphql support could be a different middleware

Middleware stacks are pretty common in other languages, Python and Clojure being the two I'm most familiar with.

A middleware stack is simply a function wrapping another function.

If we have a function `handle(req : Request) -> Response`, then a middleware handler is a function

`middleware(innerFn : Request -> Response) -> (Request -> Response)` \(that is, it takes as an argument a function and returns a function, and both the parameter and returned functions take a request and return a result\).

### **What's in the Dark v1 "middleware"?**

### **How would users create, edit, and delete a middleware?**

### **Where would users specify a middleware for their handler?**

### **How would users change the middleware of some handler or set of handlers?**

\*\*\*\*

### 

## **Implementation**

**Middlewares**

* add content-length to response
* cookies? auth?
* create form-body
* create json-body from JSON and type
* create body
* create headers

