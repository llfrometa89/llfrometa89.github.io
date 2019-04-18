---
layout:       post
title:        "Playing with pattern matching and extractor objects in Scala"
description:  "Examining two powerful benefits of the Scala language, such as pattern matching and the extractor objects."
category:     articles
tags:         [scala, pattern-matching, extractor-objects, functional-programing]
---

[//]: <> (trans-es -> description:Examinando dos poderosas bondades del lenguaje Scala como son pattern matching y de el extractor object.)

I want to show you two powerful syntax that the scala language has.

[//]: <> (trans-es -> Quiero mostrarle dos poderosas sintaxis que posee el lenguaje escala.)
 
We will start with the Pattern matching, this syntax in used when we want to match one or more patterns in an expression such as a constant pattern, variable pattern, constructor pattern, sequence pattern, tuple pattern or type pattern.

[//]: <> (trans-es -> Comenzaremos con el Pattern matching, esta sintaxis en usada cuando queremos hacer coincidir uno o más patrones en una expresión como pueden ser un patrón constante, patrón variable, patrón constructor, patrón de secuencia, patrón de tupla o patrón de tipo.)

## Pattern matching
>Pattern matching is a mechanism for checking a value against a pattern. A successful match can also deconstruct a value into its constituent parts. It is a more powerful version of the switch statement in Java and it can likewise be used in place of a series of if/else statements.

The following examples show many different types of patterns that can be used:

[//]: <> (trans-es -> El siguiente ejemplos muestra muchos tipos diferentes de patrones que se pueden usar:)

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

......

## Constant patterns

Any literal can be used as a constant. A constant pattern can only coincide with itself, this means that if we declare a variable with value 2 it will only coincide with an Int value of 2. e.g:

[//]: <> (trans-es -> Cualquier literal puede ser usado como una constante. Un patrón constante solo puede coincidir con si mismo, esto significa que si declaramos una variable con valor 2 solo coincidirá con un valor Int de 2. e.g:)

```scala
val value: Int = 2
val result: String = value match {
  case 2 => "two"
  case true => "true"
}
// res0: result: String = "two"
```

## Variable patterns

A variable pattern matches any object just like the wildcard character. For example, at the end of a match expression, you can use the wildcard character to match any type or capture the value in a variable. e.g:

[//]: <> (trans-es -> Un patrón variable coincide con cualquier objeto al igual que el carácter comodín. Por ejemplo, al final de una expresión de coincidencia, puede usar el carácter comodín para coincidir con cualquier tipo o capturar el valor en una variable. e.g:)

```scala
val value: Int = 2
val result: String = value match {
  case _ => "any"
}
// res0: result: String = "any"
```
Or you can write this instead:

```scala
val value: Int = 2
val result: String = value match {
  case foo => s"My value is $foo"
}
// res0: result: String = "My value is 2"
```

[//]: <> (trans-es -> )

[//]: <> (trans-es -> )

[//]: <> (trans-es -> )


## Resources
- <a href="https://docs.scala-lang.org/tour/pattern-matching.html" target="_blank">https://docs.scala-lang.org/tour/pattern-matching.html</a>
- <a href="https://docs.scala-lang.org/tour/extractor-objects.html" target="_blank">https://docs.scala-lang.org/tour/extractor-objects.html</a>
- <a href="https://alvinalexander.com/scala/how-to-use-pattern-matching-scala-match-case-expressions" target="_blank">https://alvinalexander.com/scala/how-to-use-pattern-matching-scala-match-case-expressions</a>