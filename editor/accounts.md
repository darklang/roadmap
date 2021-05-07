# Accounts

Dark supports both users and organizations, in a similar way that GitHub does

## Dark v1 Problems

### Only Dark employees can create organizations

**Problem:** There is no UI for organizations

**Solution:** Add UI, using a Dark canvas

**Status: Spec'ed or not spec'ed**

### **Users and orgs are the same thing**

**Problem:** It seems that it's wise to separate user and orgs somehow. We should do that.

**Solutions:**

* figure out best practices
* should not be possible to login as an org \(we've been implementing this by having the username be a dark email and the password be invalid\)
* keep orgs and 

**Status: Need to investigate best practices and make a design**

### Can't rename username or orgs

**Problem:** We would like to rename usernames or orgs. The main issue is that the builtwithdark urls would change

**Solution:** 

* stop using user.builtwithdark.com and create a new URL per canvas \(or possibly multiple per canvas\) using darklang.io
* then allow users to change their username, validating the same rules as otherwise exists

**Status: Need to spec darklang.io naming, and forwarding and deprecation policy for builtwithdark.com**

### **No trademark/usage policy for username**

**Problem:** Companies get into trouble when they make changes to usernames. Users are very protective of their identities so we should establish rules and norms early

**Solution:**

* investigate best practices
* Some obvious rules
  * Users can't sell usernames \(any financial transaction would result in the domain being taken\)
  * No squatting
  * Allow company to re-allocate usernames in event of abuse, significant confusion, or squatting, dead accounts

**Status: TODO**

\*\*\*\*

### 

