# Language versioning

Dark needs to be able to support evolution of the language. We intend to have different versions of the language, removing old language features and adding better ones.

At the same time, we have a goal that customers experience no downtime. We also don't want language versions to become a burden either to users or to us.

### Evolving within a single language version

As we control the language implementation, and all running instances of it, we can make changes to the language if we can make them fully compatible  \(or one deemed so close to fully compatible that no-one will be bothered by it\). The F\# rewrite is one example of this, and we made a number of different changes to Dark in this version which were compatible:

* added a real type system
  * this was compatible as the type system was barely used
* switch to bigint
  * since we didn't actually know what the overflow behaviour was, this was deemed safe
* changed `FnCall` to `Apply`, technically making functions first-class \(rather than just passing around lambdas\)

Some other changes we should be able to do:

* Remove `null` and change all instances to `Nothing`
  * Definitely some open questions on this
* Change variable, function and DB definitions to use an ID instead of looking it up by name
* Add Worker global vars like we have DB global vars
* Move OK/Nothing/Error/Just into types
* Move uuid, date and httpresponse into types

To keep this safe, we need a definition of what is a "safe" change. For example, we currently believe that changing error messages should be allowed to be a "Safe" change. To allow this, we need to inform users what behaviour we believe is changeable without notice, and to discourage the use of that behaviour.

### Support for multiple language versions

Sometimes there's a change which can't be done fully-compatibly. In order to support this, we want to make multiple versions of the language. This means, that we'll always need an implementation of the following for all language versions:

* RuntimeTypes
* ProgramTypes
* toEnduser serialization function
* toPrettyMachineReadable serialization function
* toRoundtrippable serialization function
* toQueryable serialization function
* a way to indicate which language version some data is serialized with
* a conversion function to/from the `n-1` language version
* a conversion function to/from the `n + 1` language version

#### Versioning code

User code needs to be versioned. Users will need to version functions, handlers and types. Each one can be versioned individually.

Dark stdlib functions are typed by the some version. If we add a new v7 of the language, what should happen to a stdlib function \(call this `myFunc_v2`\) that returns v6. Options:

* add `myFunc_v3` which returns v7
* change `myFunc_v2` so that it returns a v7 value
* we could also change it where appropriate and version it where appropriate

#### Interactions between language versions

Suppose we have a handler with v6 code, and it calls a function with v7 code. What should happen? Obviously, the v6 arguments should be converted to v7, the code should be run, and the v7 return value should be converted to v6.

This should work for any simple cases of calling code. Handlers calling functions, functions calling functions, handlers/functions emitting to other workers.

What about if we're trying to store a v7 value in a DB with type v6? We would convert the value to v6 and then store it.

#### Transitioning between language versions

Handlers should always aim to be on the latest version, as should functions.

But what about types and DBs? Should they even have language versions? What benefit would that bring? For storing a value in a DB, rows already have a Dark type field. That could represent the language version and we tell us which serializer to use. Then the retrieved value would be of a particular version and can be converted appropriately.

Types don't have any code associated with them to be versioned \(though if they did, presumably we could version those functions\). So it's not really clear why we'd have language versions for types, and what that would mean. So we can ignore this for now.

#### Migrating code automatically for users

Flags?

Dark should have a single version number, even if for example there is no difference between types in v2 and v3.



