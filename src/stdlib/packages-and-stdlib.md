# Package manager

Most of the libraries in Dark, especially for access to 3rd party services (Twitter, Stripe, etc), will be provided by users in the package manager.

Packages will have a naming scheme similar to github (username/package, eg "darklang/tablecloth") and a module and versioning system like Dark's current stdlib (module::function_version, eg "String::trim_v1").

### Dark v1 problems

* In Dark, packages do not have versions, their contents do. Individual functions, types, etc, are versioned, and once added to a package are never removed. Instead, they can be deprecated by future functions.
* TODO: how do we slow roll out new versions if we're not sure they're ready?
* TODO: do we address functions by hash/ID, or by name?
* What is the mechanism to upload functions?
* What about dependencies?
* TODO: nested modules
* How do traces work? we want traces to be available to users of functions, and we want to allow users to be able to submit traces to package managers (probably with info redacted)



### Other

In all languages, there is a question of allowing the user to add functions to libraries they don't control. Given a function `module.x`, they want to add `module.x1` which is sort of different, without having to write `MyModule.x1` instead. JS and Ruby use monkey patching, in C++ and F# you can open the module and add to it. In Java you use inheritance, sorta.

In Dark, you add a function which is in a different namespace, but the editor makes it feel like you didn't. So if you've added `mymodule/stdlib/String::trimDifferent`, the editor will show you `String::trimDifferent` instead. Unless there is another `String::trimDifferent` in scope, in which case it will disambiguate.



### Definition of a package, v2

A dark toplevel is a namespace, defined as `<owner>/<package>/<module>::<item>_<version>`. The owner is the user or organization who owns it, similar to github. similar to github. Within this namespace, 



#### Security

* dont allow access to global variables (DBs)
* only allow httpclient calls to know domains
* packages must typecheck

#### Standard packages

The dark standard library is within `dark/stdlib`.

TODO
