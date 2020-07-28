# Var: a new feature from Java 10

It's a new reserved word, that permits type inference for local variables.

This feature is provided to enhance the Java language and extend type inference to declarations of local variables with initializers. This reduces the boilerplate code required, while still maintaining Java’s compile time type checking.

Remembering that Java is a Strong Typed and Static language, that is, we cannot initialize a variable with one type and change it to another, without a cast. The types are verified in Compilation time, not in Runtime.

Some 'var' examples: (try them using Jshell! It's the Java's REPL enviroment. Just type $ jshell on the terminal)

Inside a normal For loop:

```java

for (var x = 1; x <= 5; x++) {
           var m = x * 2; //equivalent to: int m = x * 2;
          System.out.println(m);
}
```

And here is how it used with For Each Loop:

```java
var list = Arrays.asList(1,2,3,4,5,6,7,8,9,10)
    for (var item : list) {
          var m = item + 2;
          System.out.println(m);
}
```

It works with Java 8 Stream:

```java
   var list = List.of(1, 2, 3, 4, 5, 6, 7)
   var stream = list.stream()
   stream.filter(x ->  x % 2 == 0).forEach(System.out::println)
```

Ternary Operator:

```java
var x = 1 > 0 ? 10 : "Less than zero"; System.out.println(x.getClass()) //Integer
var x = 1 < 0 ? 10 : "Less than zero"; System.out.println(x.getClass()) // String
```

Check additional informations about var: [Infoq](https://www.infoq.com/articles/java-10-var-type/)
