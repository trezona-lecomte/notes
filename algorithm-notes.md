##Floyd's cycle-finding algorithm

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

> Written with [StackEdit](https://stackedit.io/).