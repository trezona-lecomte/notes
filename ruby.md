## Fundamentals ##

Everything is an object, and every object is an instance of exactly one class.

The concept of an object is 'more important' than the concept of a class in
Ruby. What this means is that while the class is responsible for instantiation,
the object is mutable following instantiation (in terms of it's methods and 
behaviours), so it takes on 'a life of it's own'. This ability for objects to
adopt behaviours that weren't defined in their class is a core aspect of the
Ruby language design.

### Command Line & irb ###
The `ruby` interpreter can check programs for errors without executing them,
using:
```
ruby -cw my_file.rb
```
The `-c` flag means *check for syntax errors*, while the `-w` flag means *use
a higher level of warnings*.

To get `ruby` to let you access to lots of compiled-in config information
about your Ruby installation, use `irb`'s `-r` flag and the `rbconfig` package:
```
irb --simple-prompt -rrbconfig
```


### Input/Output ###
Reading a file in Ruby is super easy:
```
data = File.read("my_file.dat")
```
Writing to a file is just as simple:
```
fh = File.new("output.txt", "w")
fh.puts "Sending output to a file rather than stdout..."
fh.close
```
Note that `fh` is shorthand for file handle.



## Conventions ##
Ruby variable conventions:

| Type     | Ruby convention |
| :--------|:----------------|
| Local    | last_name       |
| Instance | @last_name      |
| Class    | @@last_name     |
| Global   | $LAST_NAME      |

