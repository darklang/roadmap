# HTTP handlers

## **Problem**

Dark v1 had an implicit HTTP framework that was limited, opaque, and inflexible.

### **Problems with the Dark v1**

Users could not change how we processed a HTTP request

* can't have union types in JSON
* other encodings aren't supported and can't be added
  * you can't upload video or other "bytes" and things that aren't strings
* validation is manual and really annoying
* empty request body was impossible to use
* Headers in HTTP should be allowed to be specified twice
* magic sending did not match the magic receiving
* No way to specify a 404 or a 500 handler
* No input validation for any fields
* Couldn't match against multiple segments
* No way to match arbitrary HTTP methods

TODO: JSON serialization/deserialization

## **Solution 1: middleware**

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

* converting to JSON
* converting from a byte string to utf-8
  * we supported converting for charsets us-ascii, iso-8859-1, latin1
* parsing path segments and inserting into the symtable
* adding request.formBody
* adding request.jsonBody
* adding request.body
* automatically respond to HEAD for GET requests
* converting response to JSON string
* converting response to other type?

### **How would users create, edit, and delete a middleware?**

### **Where would users specify a middleware for their handler?**

### **How would users change the middleware of some handler or set of handlers?**

## **Implementation**

**Middlewares**

* add content-length to response
* cookies?
* is logged in - add request.user
* create form-body
* create json-body from JSON and type
* create body from either form, json, or something else
* create headers
* tls redirect
* www redirect / apex domain

TODO: how would we allow validation where, for the admin page:

* an admin gets access
* a regular user gets told they're not an admin
* a non-logged-in person gets redirected to the homepage



## Editor integration

How do we write out HTTP handlers in fluid, taking into account middleware?

```text
// idea: type http::GET, and it fills out the parameters path and response
http::GET
  path : ___
  response : ___
___

// then we fill in the values and we get
http::GET
  path : /hello/:name/:age
  name : String
  age : String
  response : 
  
// these are defined by middleware such as:
fn get_body(raw_req :: HTTP::Request, user_obj, 
  
  

```

Problem: we don't have anyway to dynamically create data in a type sensitive way. I want the handler to say "there is this value \_body\_ that you now have available", how can I do that?

* Can the user\_obj just be untyped and everything writes to it and we know it's type because the type checker figures it out?

