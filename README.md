# Goals

This document is to describe the "2nd" version of Dark. The intent is to document the vision for Dark in the future, to allow us to get there incrementally.

This document is being written simultaneously with "writing" a few Dark applications. I say writing because they are being written not against a real implementation, but on paper, to try and articulate the design of the language without getting bogged down on the implementation \(v1 of Dark has an implementation which I already have a lot of experience with\).

_**Note:** this document is organized round Dark features, for example, the Strings page discusses v1 problems, solutions, detailed implementation, etc, all in one doc._

## Dark v2

These items are specific to Dark v2

### Fix issues from Dark v1

"v1" of Dark refers to the current state of Dark in August 2020. While this isn't really a v1, it serves as a reference point to discuss the shortcomings and challenges that we discovered by people using, creating, and maintaining it. [Dark v1 problems](dark-v1-problems.md) attempts to fully document the issues that users experienced.

### Make Dark more robust

Dark was brittle in a number of senses. We cut every corner we could in an effort to get Dark far enough along to get feedback about how it works. Though we went back and reworked several components \(in some cases several times\) and iterated quite broadly, many problems surfaced because components of Dark were MVP quality.

This is true of product and language features \(eg the error rail and feature flags\), as well as simple usability \(eg traces can be created, but not edited, searched, graphed, named, saved, etc\). In a sense, we often only implement the "C" and "R" of CRUD.

I want to fully think through the problem spaces and their solutions, to deliver an excellent experience.

A number of examples:

* use a real type system to avoid all the hacks in v1
* have an async implementation of the runtime to scale better

### Platformization

Dark v1 is very much a "product" - each feature was built and supported directly. Dark v2 attempts to be more of a platform, where more and more features are built in a way that they can be extended, or their own versions created.

For example, instead of having a dozen built-in refactoring commands, we'll expose the Dark language within the editor, allowing people to write transformations in the editor, in Dark itself.

Similarly, writing as much as possible in Dark itself.

### Continuous Delivery

A core tenet of Dark is that everything is live. That means we need robust ways to carefully make changes to running applications. We have some already:

* all stdlib functions are versioned
* basic feature flag support exists
* static assets are all versioned

However, we want to support a situation where any change can be made carefully and incrementally, such as:

* versioning functions
* support carefully changing other features, such as types, secrets, and handlers
* db migrations

In particular, incremental changes should be able to 

### Support different access levels

Right now, there are no access types and Dark can only be accessed by signed-in users. We want to support:

* users trying dark without logging in
* using the editor \(including live values\) embedded in other docs
* public canvases that can be edited by anybody
* granular ACLs

### Better infrastructure

Dark v1 was built quickly and hackily. We'd like to use:

* an async framework
* we plan to abandon OCaml for the backend for Rust, as the libraries, community, run-time, etc, are far far more mature in Rust.
* GraphQL: one reason that Dark isn't as robust as it could be is due to the overhead of supporting each CRUD operation in the client is that we need to create APIs for everything. I want to look at using GraphQL to ease that Loothe client should use graphQL to reduce the overhead of 

## High level goals of Dark

* trace-drive development: Live values / introspection / traces
* Instant, no fuss, infrastructure
* deployless: Changes reflected instantly
* APIs trivial to use

