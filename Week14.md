# Week 14: The Semantic Classes, Focusing on Object-Orientation and Dependency Inversion

One of the major topics of this class is the comparison of different _paradigms_
of programming languages. This week, we will review the differences between paradigms
and then focus on an aspect of particular importance: the power of polymorphism 
to invert dependencies in object-oriented programming.

## A Brief History of Programming Languages

Watch [Robert Martin's ACCU 2011 keynote presentation, &ldquo;The Last Programming Language&rdquo;](https://www.youtube.com/watch?v=P2yr-3F6PQo).

Treat this like the high-quality lecture it is. Take notes. Record questions.
Identify things you don't know that you want to learn about. After watching the
presentation, complete the corresponding assignment on Canvas. This assignment
will require you to read your notes, reflect on them, and share some of your
findings.

## Structured Programming and Unconstrained GOTO

The odds are slim that anyone has taught you how to use the &ldquo;goto&rdquo;
statements that Robert Martin mentioned in his presentation.
Before the structured programming revolution, many languages had such 
statements to allow for jumping around source code. Their use has been
discouraged for years, although they still exist in some modern languages,
including C and C++. 

Look at [this brief TutorialsPoint example](https://www.tutorialspoint.com/cprogramming/c_goto_statement.htm)
to see how `goto` works. If you think back to what you learned in CS230,
you should recognize what's happening here: `goto` is essentially
a &ldquo;jump&rdquo; instruction in assembly language, exposed
in a high-level programming language. 
You should remember that method calls are implemented as jumps in
machine code, but their semantics are carefully constrained.
When you call a method, and it returns, you come back to where you started,
for example.
Not so with `goto`, which in the general case allows you to jump
anywhere in a program. (That's how it worked when I first learned to program
in BASIC on the Commodore&nbsp;64!)

With a little imagination, I think you can consider how this powerful little
language feature can very quickly lead to a complete mess.
I believe there is a relationship here between `goto` and the structure
of Blueprint visual programming in Unreal Engine 4. 
[The official documentation for Blueprint](https://docs.unrealengine.com/en-US/ProgrammingAndScripting/Blueprints/index.html)
demonstrates clean layouts and good practices, but the trenches are filled
with stories of [Blueprints From Hell](https://blueprintsfromhell.tumblr.com/).
This is analogous to what happens if you start messing with `goto`:
one little shortcut, one little kludge, and you start down a devastating 
slippery slope.

The community has pretty well decided that we would rather do without
`goto`, so let's turn to look at one of the most popular paradigms
and the benefits gained by the constraints it offers.

## Object-Orientation, Polymorphism, and Dependency Inversion

Many people talk about object-orientation as being defined by inheritance,
polymorphism, and encapsulation. I will assume you have a good
working understanding of those three terms, so take a moment to review
them if you are unsure. They provide a definition of object-orientation that
is appropriate for CS121, but we can do better!

### Principles of Object-Oriented Programming

You may have seen 
[this other presentation by Robert Martin](https://www.youtube.com/watch?v=t86v3N4OshQ), 
which I regularly assign in CS222.
In this talk, he makes the case that of those three properties described above,
only polymorphism is characteristic to object-oriented
programming.
Martin is very practical in his approach, not getting into language-theoretic issues of 
polymorphism but focusing on what it _does_ for us as software developers.
In particular, he talks about how polymorphism allows us to invert
dependencies... but what exactly does this mean? 

When you studied object-oriented programming in CS222, you should have come
across [the SOLID principles](https://en.wikipedia.org/wiki/SOLID):

- Single-Responsible Principle
- Open-Closed Principle
- Liskov substitution principle
- Interface segregation principle
- Dependency inversion principle

Take a moment now to review these.
There is rarely time in CS222 to go deeply into each principle, and
we usually focus on the first. However, it is worth being familiar with all
of them. In this exercise, you are going to learn more about the last one,
which can be difficult to understand unless you see it in action.
That is exactly what we will do by exploring _dependency injection_.

### Understanding Dependency Injection using Guice

We will be using
[Guice](https://github.com/google/guice). Read [the Motivation
page](https://github.com/google/guice/wiki/Motivation), which establishes
the case for dependency injection using examples that should be familiar
from CS222 or your SE coursework.
Keep in mind that if you need a refresher on Java, 
[The Java Tutorials](https://docs.oracle.com/javase/tutorial/) are the best reference
despite being dated; I would follow 
[the Learning the Java Language trail](https://docs.oracle.com/javase/tutorial/java/index.html)
if you need reminders about classes and interfaces in particular.

Read the [Getting Started](https://github.com/google/guice/wiki/GettingStarted)
page for a demonstration of dependency injection using Guice. Within this page,
you will see a reference to a _DSL_ or _Domain-Specific Language_&mdash;a topic
which came up in Robert Martin's video. Read [Martin Fowler's overview of
DSL](https://martinfowler.com/bliki/DomainSpecificLanguage.html), note that the
DSL presented in Guice is an _Internal DSL_, and follow up by reading [Martin
Fowler's definition of a
FluentInterface](https://martinfowler.com/bliki/FluentInterface.html), which is
another term for the same idea. What Fowler describes as being used in JMock is
common in many contemporary unit testing frameworks, including [Mocha for
Javascript](https://mochajs.org/) and [the `flutter_test` framework in
dart](https://flutter.dev/docs/cookbook/testing/unit/introduction). Once you
have worked through these readings, you may notice that, contrary to the Getting
Started page, `DemoModule` does not actually use the DSL; it only uses the
binding annotations. Don't worry, it comes up again soon.

[Guice's Mental Model documentation](https://github.com/google/guice/wiki/MentalModel)
is the final part of the required reading.
It will help you get an idea of what Guice is doing without having to get into
the implementation details.
This page more clearly presents the internal DSL, 
which is the alternative to the binding annotations.
Remember, this is an _internal DSL_, because it is written in Java. 

### Starter Project Configuration

Download and install [the community edition of IntelliJ
IDEA](https://www.jetbrains.com/idea/download/) if you do not already have it.
You will also need JDK15, which can be downloaded from within IDEA. IntelliJ
IDEA has recently changed their default interface to git, so if you haven't used
it in a while&mdash;or you are new to [Gradle](https://gradle.org/)&mdash;you
may want to [review this video](https://youtu.be/_XjTyQpmzUk).
You will not need to follow all of these steps shown in the video, but it
demonstrates how to get around IDEA and describes what to expect from it.

Log in to GitHub and fork
[my Wikipedia Revisions Reporter repository](https://github.com/doctor-g/WikipediaRevisionsReporter).
Do this by clicking the &ldquo;Fork&rdquo; button in the upper right
of the browser. This will make a copy of the project in your 
GitHub account. (I assume at this point you all have GitHub accounts; if you
do not, then of course, you will have to make an account first.)

Clone _your copy_ (not the one in my repository!) of the project into IntelliJ IDEA.
You can do this in one step by telling IDEA to create
 a new project from version control.
Make sure that you can run the application and its unit tests following the
instructions in the `README.md` file.
This will set you up to complete the challenges below.

It is recommended to complete the following challenges in order and commit to
your local repository at the end of each. Remember to maintain the integrity of
the project by following the rules of 
[Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
as you learned in CS222.

### Challenge #1

The default application configuration uses `FakeQueryEngine` to simulate a slow
network request. This allows the UI to be developed regardless of whether the
backend is working, and it prevents the application from unnecessarily hitting
Wikipedia's servers.

Guice is used to configure which `QueryEngine` is used. Change the
configuration so that the application uses the real `WikipediaQueryEngine`
instead. Note that you should be able to do this by only modifying Guice
configuration: no changes should be made outside of module configuration.

### Challenge #2

The default presentation of results is not very attractive, particularly the
timestamp formatting. Also, the dependency on `RevisionFormatter` follows the
flow of execution. Create a new, alternative `Revision` formatter that presents
the revision information in a more user-friendly way. Incorporate it into the
application in such a way that the dependency opposes the flow of execution. You
can do this by introducing a new interface that is implemented by all
formatters, creating a module that injects the correct dependency at runtime,
and adding that module to the Guice injector.

Earn a [No-Prize](https://en.wikipedia.org/wiki/Marvel_No-Prize) by using TDD to
develop your new formatter!

### Challenge #3

In `WikipediaAnalyzer`, you will find an iterative approach to combining strings:
```
StringBuilder stringBuilder = new StringBuilder();
for (Revision revision : response.revisions()) {
    String message = formatter.format(revision);
    stringBuilder.append(message);
    stringBuilder.append("\n");
}
```
Replace this implementation with a functional approach using Java streams.
That is, rather than use a `for` loop to iterate through the revisions,
call `stream()` on the list and use higher-order functions and method chaining
to accomplish the same goal in a single line. 

This challenge should only change `WikipediaAnalyzer` and no other class.

_Hint:_ Java provides an API for defining or using standard &ldquo;collectors,&rdquo;
which may be useful.
Review the common functional programming utilities that you used
in the first half of the semester to puzzle through the data transformations
you desire.

### Wrapping Up

Complete the project report that you can find as `ProjectReport.md` in your
repository. This includes documenting your solutions (or attempts) to the
three challenges as well as addressing two reflection questions.

Once you are satisfied with your submission, make sure you have committed and
pushed all your changes to your repository. Then, through GitHub's web
interface, open a pull request to my repository. I will evaluate your work via
the pull request and enter my evaluation on Canvas.

Note that the pull requests of your peers will be visible through the Web interface.
As always, fight any temptation to dishonestly review others' work, as this
would certainly violate the university's standards for academic integrity.
My hope would be that this point would be unnecessary, but I include this just
to be sure that there are no miscommunications of expectation, since we only
just started working together.
