A couple of days ago, I found myself in a position where I upload some C# classes to production. These C# sharp classes all reference a centralized library that I use. In order so that I don't need to rebuild every single file when I change one method on the library, I use different versions of the library. The problem is that I forget the version of the library that I'm referencing whenever I make changes to the C# class. 

![Uh Oh](https://img.thedailybeast.com/image/upload/c_crop,d_placeholder_euli9k,h_1440,w_2560,x_0,y_0/dpr_1.5/c_limit,w_1044/fl_lossy,q_auto/v1513982397/171220-ryan-home-alone-tease_zntomw)

I wondered to myself if you'd be able to tell the version of my library being referenced from the DLL. It makes sense because you still need the library DLL even after the C# class is compiled. Is this actually possible? Is this reverse engineering? Will I go to jail? To my great elation, I found that this definetly is possible using the [reflections](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection) library. 

To find useful information about a file assembly, you can simply use the following and stick that assembly object in a variable with `var`:

```cs
var assembly = System.Reflection.Assembly.ReflectionOnlyLoadFrom(fileName);
```

The `var` keyword allows the compiler to determine the type. Like Javascript, the var keyword can contain any type of variable and the compiler will throw an error if anything is amiss.

Now, we can go ahead and get all of the referenced assemblies with:

```cs
var referencedAssemblies = assembly.GetReferencedAssemblies();
```

This gives a lot of information that I don't need about the file. References to mscorelib, system.data, microsoft.csharp. I only need to know about my library. I can easily just filter this:

```cs
if (assemblyName.ToString().Contains("<Library Name>"))
                            {
                            \\found!
                            }
```

What makes this even easier is that I have all of my C# classes located in one directory. So, I can simply iterate over the entire directory. I can even filter the fileNames so that only DLLs are found. What's more? I can write all of this to a file so that I don't have all of this information scroll by in the console.

```cs
string[] fileNames = Directory.GetFiles("C:\\P21\\Plugins", "*.dll");
            using (System.IO.StreamWriter file = new System.IO.StreamWriter("references.text"))
            {
                
                foreach (string fileName in fileNames)
                {
                    try
                    {
                        var assembly = System.Reflection.Assembly.ReflectionOnlyLoadFrom(fileName);
                        var referencedAssemblies = assembly.GetReferencedAssemblies();

                        foreach (var assemblyName in referencedAssemblies)
                        {
                            if (assemblyName.ToString().Contains("<Library Name>"))
                            {
                                file.WriteLine(fileName);
                                file.WriteLine(assemblyName);
                            }

                        }
                    }
                    catch (System.IO.FileLoadException ex)
                    {
                        file.WriteLine($"Unable to parse ${fileName}. Error: ${ex.Message}");
                    }
                    
                }
            }
```

Lastly, notice that we've included a try catch statement to catch any errors if we're unable to load the assembly information. Because of the nature of DLLs, the file could be locked by another program.
