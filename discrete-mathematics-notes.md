# Discrete Mathematics Notes #

## Introduction ##
These notes will be organized around 5 types of thinking:
 - logical
 - relational
 - recursive
 - quantitative
 - analytical

## Logical Thinking ##
Throughout these notes the word _formal_ will be used to 
describe a process that relies on manipulating notation
(as opposed to meaning 'rigorous').

### Connectives & Propositions ###
A _statement_ (also known as a proposition) is a 
declarative sentence that is either true or false, but
not both.
 - 7 is odd
 - 1 + 1 = 4
 - If it is raining, then the ground is wet
 - Our professor is from Mars

A declarative sentence fails to be a statement if it 
contains an unspecified term:
 - x is even
In this case x is a _free variable_. A second instance
in which a declarative sentence fails to be a statement
is when it is self-referential:
 - This sentence is false

There are five _logical connectives_ that can be used
to join statements to form more complex statements:

![Table of connectives & their symbols](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/tab_1_1.jpg "Optional title")

If _p_ is the statement "you are wearing shoes" and _q_
is the statement "then you can't cut your toenails":

  _P_ -> _q_

### Truth Tables ###
The precise meaning of each of the aforementioned 
connectives can be defined using tables that list the
True/False values for every possible case.

The _not_ connective, -|:

![Not connective truth table](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/5_1.jpg "Optional title")

The _and_ connective, ^, and the _or_ connective, v:

![And and Or connective truth tables](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/5_2.jpg "Optional title")

The _if and only if_ (sometimes known as 'iff') 
connective, <->:

![Iff connective truth table](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/5_3.jpg "Optional title")

The _implies_ connective: ->:

![Implies connective truth table](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/5_4.jpg "Optional title")

### Logical Equivalences ###
Two statements are _logically equivalent_ if they have
the same T/F values for all cases - they have the same
truth tables. For example, the theorem:

_p_ -> _q_

is logically equivalent to the theorem:

¬_q_ → ¬_p_

as proven by the below truth table:

![logical equivalence truth table](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/7_1.jpg "Optional title")

The statement ¬q → ¬p is called the _contrapositive_ of 
_p_ → _q_, and the statement _q_ → _p_ is called the
_converse_. For any statement _s_, the contrapositive
of _s_ is logically equivalent to _s_, while the converse
might not be.

Example:
If Aaron is late then Bill is late, and, if both Aaron and
Bill are late, then class is boring. Suppose that class
is not boring. What can you conclude about Aaron?

_Solution:_ 

_p_ = "Aaron is late"

_q_ = "Bill is late"

_r_ = "Class is boring"

Let _S_ be the statement "If Aaron is late then Bill is late, 
and, if both Aaron and Bill are late, then class is 
boring." _S_ translates to:

_S_ = ( _p_ → _q_ ) ^ [ ( _p_ ^ _q_ ) → r ]

Now the truth table, constructed by building truth tables
for the different statements within _S_, starting inside
the parentheses and working out way out:

![Statement truth table](https://www.safaribooksonline.com/library/view/essentials-of-discrete/9781449604424/images/9_1.jpg "Optional title")

