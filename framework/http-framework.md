# HTTP handlers

## **Problem**

Dark v1 had an implicit HTTP framework that was limited, opaque, and inflexible.

### **Problems with the Dark v1**

* Users could not change how we processed a HTTP request
  * other encodings aren't supported and can't be added
  * you can't upload video or other "bytes" and things that aren't strings
  * Headers in HTTP should be allowed to be specified twice
* No input validation for any fields
  * you can validate manually which is really annoying
  * a JSON field is not type checked and could be any type
* empty request body \(with just incompletes\) was impossible to use
* magic sending did not match the magic receiving
* No way to specify a 404 or a 500 handler
* No way to match arbitrary HTTP methods
* Can't have a HEAD handler \(the framework converts the request to a GET\)
* Should the standard 404 have a content-type header
* if you return a string, it shouldn't have quotes, right? I mean it already is ct: text/plain

## **Solution 1: middleware**

We want to support the creation of middleware stacks, collections of functions which transform HTTP requests and responses in a common way. These would allow:

* users to customize how input to HTTP handlers is created
* separate handling for authenticated and unauthenticated routes
* gradually adding support for partially implemented features \(for example, v1 Dark can read latin1 and utf8, but not other encodings\)
* potentially graphql support could be a different middleware

Middleware stacks are pretty common in other languages, Python \(WSGI\) and Clojure \(Ring\) being the two I'm most familiar with.

A middleware stack is simply a function wrapping another function.

If we have a function `handle(req : Request) -> Response`, then a middleware handler is a function`middleware(innerFn : Request -> Response) -> (Request -> Response)` \(that is, it takes as an argument a function and returns a function, and both the parameter and returned functions take a request and return a result\).

### **What's in the Dark v1 "middleware"?**

* The Dark middleware is complicated and works poorly.

Responses

* Anytime we infer a content-type, the content type is `text/plain; charset=utf-8` unless the value is an Object or List, in which case it is `application/json; charset=utf-8`
* If the response is a HttpResponse value, then we infer a content-type if none exists, then convert it to json or plain text using built-in functions
* If the response in a HttpRedirect response, the value is ignored.
* If the response is on the ErrorRail, a response of 404 is returned \(**Note:** even if the ErrorRail is an Error\)
* If the response is a DError, a 500 is returned with an error message.
* If the response is none of these, then we convert it to JSON and infer the header, using a code of 200. **Note: this often gives a JSON string response with a text/plain header. this is unexpected and bad, and also the most common outcode. Instead it should content-negotiate**
* Cors headers are then added, based on the CORS settings in the canvas
* The value is then converted to Bytes, and returned to the caller
* At no point does Dark do any content-negotiation

Requests

* parsing path segments and inserting into the symtable
* returning 418 for text/ping
* creating a request object with formBody, jsonBody, cookies, url, body
* automatically respond to HEAD for GET requests. Currently HEAD handlers can be created but will not be hit
* automatically handling OPTIONS/CORS
* using the dark favicon if none is provided
* returning a blank sitemap or favicon
* converting response to JSON string
* converting response to other type?

### **How would users create, edit, and delete a middleware?**

* middleware is just a function with a specific type signature
* each step in the middleware would have to type check with the previous middleware
* final middleware shows the type of request

### **Where would users specify a middleware for their handler?**

* the editor would allow the choice. HTTP uses the default stack \(defined at handler creation time\), and you can change the middleware stack directly, including changing to use the "feature flag middleware" stack

### **How would users change the middleware of some handler or set of handlers \(eg feature flags\)?**

* a feature flag middleware which chooses which of the two middleware stacks to process

## **Implementation**

**Middlewares**

Middlewares are typed functions that contribute a small, composable part of decoding a web request for the handler to use. Middlewares receive a request, and then based on the request, may choose to call the next middleware or simply return a response instead. As such, middlewares receive as parameters both the request so far, as well as the next middleware to call. They are responsible for calling the next middleware, possibly changing the request first and possible altering the response as well. This leads to middlewares having the following shape:

```text
let myMiddleware (arg : myMiddlewareArgType) next =
  fun (req : 'req) ->
    let doSomethingToRequest req = { req with someExtraField = someFunction req }
    let doSomethingToResponse res = { res with someExtraField = someFunction res }
    let shortCircuitResponse = { status = 404, body = "", headers = [] }
    if someCondition req
    then shortCircuitResponse
    else req 
         |> doSomethingToRequest
         |> nextMiddleware
         |> doSomethingToResponse
```

A middleware returns a function which takes a request. A middleware takes whatever arguments it needs, as well as the next middleware to call. As such, a middleware stack looks like this:

```text
let middleware =
  (\ctx -> handler ctx) // shown like this for clarity
  |> addQueryParams url
  |> addHeaders headers
  |> readVarsFromURL
  |> addJsonBody headers body
  |> addFormBody headers body
  |> addCookies headers
  |> processErrorRail
  |> optionsHanderMiddleware
  |> headHandlerMiddleware
  |> textPingMiddleware
  |> sitemapFaviconMiddleware middleware emptyRequest
```

Each middleware wraps the previous one, so the outermost middleware is last, and the handler comes first.

EmptyRequest is an empty record, and each middleware adds fields to it until the request has the shape required by the handler. It then returns a response, which can also have fields added to it by middleware wishing to send those fields to other middlewares.

As such, the types of the entire middleware have to add up to the type of the handler.



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
* add fields like in elm, start with an empty record and add fields to it. Type checks the whole way down

