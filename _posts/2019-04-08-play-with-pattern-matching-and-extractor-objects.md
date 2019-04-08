---
layout:       post
title:        "Playing with pattern matching and extractor objects in Scala"
description:  "Playing with pattern matching and extractor objects in Scala."
category:     articles
tags:         [scala, pattern-matching, functional-programing]
---

## Pattern matching
>Pattern matching is a mechanism for checking a value against a pattern. A successful match can also deconstruct a value into its constituent parts. It is a more powerful version of the switch statement in Java and it can likewise be used in place of a series of if/else statements.

```scala
  val ZERO = "zero"
  val ONE  = "one"
  val TWO  = "two"
  val MANY = "many"

  val number: Int = Random.nextInt(6)

  def numberAsLiteralString(value: Int): String = value match {
    case 0 => ZERO
    case 1 => ONE
    case 2 => TWO
    case _ => MANY
  }

  val numberAsString = numberAsLiteralString(number)
  //numberAsString = "one"
```

## Extractor objects
> An extractor object is an object with an `unapply` method. Whereas the `apply` method is like a constructor which takes arguments and creates an object, the `unapply` takes an object and tries to give back the arguments. This is most often used in pattern matching and partial functions.

## Resources
- https://docs.scala-lang.org/tour/pattern-matching.html
- https://docs.scala-lang.org/tour/extractor-objects.html
- https://alvinalexander.com/scala/how-to-use-pattern-matching-scala-match-case-expressions