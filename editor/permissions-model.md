# Permissions model

Dark should support fine-grained permissioning

## Dark v1 Problems

### Only owners exist

**Problem:** Users who are added to orgs become owners

**Solution:** Allow different permissions, and create common roles to reflect them

**Status: Design needed**

### Public canvases are not yet supported

**Problem:** We'd like users to show off their canvases \(and may even make this the default\)

**Solution:** We need enough permissions that this is safe to do

* Should be able to disable traces on a canvas
* Secrets should actually be secret
* We need a subset of traces that provide value,

**Status: Spec needed**

\*\*\*\*

## v2 Spec

### Trace design:

* By default, traces are private, even on public canvases \(can be made public, opt-in\)
* A subset of traces are shown to users
  * just the fact that they exist
  * when traces have users, show something else, like flags of the country the IP address is from
* Default values are generated for each type to help who are contributing

