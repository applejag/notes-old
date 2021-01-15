---
date: 2021-01-15T21:38
tags: 
  - programming/optimize memory usage
  - programming/quality of life
  - programming/working with strings
  - lang/c#
---

# Interchanging ReadOnlySpan&lt;T&gt;, string, and char[] in C#

Most think of only using `Span<T>` and `ReadOnlySpan<T>` (in C\#) in places they
need ultimate performance. But there is another use case where they are offly
useful. And that is when you start working with `string` and `char[]`.

## Relying on ReadOnlySpan&lt;T&gt;, letting callers decide types

If you make your utility methods deal with `ReadOnlySpan<T>` (wherever
appropriate[^inap-span-usage]) instead of `string` or `char[]`, you will only
have to make slight refactorings to adjust for correct methods used. Most just
include indexing and slicing, which can be done with `span.Slice(i, len)` or
`span[a..b]` instead of `string.Substring(i, len)`. Other common operations such
as concatenation does have proper support already throughout the .NET standard
library (See: [[[b3016de3]]]).

With that you can then let the caller of the function choose between sending a
range of different types, as `string`, `Span<T>`, and `char[]` all can be
implicity casted to `ReadOnlySpan<T>`.

Let's say you have the following method:

```cs
public class StringHelper
{
    /// <summary>
    /// Example: <c>"john.doe"</c> as username and <c>['.']</c> as separator, gives <c>"doe"</c>
    /// </summary>
    public ReadOnlySpan<char> GetLastSegment(ReadOnlySpan<char> source, ReadOnlySpan<char> separators)
    {
        // ...
    }
}
```

Now in your code production code, let's say you may have those name name
separators specified as an `char[]` because you also need it in a `string.Split`
operation you're doing later on. No worries! Just pass in that array as-is:

```cs
public class UsernameHelper
{
    private static readonly char[] _nameSeparators = new [] { '.', '-', '_' };

    public string GetNameSegments(string username)
    {
        return username.Split(_nameSeparators, StringSplitOptions.RemoveEmptyEntries);
    }

    public string GetLastName(string username)
    {
        return StringHelper.GetLastSegment(username, _nameSeparators);
    }
}
```

And then later in your tests, you want to declare test cases in NUnit, and you're
fully allowed to do that by representing the name separators as a string instead
_(which is very helpful as you cannot have array constants in attributes)_:

```cs
public class StringHelperTests
{
    // You cannot have array definitions in attributes
    [TestCase("john.doe", ".", "doe")]
    [TestCase("steve-smith", "-", "smith")]
    [TestCase("anne-frid.von.bygel", ".-", "bygel")]
    public void CorrectlySplits(string input, string separators, string expected)
    {
        var result = StringHelper.GetLastSegment(input, separators);
        Assert.AreEqual(expected, result);
    }
}
```

No extra casting required! Perfectly fine to just feed the separators in as a
string instead. Need an empty array of `char`? Just pass an empty string!
They're stored in memory in the same way, so why not take advantage of that?

## Summary

The `ReadOnlySpan<T>` type was introduced to allow for writing hyper-optimized
array managing code, but the use cases does not stop there.

The biggest downside of using `ReadOnlySpan<char>` everywhere instead is partily
because it's a `ref struct` and has those limitations put on it, but worst
(and almost silly, in a way) is that the type name is so long! It clutters the
signatures of your methods enourmously, though it does go hand in hand with
some clean code principles as it gives you yet another reason to make your
functions smaller and take less arguments.

[^inap-span-usage]: As you cannot have `ref struct`s in classes or records, those are inappropriate. Other examples are in asyncronous code and enumerators.
