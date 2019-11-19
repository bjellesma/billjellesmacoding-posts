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

### Tertiary Statements

Using if statements isn't always my favorite because of the readability and maintainability, but Python has improved on the idea of `tertiary` statements to make them concise and readable at the same time. Tertiary statements are really just single line if statements. 

Here's a tertiary statement in C#:

```cs
Console.Writeline("You can dance") ? variable=="you want to" : Console.Writeline("You can leave your friends behind");
```

That's pretty unintuative to a beginner if you ask me. What's the ? and what's the :

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