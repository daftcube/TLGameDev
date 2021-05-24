# Debugging 102

> "There has never been an unexpectedly short debugging period in the history of computers."
>
> <cite>Steven Levy</cite>

Now that we understand the fundamentals of debugging, we will now learn how to leverage modern debugging tools to assist in our debugging process.

AP Computer Science A and other courses emphasized debugging through the use of print statements and . While this builds good habits early, debugging with just print statements is not very efficient. This article will enlighten you to the glorious power of the modern debugger, and it will certainly become a crutch you will learn on for the long-term future! Muhahahaha!



## Methods and the Runtime Stack

Before we learn about the debugger, let's first talk about how functions actually execute in a program.

When code runs, the processor has an internal data structure called the 'Runtime Stack' that is used to keep track of the processor's current position within the program and provide a space to store local variables. 

You can imagine the runtime stack works like a literal stack of labelled notecards. Every time the processor calls a new method, it adds a 'notecard' to the top of the stack. On this 'notecard' is the current method and all of its local variables. When the processor reaches the end of the currently executing method, it removes the topmost notecard from the stack. 

Consider the following code:

```csharp
public class StackDemo
{
    // This function is where the program starts.
    public static void Main(string[] args)
    {
        C();
        A();
    }

    public void A()
    {
        // Do stuff
        B();
    }

    public void B()
    {
        // Do stuff
        C();
    }

    public void C()
    {
        // Do stuff;
    }
}
```

If we were watching the runtime stack as the program executed, it would look something like the following diagram:

![Stack Diagram](../../../_assets/stackDiagram.png)

The following diagram visualizes what the stack looks like at after each method call:

In technical terms, each one of these notecards is called a **stack frame.** The idea is that the stack frame on the very top of the stack will always have the currently executing function, and each stack frame under it represents the function that called the function above it. The bottom of the stack will have the function that represents the entry-point of the application.[^1]



## Stack Traces

When a program throws an unhandled exception or error, the program will crash. One of the things a program does when it crashes is that it writes the current stack trace to an error log. A **stack trace** is the list of all of the stack frames on the runtime stack. You can think of it as the precise location of where the program crashed, including the precise function where the error occured and all the functions called to reach that point.

A typical stack trace from an error log looks something like this:

```
```

Stack traces are invaluable to debugging because they help narrow down the logical path the program took to reach the error. With a stack trace, you can see exactly what path the code took to reach the place where it crashed. This helps narrow down the possibilities of the cause of the bug.

## Using the Debugger in Unity

This section will focus on teaching how to use the debugger in code within Unity projects. However, it is worth mentioning that almost all debuggers work in the same way, so almost everything you learn from this article should be readily applicable in many other programming languages and environments.

### Programs Required



### Attaching the Debugger

### Breakpoints

### Peeking Variables

[^1]: In multithreaded contexts, each thread gets its own stack, and the bottom of the stack will have the entry function for that thread. Multithreading is really complex though.