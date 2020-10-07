# Real types

## Dark v1 problems

* Datastores use a "schema" - they should use a type
* HTTP's `request` variable are magically converted into JSON. The HTTP middleware does not have real types.
* Worker  `event` variables do not have types, and so they can receive types of any shape
* HTTPClient calls automatically convert JSON into objects of the right shape

