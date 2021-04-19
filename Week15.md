# Week 15: Title Pending

## Logic Programming in Prolog

Watch the video tutorial to Prolog that I have linked from Canvas.

I want to briefly clarify some of the technical terminology that I used in the
video.

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

### Thinking in Prolog

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
challenge for you as well.

<hr>
<p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/doctor-g/cs431">CS431 Course Plan</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://www.cs.bsu.edu/~pvgestwicki">Paul Gestwicki</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"></a></p>