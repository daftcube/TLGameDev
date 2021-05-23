# Interface Activity

The following is a lesson plan outline for teaching the design side of interfaces.

# Interfaces, Implementations, Oh My: Writing More Flexible Code Through Programming to Interfaces

The purpose of this activity is to try to improve one’s ability to use the principles of object-oriented programming (in this case, specifically with interfaces) to design programs that are easy to change and extend in the future. Such design skills are highly coveted among tech companies, and often are the deciding factor in making new hires and senior promotions.

The activity will not involve any code. Instead, students will be given a program specification of an e-commerce payment processing application and asked to draw out what the program would look like from a design standpoint. Students will be organized into groups and will be given time to come up with a first iteration of their program design.

Five minutes into the activity, the instructor will stop discussion and announce that the program specification has been modified. The specification now requires that the program can handle three different types of payment method. The instructor will then resume group work.

Students will scramble to modify their current designs. Students will likely encounter several issues with modifying their current designs:

1. Programming to an Implementation: Programming to an implementation is writing concrete code in a project. In object-oriented projects, it is better design to define an interface and then program to that interface; this allows
2. Coupling: Modules that are highly dependent on one another are called ‘coupled.’ Coupled code is hard to change and maintain because there is no guarantee that a change to one part of the program will not cause unintended changes in behavior to another part of the application. Following the “separation of concerns” principle is paramount in large projects.

Five minutes later, the instructor will stop discussion again and announce that the program specification has been changed to now include the requirement of processing sales tax in certain states in addition to all of the other features.

At the end of this section of the activity, the instructor will lead a guided discussion surrounding the challenges of designing an application with rapidly changing and expanding requirements. The discussion should be oriented towards identifying poor design and its consequences while providing a motivation for learning how to design interface-oriented applications.

The instructor will then give a short presentation on programming to interfaces.

After the instructor’s presentation, the class will attempt the activity again. The specification changes will be different, but they will happen at the same time intervals. Using the principles of programming to an interface, students should be able to create more modular design that can easily allow for large parts to be changed, removed, or swapped.

The activity will end with another group discussion about how the design approach shifted when considering the idea of programming to an interface instead of an implementation. The key questions to discuss should be:

How did this round of design compare to the previous round of design?
Why did interfaces make it easier to adjust to changing requirements?
How might this look when actually writing code?
What disadvantages might interfaces bring, and how would they be mitigated?