Watch [Robert Martin's ACCU 2011 keynote presentation, &ldquo;The Last
Programming Language&rdquo;](https://www.youtube.com/watch?v=P2yr-3F6PQo).
(Take Notes. Ask questions. Turn in both.)

We will be using [Guice](https://github.com/google/guice). Read [the Motivation
page](https://github.com/google/guice/wiki/Motivation). Make sure you understand
everything that is being described here: it builds upon what you have already
learned in CS222, which is a prerequisite for this course. Remember that if you
need a refresher on Java, 
[The Java Tutorials](https://docs.oracle.com/javase/tutorial/) are the best reference
despite being dated; I would follow 
[the Learning the Java Language trail](https://docs.oracle.com/javase/tutorial/java/index.html)
if you need reminders about classes and interfaces.

The [Getting Started](https://github.com/google/guice/wiki/GettingStarted) page shows a complete demo.
Note that within this page, you see a reference to a _DSL_ or _Domain-Specific Language_, which came
up in Robert Martin's video.
Read [Martin Fowler's overview of DSL](https://martinfowler.com/bliki/DomainSpecificLanguage.html),
note that the one presented in Guava is an Internal DSL,
and follow up by reading [Martin Fowler's definition of a FluentInterface](https://martinfowler.com/bliki/FluentInterface.html), which is another term for the same idea.
The internal DSL approach Fowler describes having been taken for JMock is common in contemporary unit testing
frameworks such as [Mocha for Javascript](https://mochajs.org/) and 
[the `flutter_test` framework in dart](https://flutter.dev/docs/cookbook/testing/unit/introduction).
Once you have understood these sources, 
you will see that, contrary to the Getting Started page, 
`DemoModule` does not actually use the DSL; it only uses the binding annotations.

[Guice's Mental Model documentation](https://github.com/google/guice/wiki/MentalModel)
is the final part of the required reading.
Note again here that there examples of the DSL, which are an alternative to binding annotation.
Specifically, this is an _internal DSL_, because it is written in Java. 

Download and install [the community edition of IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
if you do not have it. You will also need JDK15, which can be downloaded from within IDEA.
Clone [my Wikipedia Revisions Reporter repository](https://github.com/doctor-g/WikipediaRevisionsReporter)
and open it within IDEA. Make sure that you can run the application and its unit tests following the
instructions in the `README.md` file.
This will set you up to complete the following challenges.

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

Which `QueryEngine` is used has been configured with Guice. Change the
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

In addition to the change in the code, write a paragraph in the `README.md` file
comparing and contrasting the two approaches. Which approach do you think is
preferable, and why? 

## Wrapping Up

Export your project by using `File&rightarrow;Project to Zip file` and submit it
via [Canvas](https://bsu.instructure.com).

