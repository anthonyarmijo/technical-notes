# Methods
Methods, just like in PowerShell, are types of actions that can be performed on a piece of data.

For example,
```py
name = 'ada_lovelace'
print(name.title())
```
You can see above that we call the `title()` method using a `.` on the `name` variable. This particular method converts the variable string to use **title case** (e.g. `Ada_Lovelace`)

Some other methods include:
```py
name.upper() #changes the variable (name) to uppercase
name.lower() #changes the variable (name) to lowercase
```
# F-Strings
```py
first_name = "ada"
last_name = "lovelace"
full_name = f"{first_name} {last_name}"
print(full_name)
```

You can use f-strings to reference variables within a string. Simply place the letter f immediately before the opening quotation mark. Then you can use curly braces to reference the variable.

```py
print(f"Hello, {full_name.title()}!")
```

This prints an f-string and calls the 'title' method on our full_name variable in order to provide title case for the stored name within our string.

# Whitespace
## Add Whitespace
You can add whitespace into code by adding these character combinations into strings:
`\t` - Add a tab to your string 
`\n` - Add a newline to your string

```py
print("\tPython") #adds a tab to a string
	Python

print("Languages:\n\tPython\n\tC\n\tJavaScript") #combine multiple
Languages:
	Python
	C
	JavaScript
```
## Remove Whitespace


