# Code Styling Guide



It is important to say that code style serves no objective purpose in terms of functionality and is a purely aesthetic decision. However, what matters is having a style that is consistent and works for your team.

This styling guide is a simplified version of the [C# Standard Styling Guide](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions).


## Types of Casing

This styling guide refers to three distinct ways to capitalize keywords in code:

- `PascalCase`: Capitalize the first letter of all words.
- `camelCase`: Capitalize the first letter of all words _following the first word._ 
- `CAPITAL_SNAKE_CASE` Capitalize all characters and separate words with an underscore.

## Styling Guidelines

### Naming Conventions

Naming should be consistent with the following conventions:

#### Naming Fields
All field names should be `camelCase`.

```csharp
// Example Field Names
private string npcName = "Jerry";
private string teacher = "Mr. Gustin";
public int points = 10;
public char newLine = '\n';
```

#### Naming Constant and Readonly Fields

Any readonly or constant fields should be `CAPITAL_SNAKE_CASE`.

```csharp
// Example Constant Field Names
private const int POINTS_TO_WIN = 100;
private readonly string WIN_MESSAGE = "You won :D";
private const char DELIMITER = ';';
```

#### Naming Properties
All property names should be `PascalCase`. Property names should not 

```csharp
// Example Field Names
private string npcName = "Jerry";
private string teacher = "Mr. Gustin";
public int points = 10;
public char newLine = '\n';
```

#### Naming Methods
All method names should be `PascalCase`.

#### Naming Interfaces

All interface names must be `PascalCase` and **start with the letter** `I`.

```csharp
// Example Interface Names
public interface IInventoryItem {}
public interface IDestructible {}
public interface IInteractable {}
```

#### Naming Classes

All class names must be `PascalCase`.

```csharp
// Example Class Names
public class Student {}
public class NpcController {}
public class RaycastCombatController {}
```

### Commenting Conventions

#### General Comments

- Begin comment text with an uppercase letter.
- End comment text with a period
- Insert one space between the comment delimiter `//` and the comment text.
- For longer comments, either block comments
- If using block comments, indent each line of the comment.

```csharp
// This is an example comment.

/*
    This is an example of a longer comment
    that uses a block comment with indented
    lines. Aint this neat?
*/
```

#### XML Comments

Microsoft Visual Studio provides additional autocomplete information if methods, classes, and properties are given XML block comments. All methods and classes should have XML block comments. Properties should have XML block comments, but this is not explicitly required.

For methods with return types and parameters, they should have a `<param>` tag for each parameter and a `<returns>` tag for the return type.

Any additional considerations should be mentioned in `<remarks>`.

For more reading on XML block comments, see this article.

```csharp
    // XML Block Comment Example

    /// <summary>
    /// Removes the given follower from this manager.
    /// </summary>
    /// <param name="identityToRemove">The identity of the follower to remove.</param>
    /// <returns>True if the identity was removed, false otherwise</returns>
    public virtual bool RemoveFollower(FollowerIdentity identityToRemove)
    {
        return followers.Remove(identityToRemove);
    }
```
