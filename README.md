# Dark v2

This document is to describe the "2nd" version of Dark. The intent is to document the vision for Dark in the future, which can then be used to design a path from v1 to v2.

This document is being written simultaneously with "writing" a few Dark applications. I say writing because they are being written not against a real implementation, but on paper, to try and articulate the design of the language without getting bogged down on the implementation \(v1 of Dark has an implementation which I already have a lot of experience with\).

After this chapter, the rest of this document is organized by feature - we discuss what we learned from Dark v1 and what problems users experienced, then explain what we believe the solution is. Finally, each section will have a spec for v2 of the feature. This will expand to \(or possibly link to\) an implementation plan to migrate from v1 to v2.

## Goals of Dark v2

### Overall goals of Dark

Obviously, the goals of Dark v2 are to support the goals of Dark. Those goals are to remove accidental complexity from writing backends, via:

* Instant infrastructure: create and scale infrastructure without thinking about it
* Deployless: Changes are safely deployed to production instantly
* Trace-drive development: Live values / introspection / traces
* Integrated tooling: by integrating the editor, programming language and infrastructure, reducing a huge amount of surface area
* making APIs as easy to call as functions

### Get to Product market fit

Currently, we get 10 user signups a day, and on average, 0 of them stick. We do have developers who love Dark, but not enough. To get developers loving Dark, we need two major things:

* developers need access to a large library of functions/modules/packages to access 3rd party services, such as Stripe, Twilio, Slack, etc.
* developers need to be able to trivially set up a user account system for their users

These are believed to be the major missing features. However, these missing features -- in order to be implemented with a great UX -- need the language and platform to expand to 

### Fix issues from Dark v1

"v1" of Dark refers to the current state of Dark in August 2020. While this isn't really a v1, it serves as a reference point to discuss the shortcomings and challenges that we discovered by people using, creating, and maintaining it. Most parts of this document start by listing the problems in v1, and [Dark v1 problems]() attempts to discuss overarching problems that users experienced.

### Platformization

Dark v1 is very much a "product" - each feature was built and supported directly. Dark v2 attempts to be more of a platform, where more and more features are built in a way that they can be extended, or their own versions created.

For example, instead of having a dozen built-in refactoring commands, we'll expose the Dark language within the editor, allowing people to write transformations in the editor, in Dark itself.

Many of the things that are built into Dark could be put in the package manager, such as refactoring commands, templates, etc. That way developers could add refactoring tools that would allow them or other to , for example, create handlers to receive API-specific webhooks, build CRUD generators, build tooling to automatically create entire API modules from swagger files, or automatically upgrade from deprecated interfaces to newer ones.

In the platformizing spirit, we also want to write as much of Dark in Dark as possible. Since Dark is much easier to write than most other languages, writing as many features as possible in Dark will lead to faster iteration cycles and so better outcomes. It will also allow contributors to contribute more easily to core services and features.

### Continuous Delivery

A core tenet of Dark is that everything is live. That means we need robust ways to carefully make changes to running applications. We have some already:

* all stdlib functions are versioned
* basic feature flag support exists
* static assets are all versioned

However, we want to support a situation where any change can be made carefully and incrementally, such as:

* versioning functions
* support carefully changing other features, such as types, secrets, and handlers
* db migrations

The rule here should be that all changes that affect the observable system to grandusers should be controllable and slow launched by the developer.

### Support different access levels

Right now, there are no access types and Dark can only be accessed by signed-in users. We want to support:

* users trying dark without logging in
* using the editor \(including live values\) embedded in other docs
* public canvases that can be edited by anybody \(safely, that is, so solving things like access to traces, passwords, etc\)
* granular ACLs

### Better infrastructure

Dark v1 was built quickly and hackily. We'd like to use:

* an async language/framework so that things like calling HTTP functions do not use all the resources, and so that functions like `sleep` can be supported
* we plan to abandon OCaml for the backend for Rust, as the libraries, community, run-time, etc, are far far more mature in Rust.
* GraphQL: one reason that Dark isn't as robust as it could be is due to the overhead of supporting each CRUD operation in the client is that we need to create APIs for everything. I want to look at using GraphQL to ease that.

### Make Dark more robust

Dark was brittle in a number of senses. We cut every corner we could in an effort to get Dark far enough along to get feedback about how it works. Though we went back and reworked several components \(in some cases several times\) and iterated quite broadly, many problems surfaced because components of Dark were MVP quality.

This is true of product and language features \(eg the error rail and feature flags\), as well as simple usability \(eg traces can be created, but not edited, searched, graphed, named, saved, etc\). In a sense, we often only implement the "C" and "R" of CRUD.

I want to fully think through the problem spaces and their solutions, to deliver an excellent experience.

A number of examples:

* use a real type system to avoid all the hacks in v1
* have an async implementation of the runtime to scale better



### Improve the feeling of safety while coding

Dark feels unsafe to users. They feel reluctant to make changes because they don't know if they will work, or if they'll break things. We need ways to make this safer:

* unit tests on functions and handlers will make users feel safe
* type checking:
  * by having type checking on functions and handlers, users can feel confident that their code will work
* error tracking
  * highlight \(and email users about\) errors in their apps
  * highlight data being sent that isn't being used by the app \(eg form fields\)
    * is this the same as warn/error log messages?
* application understanding
  * email users about their traffic so that they understand that their code works
  * allow people search their traces for 
* feature flags:
  * make feature flags global and easier to use and understand
* fix size of traces
* fix editor layout
  * the layout of the canvas
* education so that users can understand



