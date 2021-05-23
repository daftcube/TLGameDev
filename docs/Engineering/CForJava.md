# C# For Java Programmers

Many programmers from this course come from Introduction to Programming in Java or AP Computer Science A. Both of these classes teach programming through the lens of Java, but the game development class uses C#. This can lead to a bit of confusion as C# is very similar to Java, but different enough to cause troublesome issues.

This page is a reference for the main differences between Java and C#.

## C# Is Java with Slightly Different Keywords and Syntax

C# and Java have very close syntax. In addition, C# and Java are both object-oriented languages. This means that most of the features that define Java, namely object-oriented programming, exists in a very similar form within C#. There are a few differences in syntax though, so keep these in mind:

### Bools

In Java, the boolean type is called `boolean`. In C#, the boolean type is just called `bool`.

In Java:
```java
boolean x = true;
```

In C#:
```csharp
bool x = true;
```

### Strings

In Java, string objects are named `String`. In C#, they are named `string`.

### Foreach Loops

In Java, one would define a foreach loop like so:
```java
int[] collection = new int[10];
for(int value : collection)
{
    // Do stuff
}
```

In C#, the syntax is closer to the English language:
```csharp
int[] collection = new int[10];
foreach(int value in collection)
{
    // Do stuff
}
```

### Inheritance Keywords

Java uses the keywords `extends` and `implements` for inheritance of classes and interfaces.
```java
public interface ITestInterface { }
public class Superclass {}

// Subclass inherits from Superclass
public class Subclass extends Superclass {}

// ClassWithInterface implements an interface
public class ClassWithInterface implements ITestInterface {}

// SubclassInterface both inherits from superclass and implements the interface.
public class SubclassInterface extends Superclass implements ITestInterface {} 
```

In C#, we just use a colon to denote a class inheriting a subclass or interfaces. If we are implementing multiple interfaces, we use commas:
```csharp
public interface ITestInterface { }
public class Superclass {}

// Subclass inherits from Superclass
public class Subclass : Superclass {}

// ClassWithInterface implements an interface
public class ClassWithInterface : ITestInterface {}

// SubclassInterface both inherits from superclass and implements the interface.
public class SubclassInterface : Superclass, ITestInterface {} 
```

### C# Primitives Define Methods

In Java, primitive and object types are distinct. Primitives specifically refer to the numeric types `byte`, `short`, `int`, `long`, `float`, `double`; the character type `char`; and boolean type `boolean`; which can only have numeric, character, and boolean values respectively. If you wanted to print a primitive value as a string, you would need to call
```java
void PrintPrimitiveDemo()
{
    int x = 1;

    // In java, we need to specifically call the Integer static class's
    // toString method.
    String xAsString = Integer.toString(x);  
}
```

In C#, primitive types actually implement interfaces. The most important implication is that you can call certain methods directly on primitive types.
```csharp
void PrintPrimitiveDemo()
{
    int x = 1;

    // In C#, int has the ToString method through its implicit interface.
    string xAsString = x.ToString(); 
}
```
For the list of all methods on primitive types, go check out the documentation!

## C# Is Java with More Stuff

## C# Is Java 

## Unity MonoBehaviour Quirks

