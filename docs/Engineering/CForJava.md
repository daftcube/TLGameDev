# C# For Java Programmers

Many programmers from this course come from Introduction to Programming in Java or AP Computer Science A. Both of these classes teach programming through the lens of Java, but the game development class uses C#. This can lead to a bit of confusion as C# is very similar to Java, but different enough to cause troublesome issues.

This page is meant to serve as a **high level reference for the main differences** between Java and C#.

This page does not have every nuance between the two languages, nor does it talk much about the distinction between the Java Runtime Environment and the .NET Common Language Runtime. For a full breakdown of the differences between the languages, this [Wikipedia article](https://en.wikipedia.org/wiki/Comparison_of_C_Sharp_and_Java) is a great start.

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

### String Equality Quirk

In Java, there is a distinction between using `String.equals()` and the `==` operator to compare strings:

```java
// These strings have the same value, but are two distinct objects.
// You can tell because the 'new' keyword means 
// 'make a new instance of this object.'
String stringA = new String("HELLO, WORLD!");
String stringB = new String("HELLO, WORLD!");

// isSameObject will be false. This is because == tests for
// 'reference equality,' meaning whether the two variables
// contain a reference to the same object. stringA and stringB
// are distinct objects, so this will return false.
boolean isSameObject = stringA == stringB;

// hasSameValue will be true. This is because .equals() tests
// for 'value equality,' meaning whether the two objects have the
// same value. Because both objects have the same value "HELLO, WORLD!",
// they are considered value equivalent.
boolean hasSameValue = stringA.equals(stringB);
```

In C#, `==` across strings is actually defined for value equality. This means `==` in C# acts like Java's `.equals` for strings:

```csharp
// There isn't actually a C# equivalent to 'new String()' in Java.
// If we want to copy a string, we use String.Copy().
string stringA = String.Copy("HELLO, WORLD!");
string stringB = String.Copy("HELLO, WORLD!");


// hasSameValue will be true. This is because .equals() tests
// for 'value equality,' meaning whether the two objects have the
// same value. Because both objects have the same value "HELLO, WORLD!",
// they are considered value equivalent.
bool hasSameValue = stringA == stringB;
```

If you still want to specifically test for reference equality on strings, there is a seperate method `.ReferenceEquals()` that does exactly that:

```csharp
// isSameObject will be false. This is because ReferenceEquals
// tests for 'reference equality.' stringA and stringB
// are distinct objects, so this will return false.
bool isSameObject = stringA.ReferenceEquals(stringB);
```

However, for normal objects, C# follows the same reference-equality comparison for `==` and value-equality comparison for `.Equals()` that Java uses.[^1]

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

Otherwise, interfaces and classes work mostly the same between the languages. C# has a few extra features, but those shouldn't impact your existing knowledge.

## Java Primitives vs. C# Unified Types

In Java, primitive and object types are distinct. Primitives specifically refer to the numeric types `byte`, `short`, `int`, `long`, `float`, `double`; the character type `char`; and boolean type `boolean`; which can only have numeric, character, and boolean values respectively. If you wanted to print a primitive value as a string, you would need to call

In C#, all types derive from a root type `object`. The implication of this is that primitive types in C# act a lot like objects in-and-of-themselves. The root type `object` from which _all_ C# types derive has a set of base methods that even primitive types implement. Primitive types also have their own methods.

The following examples demonstrate this distinction.

### C# Primitives Implement ToString

In Java, if one wanted to return the `String` representation of a primitive type, a helper class would have to be used.

```java
void PrintPrimitiveDemo()
{
    int x = 1;

    // In java, we need to specifically call the Integer static class's
    // toString method.
    String xAsString = Integer.toString(x);  
}
```

However, in C#, every instance of the primitive type `int` has a method `ToString()` that returns the string representation of the number without needing to use a helper class.

```csharp
void PrintPrimitiveDemo()
{
    int x = 1;

    // In C#, int has the ToString method through its implicit interface.
    string xAsString = x.ToString(); 
}
```

### C# Primitives Have Implicit Boxing

Boxing and unboxing is the process of an object-oriented language turning a primitive type into an object type so it can be saved like an object in generic contexts. In Java, because primitive types and object types are distinct, boxing and unboxing is incredibly important. For example, if I wanted to create a generic `ArrayList` of `ints`, I would need to use the `Integer` wrapper class because Java does not support primitive generic types.

```java

ArrayList<Integer> arrayListOfInts = new ArrayList<Integer>();
arrayListOfInts.add(1);
// ...
```

However, in C#, because primitive types are basically objects, C# supports implicit boxing and unboxing. This means that you can use primitive types directly in generics:

```csharp
List<int> listOfInts = new List<int>();
listOfInts.Add(1);
// ...
```

## C# Is Java with More Stuff

In addition to the differences in syntax and handling of primitives, C# also boasts a lot more language features that increase its flexibility and ability to make performant code.

The following features are probably stuff you will never need to use, but just being aware of these features will help you in the future.

### Safe Casting with the `as` Keyword

In Java, if you wanted to convert one type into another, you would use a cast operation:
```java
// The following code represents a cast operation from
// type Object to Integer. If objectOfUnknownSpecificType
// was not an Integer, the cast would throw an exception and
// crash the program.
Object objectOfUnknownSpecificType = new Integer(1);
Integer objectAsInteger = (Integer)objectOfUnknownSpecificType;
```

You can also do this in C#:

```csharp
// The following code represents a cast operation from
// type Object to String. If objectOfUnknownSpecificType
// was not a String, the cast would throw an exception and
// crash the program.
object objectOfUnknownSpecificType = "Hello, World!";
string objectAsString = (string)objectOfUnknownSpecificType;
```

However, C# has a safer form of casting in the form of the `as` keyword. The `as` keyword attempts to cast the value on the left into the type on the right. If the value could not be cast, instead of throwing an `InvalidCastException`, the operation will return null instead.

```csharp
object objectOfUnknownSpecificType = "Hello, World!";

// objectAsString will be "Hello, World!". This is
// because objectOfUnknownSpecificType is a string,
// so the cast operation is successful.
string objectAsString = (string)objectOfUnknownSpecificType;

Student objectAsStudent = objectOfUnknownSpecificType as Student;

// objectAsStudentIsNull will be true. This is because
// objectOfUnknownSpecificType is not a Student, so
// 'objectOfUnknownSpecificType as Student' will return
// null instead of throwing an exception.
bool objectAsStudentIsNull = objectAsStudent == null;
```

This feature is useful when working in environments when the underlying types of the values being operated upon are unknown. However, if you know the cast operation will be successful in every case, just use a normal cast operation.

### Properties: Getters and Setters that Act Like Fields

In Java, if you wanted to have a private field that could be read by other classes, you would have to use the **mutator/accessor (also called getter/setter[^2]) pattern.**

The following shows an example of the mutator/accessor pattern and how an external class would access an object's private field through an accessor.

```java
public class Student
{
    private String name; // We want other objects 
                         // to know the student's 
                         // name, but not be able
                         // to change it. 

    public Student(String name)
    {
        this.name = name;
    }

    // To make this possible, we create a
    // 'getName' method whose only job is to
    // allow other objects to read our private
    // field.
    public String getName()
    {
        return name;
    }
}

// An example of how to access the private field of Student.
public class Main
{
    public static void main(String args[])
    {
        Student owen = new Student("Owen");
        Student finlay = new Student("Finlay");

        // We must call the method getName to get the name.
        System.out.println(owen.getName());
        System.out.println(finlay.getName());
        System.out.print("Owen is Finlay? ");
        System.out.println(owen.getName() == finlay.getName());
    }
}

```

In C#, Properties are a feature that allow you to make get and set methods that act like fields.

The following example shows how to achieve the same behavior from the Java example with C# properties:

```csharp
    // This class example uses properties and fields
    public class Student
    {
        // This code makes a private field 'name'
        // and exposes it through a public property.
        private string name = string.Empty;
        public string Name { 
            get { return name; } // When the field is read, this
                                 // get method will be called.
                                 // Here, we just return the name.
                                 // But, we could do other stuff.
            private set { name = value; }
        }

        public Student(string name)
        {
            this.name = name;
        }
    }

    public class Program
    {
        public static void Main(string[] args)
        {
            Student owen = new Student("Owen");
            Student finlay = new Student("Finlay");

            Console.WriteLine(owen.Name); // To get the value of
                                    // the property, we just access
                                    // it like a field.
            Console.WriteLine(finlay.Name);
            Console.Write("Owen is Finlay? ");
            Console.Write(owen.Name == finlay.Name);
        }
    }
```

C# also provides a shortcut for the mutator/accessor pattern to reduce the amount you must type:

```csharp
    // This class example uses properties and fields
    public class Student
    {
        // This code makes a private field 'name'
        // and exposes it through a public property.
        private string name = string.Empty;
        public string Name { 
            get { return name; }
            private set { name = value; }
        }
    }

    // This class uses the shortcut
    public class Student
    {
        // The following does the exact same
        // thing as the above snippet, but
        // uses the field-property shortcut
        public string Name { get; private set; }
    }
```

Of course, C# properties are the preferred way to do getters and setters in C#. However, if you are only comfortable with the Java way of doing things, that way works perfectly well in C#. It's better to write code you are comfortable with rather than trying (and potentially misusing) more complex language features!


## .NET Library vs Java Standard Library

In your Java programs, you often used objects from the Java standard library. C# has an equivalently large and robust standard library in the form of the .NET Framework. There are a few quirks, so we will outline them here.

### `System.Collections.Generic` vs `java.util.ArrayList`

As a Java programmer, you are likely used to using the class `ArrayList<T>` to represent generic dynamically-resizable arrays. You are also likely used to using collections from the `java.util.*` package.

In C#, the `System.Collections.Generic` namespace contains many generic collections. Among them is the `List<T>`, which is the C# equivalent of Java's `ArrayList<T>`.

The following is an example of using proper lists in Java:

```java
// Java example
import java.util.ArrayList;

public class ArrayDemo
{
    public static void main(String[] args)
    {
        ArrayList<Integer> listOfInts = new ArrayList<Integer>();
        ArrayList<String> listOfStrings = new ArrayList<String>();

        // Add numbers 0-100 to the list:
        for(int i = 0; i <= 100; i++)
        {
            listOfInts.add(i);
        }

        // Add 100 copies of "Hello" to listOfStrings.
        for(int i = 0; i < 100; i++)
        {
            listOfStrings.add("Hello");
        }
    }
}
```

And, the proper use of lists in C#:

```csharp
// C# Example
using System.Collections.Generic;

public class ArrayDemo
{
    public static void Main(string[] args)
    {
        List<int> listOfInts = new List<int>();
        List<string> listOfStringObjects = new List<string>();

        // Add numbers 0-100 to the list:
        for(int i = 0; i <= 100; i++)
        {
            listOfInts.Add(i);
        }

        // Add 100 copies of "Hello" to listOfStrings.
        for(int i = 0; i < 100; i++)
        {
            listOfStrings.Add("Hello");
        }
    }
}
```

C# does have an `ArrayList` object. However, you should not use it; it's a legacy object and does not offer both the type enforcement and performance of its generic `List<T>` counterpart.

Also keep in mind that **C# Primitives Have Implicit Boxing** (see similarly named section for more info), so you can use primitive types in generics without using a wrapper class.

[^1]: There is a method to the madness. In C#, you can actually override the behavior of operators. For example, I could define a `Point` class with fields `int x` and `int y`, and I could override the `+` operator to define addition for the points as the sum of both `x` and `y` values. In the case of `string`, what is happening under the hood is that the `string` object overrides the `==` operator to check for value equality rather than type equality. The default, however, is reference equality. That is why this particular quirk exists for C# strings.
[^2]: It is of the author's opinion that 'getter/setter' is the true name of this pattern. The author has held this position for six years and counting.