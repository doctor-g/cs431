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

## Object-Orientation and Dependency Inversion

Many people talk about object-orientation as being defined by inheritance,
polymorphism, and encapsulation. You may have seen 
[this other presentation by Robert Martin](https://www.youtube.com/watch?v=t86v3N4OshQ) 
in which he talks
about how only polymorphism is really characteristic to object-oriented
programming&mdash;a point he makes in passing during the ACCU keynote.
He is very practical in his approach, not getting into language-theoretic issues of 
polymorphism but focusing on what it _does_ for us as software developers.
In particular, he talks about how polymorphism allows us to invert
dependencies... but what does this mean?

When you studied object-oriented programming in CS222, you should have come
across [the SOLID principles](https://en.wikipedia.org/wiki/SOLID):

- Single-Responsible Principle
- Open-Closed Principle
- Liskov substitution principle
- Interface segregation principle
- Dependency inversion principle

There is rarely time in that course to go deeply into each of these, and so
we usually focus on the first. However, it is worth being familiar with all
of them. In this exercise, you are going to learn more about the last one,
which can be difficult to understand unless you see it in action.

To get our hands dirty with dependency inversion,
we will be using [Guice](https://github.com/google/guice). Read [the Motivation
page](https://github.com/google/guice/wiki/Motivation). Make sure you understand
everything that is being described here: it builds upon what you have already
learned in CS222. If you need a refresher on Java, 
[The Java Tutorials](https://docs.oracle.com/javase/tutorial/) are the best reference
despite being dated; I would follow 
[the Learning the Java Language trail](https://docs.oracle.com/javase/tutorial/java/index.html)
if you need reminders about classes and interfaces.

The [Getting Started](https://github.com/google/guice/wiki/GettingStarted) page
demonstrates how Guice can be used to invert dependencies.
Within this page, you will see a reference to a _DSL_ or _Domain-Specific Language_, which came
up in Robert Martin's video. 
Read [Martin Fowler's overview of DSL](https://martinfowler.com/bliki/DomainSpecificLanguage.html),
note that the one presented in Guava is an _Internal DSL_,
and follow up by reading 
[Martin Fowler's definition of a FluentInterface](https://martinfowler.com/bliki/FluentInterface.html), 
which is another term for the same idea.
What Fowler describes as being used in JMock is common in many contemporary unit testing
frameworks, including [Mocha for Javascript](https://mochajs.org/) and 
[the `flutter_test` framework in dart](https://flutter.dev/docs/cookbook/testing/unit/introduction).
Once you have worked through these readings, 
you will see that, contrary to the Getting Started page, 
`DemoModule` does not actually use the DSL; it only uses the binding annotations.

[Guice's Mental Model documentation](https://github.com/google/guice/wiki/MentalModel)
is the final part of the required reading.
It will help you get an idea of what Guice is doing without having to get into
the implementation details.
This page more clearly presents the internal DSL, 
which is the alternative to the binding annotations.
Remember, this is an _internal DSL_, because it is written in Java. 

Download and install [the community edition of IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
if you do not already have it. 
You will also need JDK15, which can be downloaded from within IDEA.
Clone [my Wikipedia Revisions Reporter repository](https://github.com/doctor-g/WikipediaRevisionsReporter)
and open it within IDEA. (You can do this in one step by telling IDEA to create
 a new project from version control.)
Make sure that you can run the application and its unit tests following the
instructions in the `README.md` file.
This will set you up to complete the challenges below.

It is recommended to complete the following challenges in order and commit to
your local repository at the end of each. Remember to maintain the integrity of
the project by following the rules of 
[Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
as you learned in CS222.

## Challenge #1

The default application configuration uses `FakeQueryEngine` to simulate a slow
network request. This allows the UI to be developed regardless of whether the
backend is working, and it prevents the application from unnecessarily hitting
Wikipedia's servers.

Guice is used to configure which `QueryEngine` is used. Change the
configuration so that the application uses the real `WikipediaQueryEngine`
instead. Note that you should be able to do this by only modifying Guice
configuration: no changes should be made outside of module configuration.

## Challenge #2

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

## Challenge #3

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

## Wrapping Up

Add a file to the project called `ProjectReport.md`. Address the following 
prompts as part of your report:

- Write a paragraph comparing and contrasting the iterative and functional  
  approaches to string concatenation you explored in challenge #3. Which do you
  prefer, and why? (If you were unsuccessful at Challenge #3, write a reflection
  on that experience instead. What went wrong? Where did you get stuck, and
  when?)

- Describe how polymorphism allowed dependency inversion in this little
  application. Be clear and precise here, as this is, in part, an assessment of
  your correct use of technical terminology.
  Consider, for example, where exactly is polymorphism used?
  Where exactly is a dependency inverted?

Export your project by using `File→Project to Zip file` and submit it
via [Canvas](https://bsu.instructure.com).

