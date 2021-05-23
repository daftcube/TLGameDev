# Field Property Injector

## Introduction

The Field-Property Injector, also called the 'Owen-jector,' is a debugging trick that allows us to see if and how a field is changing in the debug console. This is very useful for bugs where a particular field is not acting as expected. We used the Field-Property Injector to debug issues with fields being changed by other parts of the program in unexpected ways.

Most bugs do not require the Field-Property Injector trick to fix. The Field-Property Injector is a very specific and hacky tool for debugging. Try to use the debugger first, and leave this as a last resort.

## How it Works

In C#, there exists a feature called Properties. Properties act like fields, but can define custom get and set behavior. When a property is set equal to something, the property's `set` behavior is executed while passing the value through the keyword `value`. When the value of a property is read, the `get` behavior is called. 

The Field-Property Injector wraps the original field around a property. This allows us to add a `Debug.Log()` statement that we fire in the `set` behavior of the method, which is called whenever the property is set to a value.

## The Snippet

```csharp
private T _fieldName_ = 0;
public T fieldName {
  get { return _fieldName; }
  set { 
    Debug.Log("fieldName on " + gameObject.name + " changed from " + _fieldName.ToString() + " to " + value.ToString());
    _enemyId = value; 
  }
}
```

## How to Change the Snippet

Change all `fieldName` to the name of the field. For example, if we are trying to see how the field `private string str` is changing, replace all `fieldName` with `str`. **When replacing all `fieldName` with the name of the field, make sure not to delete any underscores that come before `fieldName`. The underscore is used to differentiate the underlying field that stores the value from the property that 'presents' the field to the program, and the snippet will not function properly in this case.**

Change all `T` to the type of the field. For example, if we are trying to see how the field `private string str` is changing, replace all `T` with `string`.

If you followed these steps, there should be no compiler errors in your code.

## Example of Snippet Implementation