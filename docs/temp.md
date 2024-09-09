gets re evaluated every time its called
meaning every time that it appears
in the call expression
so let's switch back to slides and just review
what we've seen
so far
we're interested in expressions and how they evaluate
to values the primitive expressions we've seen so far
are the number or numeral
a name and a string
strings I showed you last time
they represent text
we'll talk about them later in the course
call expressions look like this
they have an operator some parentheses
and then separated by commas some operands
we just saw that you can have no operands at all
and still have a valid call expression
you can also have nested call expressions
and operand can also be a call expression
we're really interested now in how names work
so let's go through a tricky case
and see if you can figure out what happens
what is the value of the final expression
in the following sequence
f equals min f equals max
g come a h equals min come a max
then max equals g
then I compute the max of f of
g of h of one and five
g is also applied to three
and max is also applied to four
think about it for a while
the answer is either 1 2 3 4 or five
you should pause the video now and try to work out
what the real answer is
next we'll talk about environment diagrams
so environment diagrams are a way
for us
to keep track of what's going on
within the python interpreter
when it executes a program that we typed in
and myermans are real things
so they are the way in which
an interpreter for programming language
keeps track of what names mean
so it's sort of memory
that
keeps track of the bindings between names and values
so we're going to draw pictures of what they look like
and
this will help you become a better computer scientist
lots of what computer scientists do is drop pictures
that involve boxes and arrows pointing to other boxes
it's just a huge part of the discipline
so you might as well start now
okay so an environment diagram
is there to visualize the interpreters process
so that we can really
understand how programs get executed
and they look like this
so you have some code on the left
and then you have some frames on the right
and the code is just regular python code
with some arrows to indicate where we are
in the process of execution
and the frames keep track of the bindings
between names and values
okay
so the codes on the left the frames are on the right
within the code there are statements and expressions
so we see an import statement
and an assignment statement here
the arrows indicate the evaluation order
so the gray one says this was just executed
and the red one says this is next to execute
it hasn't happened yet
okay frames on the right
show bindings between names
pi is a name and values
if there's a name there is a value
within a frame
this is usually important
this is part of the python process
within a frame a name cannot be repeated
it has to be bound to at most one value
when we saw the consequences of this
when we rebounded the name max to our new number
instead of the original function
the old binding was lost
okay so those are code on the left frames on the right
and environment diagram
these are going to get more complicated
but also more necessary
because when there are lots of names
repeated in various ways
we'll need to be able to keep
track of what they really meet
these things get drawn for you automatically
so here's the web interface
what's called the online python tutor
so
here's the code that we type in from math and port pie
you can edit this
and then you click visualize execution
and you get your coat on your left
and your frames on the right
and as you walk through
each line of code by pressing forward
you see the consequences of executing
first as import statement bound the name pi
to its value and the next thing that happened
is that the assignment statement
found the name towel to two times pi
and here's the result at the end of the day
so when you're confused about what a program does
paste it in to the online python tutor
and it will show you exactly what happens
throughout the course of execution
that's the whole point
okay so that's what an environment diagram looks like
now we can talk about
exactly what assignment statements do
they change the bindings between names and values
and frames
so here is
here is an environment diagram
for three lines of code
just executed with b equals two
next to execute
is this larger assignment statement
that has two names on the left
and two expressions on the right
now
there is an execution rule for assignment statements
that you need to understand
because python always does the same thing
over and over again
and here's what it does for assignment statements
it evaluates all of the expressions
to the right of equals
from left to right
then after evaluating all those expressions
it binds all the names to the left of equals
to the resulting values
so in this case
here are all the expressions to the right of equals
we get a plus b which evaluates two
one plus two is three
so this evaluates to three
b evaluates to two
and then 2nd step
find all names to the left of equals
to the resulting values
so b will be bound to three
and a will be bound to two
the value of that expression
okay so if we hit forward
in the environment diagram generator
the jest excuted arrow will now be online three
and the global frame will have
a bound to two and b bound to three
okay so now we can do the complicated case
that I ask you to solve by ourselves
let's just do it
live in the python tutor
okay so here was the question
what happens if I say f equals min then f equals max
then gh equals min max
and max equals g
then this large
nested call expression
well let's watch and see what happens
so the first thing that happens that f is bound to min
this is the min function
representation in the environment diagram
that's similar to
the angled bracket thing that you sell
when python printed it out
then we bind f to max
now remember the rule
that a name can be bound to at most one value
in a frame so
since we've rebound f to max
we've lost the binding between f and min
that's just gone
okay now we say g and h are bound to min and max
so we evaluate min as the min function
we evaluate max that's the max function
and we bind g and h to min and max
notice there's only one min function
there's only one max function
but the max function now has two names fnh
the min function has the name g
now there's also the name max
for the max function and the name
min for the min function
those are built in and they're part of the global frame
but we don't write them down
because if we had to write down all the built in names
then that would take up too much space
so we only write them down when they change
which is about to be what happens
so when next time max equals g
using the execution rule for assignment statements
we first evaluate g
g evaluates to the min function
then we bind the name max to that value
so now max means mid
cheapers that is complicated isn't
okay
so then we say max ff two of g of h of one and five
three and four
and that involves evaluating
all of these different operand expressions in turn
before I head forward let's just watch how that goes
so we can draw an expression tree
that evaluates the operator and operands
of the call expressions and the operand