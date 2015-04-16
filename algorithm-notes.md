# Data Structures & Algorithms #

## P & NP ##
P: Polynomial Tim
NP: Non-deterministic Polynomial Time
To understand the difference, consider the Subset Sum problem:

Given a set of numbers, is there a subset that adds up to 0?
 	{ -10, 60, 95, 25, -70, 55 }
	-10 + 25 -70 +55 = 0
This would be much harder if the set contains a larger number of elements. One deterministic solution would be to calculate all of the possible subsets and check if they = 0. While this would work, unfortunately it is not 

## Random Number Generators ##

### Linear Congruential Generators ###
Example: Xn+1 = Xn*A+B (mod M)
A = 5
B = 3
M = 7
X0 = *0* (seed)
X1 = 0*5+3(mod 7) = 3(mod 7) = *3*
X2 = 3*5+3(mod 7) = 18(mod 7) = *4*
X3 = 4*5+3(mod 7) = 23(mod 7) = *2*
X4 = 2*5+3(mod 7) = 13(mod 7) = *6*
X5 = 6*5+3(mod 7) = 33(mod 7) = *5*
X6 = 5*5+3(mod 7) = 28(mod 7) = *0*
... now we begin to repeat.

Full Period:
 - B and M must be relatively prime (they share no common factors other than 1)
 - A - 1 must be divisible by allprime factors of M
 - A - 1 is a multiple of 4 if M is

Example that doesn't meet the Full Period criteria:
A = 4
B = 3
M = 8
X0 = *0* (seed)
X1 = 0*4+3(mod 8) = 3(mod 8) = *3*
X2 = 3*4+3(mod 8) = 15(mod 8) = *7*
X3 = 7*4+3(mod 8) = 31(mod 8) = *7*
.. now we're stuck in a loop.

LCGs have the advantage of being *fast*, but they're not very random & may not generate every random number. 

Multiplicative Congruential Generator (MCG)

# Floyd's cycle-finding algorithm

 - Pointer algorithm
 - Uses only 2 pointers
 - Each pointer moves through the sequence at different speeds

```
def floyd(f, x0):
	# Main phase of algorithm: finding a repetition x_i = x_2i
	# The hare moves twice as quickly as the tortoise and
	# the distance between them increases by 1 at each step.
	# Eventually they will both be inside the cycle and then,
	# at some point, the distance between them will be divisible
	# by the period λ.
	tortoise = f(x0) # f(x0) is the element/node next to x0.
	hare = f(f(x0))
	while tortoise != hare:
		tortoise = f(tortoise)
		hare = f(f(hare))
```
