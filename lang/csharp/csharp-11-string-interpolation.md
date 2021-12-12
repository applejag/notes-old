---
date: 2021-12-12T12:32
tags:
  - programming/working with strings
  - programming/optimize memory usage
---

# C# 11 string interpolation

New features of C# 11 in .NET 6 results in super-optimized string interpolation.

## Sample

```cs
string FormatVersion(int major, int minor, int build, int revision) =>
    $"{major}.{minor}.{build}.{revision}";
```

## Before C# 11

Approximation of what C# 10 would generate:

```cs
string FormatVersion(int major, int minor, int build, int revision)
{
    var array = new object[4];
    array[0] = major;
    array[1] = minor;
    array[2] = build;
    array[3] = revision;
    return string.Format("{0}.{1}.{2}.{3}", array);
}
```

## Since C# 11

Approximation of what C# 10 would generate:

```cs
string FormatVersion(int major, int minor, int build, int revision)
{
    var handler = new DefaultInterpolatedStringHandler(literalLength: 3, formattedCount: 4);
    handler.AppendFormatted(major);
    handler.AppendLiteral(".");
    handler.AppendFormatted(minor);
    handler.AppendLiteral(".");
    handler.AppendFormatted(build);
    handler.AppendLiteral(".");
    handler.AppendFormatted(revision);
    return handler.ToStringAndClear();
}
```

## Benchmark

| C#  | .NET | Mean      | Ratio | Allocated |
| --- | ---- | --------- | ----- | --------- |
| 10  | 5    | 111.70 ns | 1.00  | 192 B     |
| 11  | 6    | 66.75 ns  | 0.60  | 40 B      |

> Note: The results are highly subjective to the machine running the benchmark.

## Key improvements

- No need for `object[4]` allocation.

- No need for the 4 `int` boxing allocations.

- Now supports writing `ref struct` types, such as `ReadOnlySpan<char>`

- Now supports writing into an existing `Span<char>` via the new extension method
  [`MemoryExtensions.TryWrite`](https://docs.microsoft.com/en-us/dotnet/api/system.memoryextensions.trywrite?view=net-6.0#System_MemoryExtensions_TryWrite_System_Span_System_Char__System_IFormatProvider_System_MemoryExtensions_TryWriteInterpolatedStringHandler__System_Int32__),
  eg:

  ```cs
  Span<char> mySpan = stackalloc char[64];
  var ok = mySpan.TryWrite(null, $"{major}.{minor}.{build}.{revision}", out var charsWritten);
  ```

- String interpolation, including when using aforementioned
  `MemoryExtensions.TryWrite`, can take use of newly `public`-made
  [`ISpanFormattable`](https://docs.microsoft.com/en-us/dotnet/api/system.ispanformattable?view=net-6.0)
  as an allocation-free `ToString` alternative.

- `StringBuilder.Append` and `.AppendLine` also supports these new string
  interpolations via `ISpanFormattable`, meaning the following `.Append` is also
  fast and allocation-free:

  ```cs
  var builder = new StringBuilder(); // obviously not allocation-free
  builder.Append($"{major}.{minor}.{build}.{revision}"); // allocation-free!
  ```

## Under the hood

- Uses [`ArrayPool<char>.Shared`](https://docs.microsoft.com/en-us/dotnet/api/system.buffers.arraypool-1.shared?view=net-6.0)
  for allocation-less string building.

  - Can be overridden to use `stackalloc`'d spans instead:

    ```cs
    string FormatVersion(int major, int minor, int build, int revision) =>
        string.Create(null, stackalloc char[64], $"{major}.{minor}.{build}.{revision}");
    ```

- [`DefaultInterpolatedStringHandler`](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.compilerservices.defaultinterpolatedstringhandler?view=net-6.0)
  grows if the `ISpanFormattable.TryFormat` returns false, and [then repeats
  until `.TryFormat` returns true](https://github.com/dotnet/runtime/blob/v6.0.0/src/libraries/System.Private.CoreLib/src/System/Runtime/CompilerServices/DefaultInterpolatedStringHandler.cs#L312-L315).
  The following works, but [reverts to using `ArrayPool<char>.Shared`](https://github.com/dotnet/runtime/blob/v6.0.0/src/libraries/System.Private.CoreLib/src/System/Runtime/CompilerServices/DefaultInterpolatedStringHandler.cs#L662):

  ```cs
  string FormatVersion(int major, int minor, int build, int revision) =>
      string.Create(null, stackalloc char[5], $"{major}.{minor}.{build}.{revision}");
  ```

## References

- <https://devblogs.microsoft.com/dotnet/string-interpolation-in-c-10-and-net-6/>
