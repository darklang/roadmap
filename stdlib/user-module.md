# User module

One essential item in Dark is a User module. It should be trivial (take no more than 1 minute) to set up a user module. The user module should support:

* signing up, logging in and out
* password reset, including emailing
* password security - no visible passwords in a trace
* login with social accounts (where logins on multiple accounts can be combined)
  * github, twitter, facebook and google, at least
* a primary key that is not an email address
* easy integration with React and Vue, as well as iOS and Android
* Easy-to-use, styleable, HTML pages 
* Profile images (pre-populated from gravatar)
* Tight integration with traces - see a users' profile image on the trace
* Tight integration with feature flags - easily enable a flag for sets of users
* Cookies
* JWT



And it should aim to, in the future, support:

* Multi-factor auth
* allowing this be a login system for backends written in other systems
* adding other social accounts
* ability to see an audit log of a single user
* ability to automatically delete a single user's data for compliance reasons
* levels of authorization

TODO: 
