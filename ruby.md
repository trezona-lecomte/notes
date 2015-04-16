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
You can now request information about the following configuration information:

| Term        | Directory Contents                                                      |
| :-----------|:------------------------------------------------------------------------|
| rubylibdir  | Ruby standard library                                                   |
| bindir      | Ruby command-line tools                                                 |
| archdir     | Architecture-specific extensions and libraries (compiled, binary files) |
| sitedir     | Your own or third-party extensions and libraries (written in Ruby)      |
| vendordir   | Third-party extensions and libraries (written in Ruby)                  |
| sitelibdir  | Your own Ruby language extensions (written in Ruby)                     |
| sitearchdir | Your own Ruby language extensions (written in C)                        |

An example of such a request would be obtaining the location of the `ruby` 
and `irb` executable files:
```
RbConfig::CONFIG["bindir"]
```
`RbConfig` is a constant that refers to the hash where Ruby keeps its config
data. `"bindir"` is the key to access the corresponding value, the binary-file
installation directory.

Note that the `gems` directory won't be available using RbConfig, however it 
is usually at the same level as `site_ruby` (`RbConfig::CONFIG["sitedir"]`).

### Loading External Files and Extensions ###
To examine `ruby`'s load path:
```
ruby -e 'puts $:'
```
Note that the `-e` flag indicates that you're passing inline ruby as an 
argument.

You can find relative directories when loading libraries:
```
load "../my_other_file.rb"
```
Because `load` is a method, it is executed at the point where Ruby encounters
it - you can load different libraries based on conditionals etc. Also, `load`
will load the file regardless of whether you've already loaded it before.

`require`, on the other hand, doesn't reload files it has already loaded. 

Strictly speaking, you don't `require` a file; you `require` a *feature*.


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


## Plain Old Ruby Loops ##

```
loop do

end
```

```
5.times do

end
```

```
while condition_is_true

end
```

```
until condition_is_false
    
end
```

```
for iterator in iterable_object

end

for number in (0..5)
    puts number
end

for item in my_array
    puts item
end
```



## Enumerable ##

### Reduce / Inject ###
```
reduce(initial, sym) -> obj
reduce(sym) -> obj
reduce(initial) { |memo, obj| block } -> obj
reduce { |memo, obj| block } -> obj
```
Combines all elements of *enum* by applying a binary operation, specified by a block or a symbol that names a method or operator. 

If your specify a block, then for each element in *enum* the block is passed an accumulator value (*memo*) and the element. If you specify a symbol instead, then each element in the collection will be passed to the names method of *memo*. In either case, the result becomes the new value for *memo*. At the end of the iteration, the final value of *memo* is the return value for the method.

If you don't explicitly specify an *initial* value for *memo*, then the first element of the colletion is used as the initial value of *memo*.

## Conventions ##
Ruby variable conventions:

| Type     | Ruby convention |
| :--------|:----------------|
| Local    | last_name       |
| Instance | @last_name      |
| Class    | @@last_name     |
| Global   | $LAST_NAME      |

