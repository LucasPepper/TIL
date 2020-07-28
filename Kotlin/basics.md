# Kotlin

Desenvolvida pela JetBrains (a mesma empresa por trás do IntelliJ e outras IDEs), o Kotlin é conhecido por ser a linguagem oficial de desenvolvimento nativo do Android. Possui total interoperabilidade com o Java e vice-versa (também é executada pela JVM).

É conhecida por ser parecida com o Java, porém considerada bem mais concisa. Também é *Null-safe* (possui estratégias nativas para evitar os famosos NullPointerExceptions, como os *Nullable* *values* e *null* *checks*).

[Docs](https://kotlinlang.org/docs/reference/basic-syntax.html)

## Functions (fun)

```kotlin
Main Function:
fun main() {
    println("Hello world!")
}

// Tipos declarados após o nome da variável
fun sum(a: Int, b: Int): Int {
    return a + b
}

// Retorno inferido
fun sum(a: Int, b: Int) = a + b

// Side-effect (não necessariamente tem um retorno, mas executa algo dentro da função)
fun printSum(a: Int, b: Int): Unit {
    println("sum of $a and $b is ${a + b}")

// Obs: o Kotlin suporta String Template (Interpolação de Strings, começando com $ para identificar a variável)
}

```

## Variables

* val: variável de somente leitura ('constante). Pode-se atribuir valor somente uma vez
* var: pode atribuir-se várias vezes. Em alguns casos, o tipo pode ser inferido

```kotlin
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
val c: Int  // Type required when no initializer is provided
c = 3       // deferred assignment

var x = 5 // `Int` type is inferred
x += 1
```

## Conditional Expressions

```kotlin
fun maxOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}

// If também pode ser usada como uma expressão:

fun maxOf(a: Int, b: Int) = if (a > b) a else b

```

Muitas estruturas são muito semelhantes aos do Java, como o Enhanced For, while...

### For

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
```

Ou

```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```

### When expression

Equivalente ao Switch do C/Java

```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```

## Nullable values and null checks

Um valor que pode ser nulo deve ser explicitamente marcado com um **?**

```kotlin
// Retorna null se 'str' não possuir um inteiro
fun parseInt(str: String): Int? {
    return str.toIntOrNull()
}

fun printProduct(arg1: String, arg2: String) {
    val x = parseInt(arg1)
    val y = parseInt(arg2)

    // Using `x * y` yields error because they may hold nulls.
    if (x != null && y != null) {
        // x and y are automatically cast to non-nullable after null check
        println(x * y)
    }
    else {
        println("'$arg1' or '$arg2' is not a number")
    }
}


fun main() {
    printProduct("6", "7")
    printProduct("a", "7")
    printProduct("a", "b")
}
```

## Collections

Semelhante às Collections do Java/Python. "A collection usually contains a number of objects (this number may also be zero) of the same type. Objects in a collection are called elements or items. For example, all the students in a department form a collection that can be used to calculate their average age."

![Kotlin Collections](https://i.imgur.com/qQUbZhC.png)

Iterando por uma collection:

```kotlin
for (item in items) {
    println(item)
}

// Checando se uma collection contém um objeto utilizando o operador 'in':

when {
    "orange" in items -> println("juicy")
    "apple" in items -> println("apple is fine too")
}

// Utilizando Lambda expressions:

val fruits = listOf("banana", "avocado", "apple", "kiwifruit")
fruits
  .filter { it.startsWith("a") }
  .sortedBy { it }
  .map { it.toUpperCase() }
  .forEach { println(it) }

```

[Classes em Kotlin](https://kotlinlang.org/docs/reference/classes.html)
