# Week 15: Thinking Functionally and Declaratively

## Streams and Higher-Order Functions

One of the goals of this class is that you be able to compare and contrast
programming paradigms, especially functional and object-oriented, which are
the two dominant paradigms in contemporary practice.
Recent years have seen a sort of convergence, with most ostensibly object-oriented 
languages providing more support for functional ideals than past languages.
The primary motivation for this&mdash;mentioned in the lecture you watched last
week&mdash;is that functional programs can make easier use of multicore and 
distributed environments. 

This week, we will aim toward the aforementioned goal by taking a closer look 
at how Java integrates functional programming concepts through
its [stream API](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/stream/package-summary.html), which was introduced in Java&nbsp;8.
This will build on the experience you had [last week](Week14.md).

A good first step is to read [Benjamin Winterberg's excellent Stream Tutorial](https://winterbe.com/posts/2014/07/31/java8-stream-tutorial-examples/). Take note of how he 
uses strategically placed `println` statements to aid in understanding the 
execution of his programs. 

Once you have a good head for what the stream system is all about,
you can exercise your understanding.
Fork [this repository](https://github.com/doctor-g/HigherOrderFunctionsAndStreams)
into your own GitHub account, clone that into IntelliJ IDEA, and review
the `README.md` file.
The repository contains a series of puzzles to solve using Java streams.
The puzzles are in roughly increasing order of complexity.
Note that the early puzzles correspond to some of the classic functional programming
transformations that you saw earlier in the semester and which appeared on the
midterm exam.

Your solutions must abide by the following rules:

- Make the test pass by assigning the result of a stream operation to the `actual` variable.
- In the spirit of pure functional programming, you may not include any other 
  stateful logic in your solutions.
- You may introduce helper methods if it yields a more &ldquo;Clean&rdquo; solution.

Submit your solution before the deadline by issuing a pull request to my repository.
As always, keep in mind our policies of academic integrity. Start early so you can
get help if you need it, and remember that it's better to be honestly wrong than dishonestly
anything.

## Logic Programming in Prolog

_And now for something completely different._

Watch the Prolog video tutorial that I have linked from Canvas.

Here is a clarification of some of the technical terminology used in the video:

- This is a _fact_: `dog(snoopy).`
- This is a _rule_: `animal(X) :- dog(X).`
- This is a _goal_: `?- likes(Person,Thing).`

Note that goals are conventionally prefixed with the &ldquo;`?-`&rdquo; notation, which
you can also find in the bottom-right of [SWISH](https://swish.swi-prolog.org/).

As you work through the following challenges, keep in mind that Prolog has been around
for decades, and some of these challenges draw upon "classic examples." 
That is to say, for many of these, you could readily find dozens of sample solutions
if you searched online. The goal of the exercises below is not _to find the solution_
but _to think through the problem_. You should be able to develop good, defensible
solutions to each of these challenges using only the resources I have shared,
and that's what you should do. As always, I am available to help.

### Translating between English and Prolog

For each of the following facts and rules, write an English sentence interpretation.

- `instrument(guitar).`
- `instrument(piano).`
- `plays(django_reinhardt, guitar).`
- `plays(art_tatum, piano).`
- `plays(lebron_james, basketball).`
- `musician(X) :- plays(X,Y), instrument(Y).`

Based on the facts and rules above, express the following goals as English-language questions.

- `?- musician(art_tatum).`
- `?- instrument(X).`
- `?- plays(X, basketball).`
- `?- plays(Who, What).`

Convert each of the following into valid Prolog facts or rules. (Test your solutions
in [SWISH](https://swish.swi-prolog.org/) to make sure they work together! 
There are multiple ways to turn English into Prolog, but not every way will work together
in a system.)

- Broccoli is a food.
- Broccoli is a vegetable.
- A hamburger is a sandwich.
- Sandwiches are food.
- Ace eats only hamburgers.
- Bob eats anything that is food.
- Carla eats food only if it is a vegetable.

Submit your translations on Canvas.

### Family Trees

Complete the family tree example shown as [example #2 on Sheila McIlraith's
Prolog examples
page](https://www.cs.toronto.edu/~sheila/384/w14/simple-prolog-examples.html).
Note that there are a total of nine relationships to express: mother, father,
sibling, sister, brother, aunt, uncle, grandparent, and cousin.

Incidentally, when I used to teach programming languages, we would spend a few
weeks on Prolog. Unlocking its full potential requires learning a few more
language features, such as list processing and arithmetic. This culminated in a
final project in which my students wrote programs to determine [the actual
relationship between Bilbo Baggins and his &ldquo;nephew&rdquo;
Frodo](http://tolkiengateway.net/wiki/Baggins_Family). If you have been enjoying
learning Prolog and want to dive just a little deeper, this might be a fun
challenge for you as well. Determining the exact relationship requires
researching a bit about how arithmetic works in Prolog so that you can compute
relationships like &ldquo;_n_-th cousin&rdquo; or &ldquo;_k_-times
removed.&rdquo;

Submit your solution as a single Prolog source file that contains the
original family tree data and your custom rules.

<hr>
<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/doctor-g/cs431">CS431 Course Plan</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://www.cs.bsu.edu/~pvgestwicki">Paul Gestwicki</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"></a></p>