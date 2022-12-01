# Basics

To loop, simply use the `for` command, along with a value to use for looping through a list.
The syntax is: `for _____ in _____:`

> Note that anything that is indented after the `for` statement is considered **inside the loop**. Anything inside the loop is executed once per list item.

```py
tests = ['test1', 'test2', 'test3', 'test4']

for test in tests:
    print(f"Printing test iteration: {test}")
print("\n")
```

# Importance of Indentation
In the above example, the un-indented newline `\n` causes the interpreter to insert a blank line after each pass through the loop,

Any code that occurs **un-indented**, after the `for` statemenet, is considered **outside of the loop**.

**Common loop errors include:**
- forgetting to indent code (that was intended to be ran through the loop)
- forgetting to indent additional lines (that were intended to be ran through the loop)
- indenting unnecessarily (non-loop related commands)
- indenting unnecessarily after the loop
- forgetting the colon `:`

# Making Numerical Lists

## range() function
- Python's `range()` function makes it easy to generate a series of numbers
- Below, you can see 
```py
for value in range(1, 5):
	print(value)
1
2
3
4
```

Interestingly, when using `range()`, Python starts at the first number and stops when it reaches the second number, thus never getting to the `print(value)` command for 5th iteration of the loop. 

Also note that you may pass just (1) argumene to `range()`, and Python will start the sequence at 0; for example: `range(6)` would supply numbers 0 through 5.

### Example 1: Even numbers
You can also use `range()` to tell Python to skip numbers. The 3rd parameter passed to `range()` indicates the "step size" for which Python increments:
```py
even_numbers = list(range(2, 11, 2))
print(even_numbers)
[2, 4, 6, 8, 10]
```

## Examples
### Squared numbers
- Note that 2 asterisks `**` represent exponents
```py
# METHOD 1 - use a variable to temporarily hold each squared value
squared = []
for value in range(1, 11):
	square = value ** 2
	squares.append(square)
print(squares)
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# METHOD 2 - calculate each squared value directly within the append() method
squared = []
for value in range(1, 11):
	squares.append(value ** 2)
print(squares)
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

### Helpful Functions
```py
digits = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
min(digits)
0

max(digits)
9

sum(digits)
45
```

## List Comprehensions
- Can generate lists using less lines compared to the squared for loop examples
- Below generates the same squared values from the earlier example:
```py
squares = [value**2 for value in range (1, 11)]
print(squares)
```

Below is an example of my pseudocode to help understand the concept:
```py
my_list = [ITEM_EXPRESSION for ITEM_VALUE in ITERABLE]
```

Excerpt from book: 
>To use this syntax, begin with a descriptive name for the list, such as `squares`. Next, open a set of square brackets and define the expression for the values you want to store in the new list. In this example the expression is `value**2`, which raises the value to the second power. Then, write a `for` loop to generate the numbers you want to feed into the expression, and close the square brackets. The `for` loop in this example is `for value in range(1, 11)`, which feeds the values 1 through 10 into the expression `value**2`. Note that no colon is used at the end of the `for` statement.