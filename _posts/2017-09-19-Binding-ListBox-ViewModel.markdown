---
layout: post
title:  "Binding a ListBox to a collection on your view model"
date:   2017-09-16 10:12:08 +0100
categories: XAML
---
There are a few steps to creating a simple MVVM program using WPF. Let's go through them!

1. First of all you need a way to define and create your viewmodel. In the simplest example
the view model is just a class. It doesn't need to inherit from anything. It is created by specifying its
name in a xaml `DataContext` element within the Resources section of a `Window`, Panel or `Control`.

   We are going to try to create a program to manipulate the Windows PATH (the environment variable used to determine
the location of executables when typed from the command line). We will need to be able to select a directory within
a `ListBox` containing all the directories in the path and move its position in the list up and down. 
Therefore, we will define a class that holds the directory and a boolean to indicate if the path is selected within
the `ListBox`. 

{% highlight csharp %}
    public class PathWithSelection : INotifyPropertyChanged
    {
        private string _directory;

        public event PropertyChangedEventHandler PropertyChanged;

        public bool Selected
        {
            get
            {
                return _selected;
            }
            set
            {
                _selected = value;
                OnPropertyChanged();
            }
        }

        private bool _selected { get; set; } 

        public bool Focused { get; set; } = false;
        public string Directory
        {
            get
            {
                return _directory;
            }
            set
            {
                _directory = value;
                OnPropertyChanged();
            }
        }

        void OnPropertyChanged([CallerMemberName]string name = null)
        {
            PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(name));
        }
    }
{% endhighlight %}
We'll delve into the details of this later, but for now, just accept that we need this class as part of our 
view model.

The actual viewmodel class is defined as follows:

{% highlight csharp %}
    public class ViewModel
    {
        public ObservableCollection<PathWithSelection> SystemPaths { get; private set; } = new ObservableCollection<PathWithSelection>();
        public ObservableCollection<PathWithSelection> UserPaths { get; private set; } = new ObservableCollection<PathWithSelection>();
        public ViewModel()
        {
            var systemPaths = Environment.GetEnvironmentVariable("PATH", EnvironmentVariableTarget.Machine);
            var userPaths = Environment.GetEnvironmentVariable("PATH", EnvironmentVariableTarget.User);

            systemPaths.Split(';').ToList().ForEach(x=>SystemPaths.Add(new PathWithSelection { Value = x }));
            userPaths.Split(';').ToList().ForEach(x => UserPaths.Add(new PathWithSelection { Value = x }));
        }
    }
{% endhighlight %}





