# Debugging 101

> "If debugging is the process of removing software bugs, then programming must be the process of putting them in."
>
> <cite>Edgar Djikstra</cite>

Bugs are an inevitable and unavoidable part of software engineering. This is mainly because programming is _really complicated_ and no one is perfect. Just take a minute to think about it; in order for a program to execute successfully, a million things need to function perfectly. Any single mistake - be it a logic error in your code, an unhandled runtime exception, or even a problem with the computer's hardware - can cause the program to crash. Honestly, it is amazing that anything works at all!

As a programmer, it is likely that you will **spend more time debugging than writing code.** So, it's important to learn not just how to code, but how to debug effectively. This article will discuss debugging techniques to hopefully reduce the time you spend on bugfixing as much as possible.

## The Two Types of Bugs

The first type of bugs are **syntax errors.** Syntax errors are errors in the formatting of your code that prevents it from being compiled and run. These are fairly easy to fix; you just need to look at the compiler error and find the line to fix. If you are working in a integrated development environment like Visual Studio, your code editor will actually do a great job in underlining syntax errors in your code as you write it. Overall, syntax errors are nothing to worry about.

<figure>
  <img src="https://www.bbvaopenmind.com/wp-content/uploads/2015/11/bug-1024x348.jpeg" />
  <figcaption>You might be surprised to learn that the first documented digital computer bug was caused by a literal bug in the system. This bug was found in the ENIAC in 1947.</figcaption>
</figure>

The second and scarier type of bug is a **logic error.** Logic errors are issues with how your code actually functions; your code might compile and execute, but it does not correctly solve the problem or throws an error when running. Logic errors are much harder to solve and require looking at the code line-by-line to diagnose what is going wrong.




## Debugging: Scientific, not Algorithmic

There exists no program, algorithm, or set of steps that can debug all programs.

It is actually impossible to create a program that can debug all programs. This might seem like an impossible statement; after all, code is just executed logic, and logic can prove statements to be true or false. However, it has been mathematically proven that there exist statements that are true but can never be proven. If you are curious about why there cannot exist a program to debug all programs, you should check out this [Veritasium video](https://www.youtube.com/watch?v=HeQX2HjkcNo) on the topic!

This leaves debugging as a uniquely human experience. Luckily, we are able to solve problems with enough practice, good technique, and the occasional windfall of lucky genius.

## The Steps to Successful Debugging

While an algorithm can't find bugs for us, we can use a set of steps to work through problems in a methodical way. The following steps aim to maximize forward progress while minimizing backtracking.

### Understand the Program and Your Tools

The first step to solving a problem is understanding the context in which the problem is occuring. Be sure you understand your codebase and all of its moving parts. If using third-party libraries or APIs, be sure to also understand how they interact with your application.

It might seem silly, but if your bug involves code that you didn't write, you may want to consult that code's documentation to see if the behavior is actually a bug. Some behavior that looks like a bug might actually be a documented feature or documented shortcoming of some other part of the codebase.

Understanding the tools you use is also very important. Many development environments include a built-in debugger that can make tracing through programs easier. We will discuss how to use modern debuggers in Debugging 102.

Once you have a mental map of the application, you can move onto identifying the issue.

### Identify the Issue

This step involves clearly defining the bug without ambiguity.

Describe the issue in terms of inputs and outputs. Given a set of input, what is the expected output? What is the actual output? How is this different from the design intent of the program, or rather, what the program is supposed to do? Answering these questions can help with narrowing the possible areas the bug could exist within the program.

With a clear definition of the problem, we can now attempt to reproduce the bug.

### Reproduce the Issue

Reproducing a bug the process of identifying a set of steps to follow in order to force the bug to occur repeatedly and predictably. When we create this set of steps, what we are really doing is coming up with a list of interactions between parts of our program that could be causing the bug. Programs can be huge, so if we can narrow down the possible location of the bug to a short list of steps, we have a lot less ground to cover.

The goal is to come up with the _shortest_ list of steps necessary to reproduce the bug. Minimizing the amount of steps to reproduce the bug minimizes the amount of systems that we have to check.

Another reason why we aim to create a list of steps to reproduce the bug is that we can use these same steps to verify whether the bug is fixed. If our project uses unit testing, we can even implement the steps to reproduce the bug as an automated test. We will discuss automated tests further in Debugging 103.

Once we can reliably reproduce the bug, we move onto the longest and most comprehensive part of debugging: diagnosing the cause.

### Diagnose the Cause: The Scientific Method of Debugging

The Scientific Method is a set of steps used by scientists in order to disprove or support a possible explanation for a set of observations. The Scientific Method cannot prove these explanations; it can only disprove them or provide unconfirming support. Just as scientists use the Scientific Method to learn more about the natural world, we will use a modified version of the Scientific Method to disprove or support theories for the possible cause of the bug.

The Scientific Method of Debugging has the following steps:

1. Take a guess at the cause of the bug.
2. Conduct an experiment to assess whether your guess is correct or not. This experiment should be controlled; only changing a single part of the program at a time.
3. See how the program responds to your change. If the results of your experiment contradict your guess for the cause, we return to step 1.
4. Often, a single experiment is not enough. Try conducting more experiments to strongly support your claim.
5. Once you have strong evidence for the cause of the bug, you can move on to attempting a fix.

#### Designing Good Experiments

Good experiments only make single changes to the system at a time. Our goal is to identify a single cause; if we change many different parts of the program at the same time, we have no idea which change produced the results to support or reject our guess.

Good experiments should not test theories already disproven. Keep a record of the experiments you have conducted. Some people can do this in their head, but if you can't, don't hesitate to write this list down in a place you can reference it.

Good experiments should produce results close to what you expect. If a change causes behavior that wildly deviates from the expected results, try undoing the changes before trying a new experiment.

### Fix It

Once you have undeniable evidence as to the cause of the bug, you can now go about fixing it. Ensure that you make fixes with purpose; your fix should exactly solve the problem, and should not introduce new bugs into the program. Once again, this requires a strong understanding of the program you are debugging.


### Reflect and Learn

Fixing the bug should not be the end of the story. Every bug comes with a cause. Most of the time, it is just an honest mistake, but sometimes, a bug can be indicative of a deeper problem with the program's overarching design, testing methodology, or your development process. Thinking about the underlying circumstances that caused the bug to exist can help give insights into how to refine the project's overall design and development processes, reducing the number of future bugs.


## Conclusion

Fixing bugs can be challenging, but the above methodology should equip you with a reliable means of identifying, testing for, and fixing bugs. These steps become very natural after a lot of practice. Ultimately, the only way real way to get better at debugging is by just doing a lot of debugging. 

So go out there and start exterminating some bugs!

## Acknowledgements

This article was inspired by instructional content from UCSD's CSE 15L course. Special thanks to the professors who developed that content!
