# Regex

## Dark v1 thoughts

Dark v1 does not have regex, due to the technical challenge that the OCaml native regex implementation we used \(re2\) does not compile to JS.

We want to use a regex implementation which can not be DOSed. Parse apparently had big problems with their regex.

Users asked for regex a lot.

I've never seen a regex implementation that was as easy to use as Perl's, so that's what we're aiming for:

```text
# does it match?
if ($str =~ /ul/) { ... }

# capturing
if($line =~ /name:\s+(\w+\s+\w+),\s+period:\s*(\d{4}\-\d{4})/)
  $composers{$1} = $2;


```



