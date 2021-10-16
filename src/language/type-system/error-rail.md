# Error Rail

The error rail isn't great, people get confused and it doesn't really do what we want.

Result.map and Option.map, etc, shouldn't go to the error rail

What if we replaced it by something from another language (eg Rust/coffeescript's `?` or F#'s `let!` (which is bind).

### let!

In F#:

```fsharp
let! x = 5 / 6
let! y = x + 2
return y + 1
```

Desugars into

```fsharp
Bind(5 / 6, fun x ->
Bind(x + 2, fun y ->
(y + 1)
```

Perhaps that's a better approach. It would imply needing a Bindable Trait or similar. See [https://fsharpforfunandprofit.com/posts/computation-expressions-bind](https://fsharpforfunandprofit.com/posts/computation-expressions-bind/)

