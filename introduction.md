# Introduction

This document is to describe the "2nd" version of Dark. The intent is to document the vision for Dark in the future, which can then be used to design a path from v1 to v2.

This document is being written simultaneously with "writing" a few Dark applications. I say writing because they are being written not against a real implementation, but on paper, to try and articulate the design of the language without getting bogged down on the implementation \(v1 of Dark has an implementation which I already have a lot of experience with\).

After this chapter, the rest of this document is organized by feature - we discuss what we learned from Dark v1 and what problems users experienced, then explain what we believe the solution is. Finally, each section will have a spec for v2 of the feature. This will expand to \(or possibly link to\) an implementation plan to migrate from v1 to v2.

### Outline

Each section in the doc represents part of the Dark language, editor, platform, infrastructure, package manager, etc. Each section will follow a standard outline:

* Dark v1 problem
  * List of problems with outline
    * problem statement
    * solution description
    * status
      * spec'ed, implemented, unknown, etc
* v2 spec
  * v2 language changes
  * v2 editor changes
  * v2 standard library changes
  * etc

### Roadmap collaboration

There will at some point be a connection between this and issues in GitHub, or some project management software. For now, Dark users are welcome to add [GitHub issues in the Dark repo](https://github.com/darklang/dark) to discuss the contents of this roadmap, and in general to discuss or propose changes to Dark.

