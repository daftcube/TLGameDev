# C# For Java Programmers

Many programmers from this course come from Introduction to Programming in Java or AP Computer Science A. Both of these classes teach programming through the lens of Java, but the game development class uses C#. This can lead to a bit 

## C# Is Java with Slightly Different Keywords and Syntax

C# and Java are both object-oriented languages. This means that most of the features that define Java, namely object-oriented programming, exists in a very similar form within C#. There are a few differences in syntax though, so keep these in mind.

### Strings

In Java, string objects are named `String`. In C#, they are named `string`.

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


## C# Is Java with More Stuff

## C# Is Java 