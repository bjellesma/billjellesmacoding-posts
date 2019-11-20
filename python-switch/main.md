It's easy to fall in love with the simplistic and beautiful syntax of Python. The ease of use, high extensibility and sheer power of Python make it the [2nd most popular programming language in 2019](https://hackernoon.com/8-top-programming-languages-frameworks-of-2019-2f08d2d21a1) according to Hackernoon. I know that Python is often my go-to programming language for side projects.

One feature of the language (or lack of) in the language that I've always had an issue with is a `switch` statement. I also work a lot in C# and whenever I'm faced with the possibility of creating a bunch of `if` statements, I can simply write a `switch` statement to test the value of the variable. Instead of writing the following `if` statements in C#:

```cs
if(variable == "jeff"){
    Console.Writeline("Hi Jeff")
}
else if(variable == "danny"){
    Console.Writeline("Hi Danny")
}
else if(variable == "nick"){
    Console.Writeline("Hi Nick")
}
else{
    Console.Writeline("Hey you")
}
```

We can write the equivalent using a `switch` statement

```cs
switch(variable){
    case "jeff":
        Console.Writeline("Hi Jeff")
        break;
    case "danny":
        Console.Writeline("Hi Danny")
        break;
    case "nick":
        Console.Writeline("Hi Nick")
        break;
    default:
        Console.Writeline("Hey You")
}
```

This is a lot neater of code and definately more maintainable.

Unfortunately, there's no official `switch` statement in Python, instead we just need to be a little more creative.

## Think outside the Box

### Ternary Statements

Using if statements isn't always my favorite because of the readability and maintainability, but Python has improved on the idea of `ternary` statements to make them concise and readable at the same time. Tertiary statements are really just single line if statements. 

Here's a ternary statement in C#:

```cs
Console.Writeline("You can dance") ? variable=="you want to" : Console.Writeline("You can leave your friends behind");
```

That's pretty unintuative to a beginner if you ask me. What's the question mark and what's the colon? I'm probably 

```python
#here's a simple if statement
print("You can dance") if variable=="you want to" else print("You can leave your friends behind")
```

That's way more concise than a regular if statement and just as readable.

```python
if variable=="you want to":
    print("You can dance")
else:
    print("You can leave your friends behind")
```

### Dictionary Lookups

Python makes the concept of Dictionaries very simple to implement. One important trick with dictionaries in Python is to utilize them as lookup tables

```python
hello_dict = {
    "jeff": "Jeff",
    "danny": "Danny",
    "nick": "Nick"
}
```

Now, you can reference the person to say hello to by using

```python
print('Hi {}'.format(hello_dict["nick"]))
```

But what happens if we want to say hi to someone not in the dictionary, namely Sam? In the C# Switch Case, this would be the default case that our logic falls through. In Python, we can use the `get` method to get our dictionary key. This way, if the key isn't in our dictionary, we can simply return a `None`. Better yet, we can pass in a second argument to return what we want in the default case.

```python
print('Hi {}'.format(hello_dict.get("sam", "you")))
```

The cool thing about this dictionary is that we can use this logic to call a function with the dictionary lookup. 

```python
def say_hi(fellow):
    phrase = "I'm in a function {}".format(fellow)
    return phrase

hello_dict = {
    "jeff": say_hi("Jeff"),
    "danny": say_hi("Danny"),
    "nick": say_hi("Nick")
}

print('Hi {}'.format(hello_dict.get("nick", "you")))
```

This is a simple example but it illustrates the fact that we create entire code blocks inside of our dictionary lookup.

## Conclustion

Personally, I will use both the ternary operatory and dictionary lookup because they have different use cases in my mind. Remembering that readability is important for other developers as well as yourself after a long weekend, I'll use the ternary operator for simple assignments. For example, if I'm building out an API, I'll use ternary operators to get my form data.

```python
username = request.form.get("username") if "username" in request.form else "Invalid user"
```

If I have either multiple cases or long codeblocks, I'll use a dictionary lookup. An example of this would be if I'm using an API that gives me a zero indexed month and I need the corresponding full name of the month.

```python
months = {
    0: "January",
    1: "February",
    2: "March",
    3: "April",
    ...
    11: "December"
}
```