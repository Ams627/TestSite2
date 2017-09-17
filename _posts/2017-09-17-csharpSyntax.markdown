---
layout: post
title:  "Pattern matching: a new feature of C# 7"
date:   2017-09-17 15:36:08 +0100
categories: c#
---
The `is` operator in C# allows you to test if an object instance is covertible to a type as follows:
{% highlight csharp %}
if (o is Window)
{
    Window w = (Window)o;
}
{% endhighlight %}

From C# 7, you can use [pattern matching](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/is#type) 
with `is` to avoid the extra declaration and cast in the code sample above.
{% highlight csharp %}
if (o is Window window)
{
    window.Centre();
}
{% endhighlight %}
Pattern matching can also be used in a `switch` statement:
{% highlight csharp %}
Shape shape = new Triangle();
switch (shape)
{
    case Square sq:
        Console.WriteLine("Square");
        break;
    case Triangle tr:
        Console.WriteLine("Triangle");
        break;
}
{% endhighlight %}





