# Integers
### standard operators
```py
2 + 3
5

3 - 2
1

2 * 3
6

3 / 2
1.5
```
### exponents
```py
3 ** 2
9

2 ** 3
27
```

### order of operations
```py
2 + 3*4
14

(2+3) * 4
20
```
Note that spacing has no effect on how Python evaluates the expressions.

# Floats
Python calls any number with a decimal point a **float**. This term is used in most programming languages, and it refers to the fact that a decimal point can appear at any position in a number.

```py
0.1 + 0.1
0.2

2 * 0.2
0.4
```

Ocasionally, due to how computers internally represent numbers, you may get odd decimal places in your python responses. This is normal.
```py
0.2 + 0.1
0.300000000004
```
# Integers & Floats
When you divide any two numbers, even if they are integers that result in a whole number, you’ll always get a float:
```py
4/2
2.0
```

Mixing integers and floats will always result in a float:
```py
1 + 2.0
3.0

3.0 ** 2
9.0
```
# Underscores
You can make code more readable by using underscores:
```py
universe_age = 14_000_000_000
```

This is only for code readability. Output will still display without the underlines:
```py
print(universe_age)
14000000000
```

# Multiple Assignment
You can set multiple variables in just a single line of code:
```py
x, y, z = 0, 0, 0
```
This will work as long as the number of values matches the number of variables.
# Constants
A **constant** is a variable whose value stays the same throughout the life of a program. Python has no built-in constant type, ==so programmers usually represent these with all caps==:
```py
MAX_CONNECTIONS = 5000
```