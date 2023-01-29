# Algorithmic Techniques for Reducing Time Complexity(TC) of a python code.

In order to reduce time complexity of a code, it's very much necessary to reduce the usage of loops whenever and wherever possible.

I'll divide your code's logic part into 5 sections and suggest optimization in each one of them.


<br><hr>
## Section 1 - Declaration of Variables and taking input

```python
number = int(input())
factors = []
perfectSquares = []
count = 0
total_len = 0
```

You can easily omit declaration of perfect squares, count and total_length, as they aren't needed, as explained further. This will reduce both Time and Space complexities of your code.

Also, you can use Fast IO, in order to speed up INPUTS and OUTPUTS This is done by using 'stdin.readline', and 'stdout.write'.


<br><hr>
## Section 2 - Finding All factors

```python
for i in range(1, number):
    if number%i == 0:
        factors.append(i)
```

Here, you can use List comprehension technique to create the factor list, due to the fact that List comprehension is faster than looping statements.
    
Also, you can just iterate till square root of the Number, instead of looping till number itself, thereby reducing time complexity exponentially. Above code section guns down to...

### *After applying '1' hack*

factors = [for i in range(1, number) if number%i == 0]

### *After applying '2' hack - Use from_iterable to store more than 1 value in each iteration in list comprehension*

```python
factors = list( chain.from_iterable(
  (i, int(number/i)) for i in range(2, int(number**0.5)+1)
    if number%i == 0
  ))
```


<br><hr>
## Section 3 - Eliminating Perfect Squares

```python
# Find total number of factors        
total_len = len(factors)

for items in factors:
    for i in range(1,total_len):
  # Eleminate perfect square numbers
    if items == i * i:
        if items == 1:
            factors.remove(items)
            count += 1
        else:
            perfectSquares.append(items)
            factors.remove(items)
            count += 1
```

Actually you can completely omit this part, and just add additional condition to the Section 2, namely ... type(i**0.5) != int, to eliminate those numbers which have integer square roots, hence being perfect squares themselves. Implement as follows....

```python
factors = list( chain.from_iterable(
  (i, int(number/i)) for i in range(2, int(number**0.5)+1)
    if number%i == 0 and type(i**0.5) != int
  ))
```


<br><hr>
## Section 4 - I think this Section isn't needed because Square Free Numbers doesn't have such Restriction

<br><hr>
## Section 5 - Finalizing Count, Printing Count

There's absolutely no need of counter, you can just compute length of factors list, and use it as Count.
### OPTIMISED CODES

### Way 1 - Little Faster

number = int(input())

```python
# Find Factors of the given number
factors = []
for i in range(2, int(number**0.5)+1):
    if number%i == 0 and type(i**0.5) != int:
        factors.extend([i, int(number/i)])

print([1] + factors)
```

### Way 2 - Optimal Programming - Very Fast

```python
from itertools import chain 
from sys import stdin, stdout

number = int(stdin.readline())
factors = list( chain.from_iterable(
  (i, int(number/i)) for i in range(2, int(number**0.5)+1)
    if number%i == 0 and type(i**0.5) != int
  ))

stdout.write(', '.join(map(str, [1] + factors)))
```

<br><hr>
> Original source: [Redirect -> Stackoverflow](https://stackoverflow.com/questions/51772888/how-can-i-reduce-the-time-complexity-of-the-given-python-code)
