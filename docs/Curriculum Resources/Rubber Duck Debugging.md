# Rubber Duck Debugging
## Staying Sane When Your Code Drives You towards Insanity
Debugging can be aggravating. If you have a bug that refuses to reveal itself, you might want to try consulting your expert rubber duck!

## Step 1: Reset
Frustration can lead us programmers to accidentally skip over small-but-important details of our code that are critical to bug identification. If you notice yourself becoming frustrated, you should first remove your hands from the keyboard. Then, take a deep breath.

## Step 2: Relax
Close your eyes and place your hands on your knees. Sit up straight, and take a deep breath. As you breathe in, take note of your feet.

As you breathe in again, slowly work your way up from your feet to your body. Acknowledge any tension and continue breathing. Do this again, working up from the body to the tips of your hands, and then to your head.

Repeat this several times as necessary.

Honestly, no one expects someone to be able to program for more than an hour straight without a brief break to mentally reset. Repeat until you feel ready to continue debugging.

## Step 3: Consult Your Rubber Duck
You are now in a headspace that is conducive to problem solving! Let’s get the problem solved by consulting your good friend, the Rubber Duck!

![Duck](duck.jpg){align=left style="height:20%;width:20%"}It might seem silly, but **explaining how your code works verbally allows you to see the bigger picture and not accidentally ignore certain details.** Many programmers at big tech companies have a rubber duck. Plus, your rubber duck is your friend, and DEEPLY INTERESTED in what your code does. Just look into those eyes…

Look at your program and identify the highest point in the stack trace. Then, look at the rubber duck, and begin to explain how the code works out loud.

Your duck is especially interested in these questions:

1. What are the values of important variables when we reach this code?
2. What code runs before this code?
3. How does this code function, line-by-line? Don’t skip anything!
    4. [A debugger breakpoint and stepthrough might be useful here!](../Engineering/Debugging/Debugging 102.md)
5. What other objects does this code interact with?

If you still have trouble, try doing the same process with a friend. If the friend asks questions, be sure to answer them in detail. 