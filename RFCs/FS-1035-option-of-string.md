# F# RFC FS-1035 - Support for converting a String to an Option

This RFC covers the detailed proposal for this suggestion.

* [x] Implementation (with discussion): [In progress](https://github.com/Microsoft/visualfsharp/pull/FILL-ME-IN)

# Summary
[summary]: #summary

Ability to convert from a non-null string to an `string option`, taking into account empty strings and whitespace-only strings.

# Motivation
[motivation]: #motivation

Given the `Option.ofObject` combinator introduced in F#4.x, it is a natural extension to want to convert from a String to an option type
in many cases. Unfortunately an empty or whitespace-only string will be mapped as to some string rather than None (which in virtually all
cases is what the user wants).

# Detailed design
[design]: #detailed-design

This would be a simple function added to the existing `Option` module in FSharp.Core which would take in a string and return an option.

Example code:

```fsharp
let ofString (value:System.String) =
    if System.String.IsNullOrWhiteSpace value then None else Some value
```

# Drawbacks
[drawbacks]: #drawbacks

Potential for confusion for a beginner - when to use `Option.ofObj` and `Option.ofString`?
Increase of surface area?

# Alternatives
[alternatives]: #alternatives

Manual implementation across all projects that need this. It's a one line function so easy to do, but it crops up very often,
hence the desire to incorporate into FSharp.Core

# Unresolved questions
[unresolved]: #unresolved-questions

* What name should this function have? Possibly `Option.ofString` might imply that this function *parses* the contents of string
somehow, although the type signature of string -> string option (plus xml comments) should make this clear.
