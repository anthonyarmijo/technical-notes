- In learning list basics, we were accessing individual elements within the list
- On the contrary, a list **slice** is a ==specific group of items in a list.==

## Slicing a list
- It is as simple as specifying the index number you want to work with
- Similar to the `range()` function, Python won't print the last item
```py
players = ['charles', 'martina', 'michael', 'florence', 'eli']

print(players[0:3]) # print the first 3 values
print(players[1:4]) # print second value through the third
print(players[:4]) # print values from index 0 to 3
print
```

As we previously learned, you can also splice from the end of the list using index number `-1`
```py
players = ['charles', 'martina', 'michael', 'florence', 'eli']

last_3_players = players[-3:]
print(last_3_players)
```

> Similar to looping through a list, a 3rd value lets you indicate how many items to skip between items in your splice/range.

## Looping through a slice
- Similar to above, just introduce loop logic:
```py
players = ['charles', 'martina', 'michael', 'florence', 'eli']
print("Here are the first three players on the team:")
for player in players[:3]:
	print(player.title())
```
## Copying a list

# Tuples
## define a tuple
## loop through a tuple

