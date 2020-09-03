# Package manager

In Dark, packages do not have versions, their contents do. Individual functions, types, etc, are versioned, and once added to a package are never removed. Instead, they can be deprecated by future functions.

TODO: how do we slow roll out new versions if we're not sure they're ready?

TODO: do we address functions by hash/ID, or by name?

What is the mechanism to upload functions?

What about dependencies?

TODO: nested modules



### Definition of a package, v2

A dark toplevel is a namespace, defined as `<owner>/<package>/<module>::<item>_<version>`. The owner is the user or organization who owns it, similar to github. similar to github. Within this namespace, 



#### Standard packages

The dark standard library is within \`

