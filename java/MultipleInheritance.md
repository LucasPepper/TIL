# Multiple Inheritance

Multiple Inheritance is a feature of object oriented concept, where a class can inherit properties of more than one parent class. The problem occurs when there exist methods with same signature in both the super classes and subclass. On calling the method, the compiler cannot determine which class method to be called and even on calling which class method gets the priority.

**Why Java doesn’t support Multiple Inheritance?**

Example:

```java
// First Parent class
class Parent1
{
    void fun()
    {
        System.out.println("Parent1");
    }
}
  
// Second Parent Class
class Parent2
{
    void fun()
    {
        System.out.println("Parent2");
    }
}
  
// Error : Test is inheriting from multiple
// classes
class Test extends Parent1, Parent2
{
   public static void main(String args[])
   {
       Test t = new Test();
       t.fun();
   }
}
```

Output : *Compiler Error*

From the code, we see that, on calling the method *fun()* using Test object will cause complications such as whether to call *Parent1’s fun()* or *Parent2’s fun()* method.

## The Diamond Problem

The below Java program throws compiler error when run. Multiple inheritance causes diamond problem when allowed in other languages like C++.

        GrandParent
           /     \
          /       \
      Parent1      Parent2
          \       /
           \     /
             Test

```java
// A Grand parent class in diamond
class GrandParent
{
    void fun()
    {
        System.out.println("Grandparent");
    }
}
  
// First Parent class
class Parent1 extends GrandParent
{
    void fun()
    {
        System.out.println("Parent1");
    }
}
  
// Second Parent Class
class Parent2 extends GrandParent
{
    void fun()
    {
        System.out.println("Parent2");
    }
}
  
  
// Error : Test is inheriting from multiple
// classes
class Test extends Parent1, Parent2
{
   public static void main(String args[])
   {
       Test t = new Test();
       t.fun();
   }
}
```

## Simplicity

Multiple inheritance is not supported by Java using classes, handling the complexity that causes due to multiple inheritance is very complex. It creates problem during various operations like casting, constructor chaining etc and the above all reason is that there are very few scenarios on which we actually need multiple inheritance, so better to omit it for keeping the things simple and straightforward.

### How are above problems handled for Default Methods and Interfaces

Java 8 supports default methods where interfaces can provide default implementation of methods. And a class can implement two or more interfaces. In case both the implemented interfaces contain default methods with same method signature, the implementing class should explicitly specify which default method is to be used or it should override the default method.

```java
// A simple Java program to demonstrate multiple
// inheritance through default methods.
interface PI1
{
    // default method
    default void show()
    {
        System.out.println("Default PI1");
    }
}
  
interface PI2
{
    // Default method
    default void show()
    {
        System.out.println("Default PI2");
    }
}
  
// Implementation class code
class TestClass implements PI1, PI2
{
    // Overriding default show method
    public void show()
    {
        // use super keyword to call the show
        // method of PI1 interface
        PI1.super.show();
  
        // use super keyword to call the show
        // method of PI2 interface
        PI2.super.show();
    }
  
    public static void main(String args[])
    {
        TestClass d = new TestClass();
        d.show();
    }
}
```

Output:

Default PI1

Default PI2

If there is a diamond through interfaces, then there is no issue if none of the middle interfaces provide implementation of root interface. If they provide implementation, then implementation can be accessed as above using super keyword.

```java
// A simple Java program to demonstrate how diamond
// problem is handled in case of default methods
  
interface GPI
{
    // default method
    default void show()
    {
        System.out.println("Default GPI");
    }
}
  
interface PI1 extends GPI { }
  
interface PI2 extends GPI { }
  
// Implementation class code
class TestClass implements PI1, PI2
{
    public static void main(String args[])
    {
        TestClass d = new TestClass();
        d.show();
    }
}
```

Output:

Default GPI

[Source](https://www.geeksforgeeks.org/java-and-multiple-inheritance/)