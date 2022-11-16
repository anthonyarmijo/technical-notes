# Basics

- Lists are a collection of items in a particular order
- Square brackets indicate a list: `[item1, item2, item3]`
- You can print a list very simply:
```py
bicycles = ['trek', 'cannondale', 'redline', 'specialized']
print(bicycles)
```

## Access individual items
- Simply append the item ==index== value after your variable
- Note that index numbers start at 0
```py
print(bicycles[0])
trek
```


```py
# Python has a special syntax for accessing the last element in a list;
# that is using index number `-1`.
print(bicycles[-1])
specialized
```

> `-2` would return the second to last item in a list.



# Editing Lists
## Modify list
Simply set the variable (with its index) to the new value:
```py
motorcycles = ['honda', 'yamaha', 'suzuki']
print(motorcycles)

motorcycles[0] = 'ducati'
```

## Add list items

- Use the `append()` method to add items to the end of the list.
```py
motorcycles = []
motorcycles.append('honda')
motorcycles.append('yamaha')
motorcycles.append('suzuki')
```

- Using the `insert()` method, you can insert items at any location using index number. 
```py
motorcycles = ['honda', 'yamaha', 'suzuki']

motorcycles.insert(0, 'ducati')
# this adds 'ducati' to the first position in front of 'honda' and shifts everything right.
```

## Delete list items
### del statement
Rather than using a method, you can use the `del` statement to remove items using an index number:
```py
motorcycles = ['honda', 'yamaha', 'suzuki']
del motorcycles[0]
```

### pop method (last item)
In cases where you want to retain the item for use after removal, you can use the `pop()` method to pull from the end of the list.
```py
motorcycles = ['honda', 'yamaha', 'suzuki']
popped_motorcycles = motorcycles.pop()

print(motorcycles)
['honda', 'yamaha']

print(popped_motorcycles)
suzuki # this is the item that was 'popped' (removed)
```

> Keep in mind that the popped item will always be removed from the original list!

### pop method (specific position)
Works similarly to accessing a list item with an index:
```py
motorcycles = ['honda', 'yamaha', 'suzuki']
first_owend = motorcycles.pop[0]
print(f"My first motorcycle was a {first_owned}.")
```

### remove method
- Use this if you don't know the index, but only the value.
```py
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.remove('yamaha')
```

> Note that `remove()` only deletes the first occurence of that value. If there are duplicates, you'll need to use a loop.


# Organizing a list
## Sort a list (permanently) with sort() method
- The `sort()` method simply changes list to be in alphabetical order.
- You can pass the `reverse=True` argument to this method if you want to use reverse alphabetical order.
```py
cars = ['bmw', 'audi', 'toyota', 'suburu']

cars.sort()
# or
cars.sort(reverse=True)

print(cars)
# Don't forget, this is a permanent change!
```

## Sort a list temporarily with sorted() function
- The `sorted()` function does the same but only outputs the sorted order, and preserved the original order in the variable.
```py
cars = ['bmw', 'audi', 'toyota', 'suburu']

print(cars) # original list
print(sorted(cars)) # sorted list using the function
print(cars) # original list again
```

## Print a list in reverse order
- The `reverse()` method modifies the list to reverse the order of items.
	- Note that this is a permanent change
	- Also note that this is not the same as reverse chronological order
```py
cars = ['bmw', 'audi', 'toyota', 'suburu']
cars.reverse()
print(cars)
```

## Find the length of a list
- You can use the `len()` function to quickly find the length of a list:
```py
cars = ['bmw', 'audi', 'toyota', 'suburu']
len(cars)
4
```
