# Unwrap Or Throw (or Die!)

[![Build and Test](https://github.com/alexito4/UnwrapOrThrow/actions/workflows/swift.yml/badge.svg)](https://github.com/alexito4/UnwrapOrThrow/actions/workflows/swift.yml)

🎁 Unwrap an optional or throw an error if nil (or crash the program).

> Not invented here. The idea for **unwrap or die** and **unwrap or throw** has been around in the Swift community for years. You can read all about it in the [references](#References) below.

Read more: [Unwrap Or Throw (or Die)](https://alejandromp.com/blog/unwrap-or-throw-or-die/)

## Usage

This library provides different facilities to unwrap an `Optional` .

> Swift provides a way to go from a throwing function to an optional `try?` but it doesn't have an easy way to do the reverse operation.

### Coalescing with `raise`

Swift's `throw` is not an expression so we can't use it on the right side of the coalescing operator `??`. The `raise` function supplies this functionality. It’s a very simple function that throws the given error, but it makes it possible to use it in places where an expression is needed.

```swift
try someWork() ?? raise(YourError())
```

### Coalescing with `??`

An overload of `??` is provided to remove the need for the `raise` function. If you prefer to be succinct instead of explicit, you can just use an error on the right of the operator and it will just work.

```swift
try someWork() ?? YourError()
```

## Method `unwrapOrThrow`

If you don't like to abuse the coalescing operator to throw errors, you can instead use a method variant.

```swift
try someWork().unwrapOrThrow(YourError())
```

The library comes with a default error: `UnwrapError`. So you can call the method without specifying a custom error.

```swift
try someWork().unwrapOrThrow()
```

## ☠️ Unwrap or die

Despite the name of the library, you can also crash the program instead of throwing an error.

You can use the same techniques as when throwing errors but using `fatalError("reason for crashing")` instead:

```swift
try someWork() ?? raise(fatalError("reason for crashing"))
```

The compiler will show a warning on this line `Will never be executed` so instead of using `raise` you can directly `fatalError` on the right side of the `??` operator.

```swift
try someWork() ?? fatalError("reason for crashing")
```

Or if you prefer the method, you can also use it:

```swift
try someWork().unwrapOrThrow(fatalError("reason for crashing"))
```

This has the same result as force unwrapping `!` but with a better error message to help you see the problems on the logs.

> A barely use the *unwrap or die* since when I want to force unwrap I just do that and I don't find the lack of proper message an issue most of the time.
>
> That's why I don't need to introduce a facility to just pass a reason `String` directly into the unwrap operation. 

## References

- [johnno1962/Unwrap](https://github.com/johnno1962/Unwrap)
- [Introducing an “Unwrap or Throw” operator](https://forums.swift.org/t/introducing-an-unwrap-or-throw-operator/51905) 
- [Unwrap or Throw - Make the Safe Choice Easier](https://forums.swift.org/t/unwrap-or-throw-make-the-safe-choice-easier/14453) 
- [[Pitch] Introducing the “Unwrap or Die” operator to the standard library](https://forums.swift.org/t/pitch-introducing-the-unwrap-or-die-operator-to-the-standard-library/6207) 
- [SE-0217 - The “Unwrap or Die” operator](https://forums.swift.org/t/se-0217-the-unwrap-or-die-operator/14107) 

# Author

Alejandro Martinez | https://alejandromp.com | [@alexito4](https://twitter.com/alexito4)
