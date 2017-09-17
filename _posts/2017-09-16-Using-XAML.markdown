---
layout: post
title:  "Comparing XAML inline syntax with XAML object element syntax"
date:   2017-09-16 10:12:08 +0100
categories: XAML
---
There are two XAML syntaxes:
* __inline syntax__ - a property is represented by an XML attribute.
* __object element syntax__ - a property is represented by a nested XML object.

Inline syntax can always be represented by equivalent object element syntax. For example, the following code

{% highlight XML %}
<ListBox ItemTemplate="{StaticResource PathVisualTemplate}"/>
{% endhighlight %}

can be represented as follows:

{% highlight XML %}
<ListBox>
    <ListBox.ItemTemplate>
        <StaticResource ResourceKey="PathVisualTemplate"/>
    </ListBox.ItemTemplate>
</ListBox>
{% endhighlight %}

Object Element Syntax is need for objects with complex properties such as a context menu:

{% highlight XML %}
<ListBox>
    <ListBox.ContextMenu>
        <ContextMenu>
            <MenuItem Header="Press this"/>
            <MenuItem Header="Press that"/>
        </ContextMenu>
    </ListBox.ContextMenu>
</ListBox>
{% endhighlight %}
though of course the context menu can be specified in any resource section like this:

{% highlight XML %}
<Window.Resources>
    <ContextMenu x:Key="CMenu1">
        <MenuItem Header="Press this"/>
        <MenuItem Header="Press that"/>
    </ContextMenu>
</Window.Resources>
{% endhighlight %}

and then referenced using inline syntax as follows:
{% highlight XML %}
<ListBox ContextMenu="{StaticResource CMenu1}"/>
{% endhighlight %}





