# Dark v1 problems

This doc is a big list of the major problems with the existing version of Dark.

* Strings
  * concatenation is annoying \(no string interpolation\)
  * only way to enter newline, carriage return, tab is by pasting them
    * display of newlines in the editor is broken
  * strings wrap at 40
    * not configurable
    * annoying .and needs to be more sophisticated 
  * characters are not implemented
  * string length is implemented naively







  
  
Goals:

* Everything we add needs a continuous delivery way to change it
* Static types everywhere
* Expose the magic as real language things
* * Dark APIs to access traces, analysis, commands, etc
  * Optional parameters
  * middleware
* Sustainable
* * Refactoring, esp frontend
* Can embed just editor in HTML
* scalable
* graphql

  
Language

* String is stringSegment list where stringSegment = text of string \| escapedChar \| interpolatedExpr of expr
* Binary data, esp for HTTP
* Types from the start, type checker to supplement runtime
* * Both typechecker and runtime are functional reactive:allow making small change without redefining everything
* Ints are infinite precision
* Let-based destructuring
* Package manager from the start
* Write functions in Dark unless impossible
* * Package manager namespace
* Store dependencies in server, load only what’s necessary
* Solve dict vs record
* * Maybe using rust’s \`TypeName { .. record fields }\`
  * Or \#{ dict fields}
  * Functional updates for records, dicts, etc
  * Sets
* Invalid arguments - what do we do for functions
* WTF with JSON
* * What about values which can be one of two types?
* Types:
* * Primitives, named type variable
* Proper function application
* Fix problems with piping, first class functions
* Don’t make Results/etc part of the dval
* Traits from the start, for stringification, nice json
* * What about type signatures \(in HTTP result\)
  * Traits for handler return values
* Rust like methods allow concrete definition for each type
* Lazy/streams
* What namespace are Ok, Err, Nothing, and Just in?

  
Story:

* Make a story about building an entire app from scratch in 10 minutes
* What’s the code that allows this?

  
Framework:

* middleware, calling Dark functions, using traits to define things
* Users module
* Don’t support every minute CRONs, maybe a new design
* System namespace
* * Can see how many items in the workers, can introspect code, etc
* Workers can have arguments that define how they work
* * Can emit with preferences or else use the per-worker default
  * Similar for HTTP client \(retries and such\)
* Queues should support fanout and other patterns
* * Support automatic parallelization of “jobs”, maybe without queues
* Traits for the different types of parsing and unparsing
* DBs are persistent hash maps - do we have persistent sets, etc

  
Editor:

* Functions, etc, use fluid system \(can have buttons that appear with mouse for adding/removing params\)
* Shortcuts from the start
* Refactorings written in Dark
* Can have multiple editors on screen at once
* CRDT / OT from the start
* Type checker from the start

  
Analysis:

* Design for only calculating the minimum based on changes
* Support nested IDs
* Design for mixed-mode execution

  
Canvas:

* Webgl for canvas
* Permissions from the very start
* * Permissions = public \| namedPermission of permissions list \| orgMembers \| person of person
* Use rust for login/etc
* Only load what you see
* * Don’t assume everything is there. Especially for renaming across the canvas

  
Package manager:

* At the start
* * Functions should support being packages, user Fns, etc
* Packages can have functions + types
* Design actual upload system
* * takes into account transitive functions
  * Takes into account permissions
  * Code review is somehow involved
* Design namespacing
* * Actually write code that uses it
  * How can someone add a function into the namespace? Eg add mypackage/myfunction/String::randomFunction.
  * * How does it display, get added, etc

  
  
Client:

* graphQL from the start
* CSS-in-JS from the start
* Settings, keyboard shortcuts, etc
* Errors should have a code
* Move tests off testcafe

  
Dark-in-Dark:

* Build dark canvas
* Static assets
* Intercom/like thing
* * presence

  
Infra:

* Traces in S3 \(maybe use Algolia to search?\)
* Rust async
* k8s + vault + terraform + honeycomb
* Spanner?
* Separate user DB from account creds from traces
* Have separate sandbox + embed + free + premium environments
* QOS for queues \(make sure the stuff we build in Dark can be used safely, eg that queue backup doesn’t ruin presence\)

