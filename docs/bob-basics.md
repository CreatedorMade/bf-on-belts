# Brainfuck on Belts Basics
You gotta start somewhere

## Getting started
BoB files are, as discussed in the readme, split into two parts - the belt definition and the program definition. Any file will look like this:

```
<belt definition>
:<machine name 1>:<minified brainfuck code>
:<machine name 2>:<minified brainfuck code>
...
:<machine name n>:<minified brainfuck code>
```

The belt definition is its own language, basically. In it, you have 6 different control characters that are used to make the belts, those being `AV<>+=`. Here, = is the most important character - it represents a belt. + is a bridge, where two belts cross each other but no data transfer occurs. And finally, A, V, < and > are input/output characters - they put data into machines and take data out.

Any valid belt will be a line of `=` leading to any i/o character. Every belt is a single line - no splitting or merging is allowed. Here are some valid belts:

```
>=====>   Pretty straighforward, it's a line

=======   Multiple inputs, one output
A  A  V

   ===
>= = =>   Wavy design, is like a straight line but longer
 ===
```
You can see that each belt has one or more i/o characters pointing onto it and exactly one pointing off of it. Every belt must have exactly one exit character - it doesn't matter where it is, data will flow towards it from anywhere. With this in mind, here's a more advanced use of belts, to give you an idea of the possibilities:
```
V   V
=====
  V
```
Here, there are two inputs to the belt and only one output - setups like this can be used to take data from multiple sources and treat it the same.

There are, however, lots of ways to create invalid belts. Remember, each belt is a line - no splitting or merging. If you want to test a belt's validity, just look at each character on it. If any `=` is adjacent to three or more other `=`s, it's invalid. If it loops, it's also invalid. And of course, the golden rule, each belt must have exactly one output.

Now that you know about belts, it's time to learn about machines! (this is going to be a link once I write the page on machines)
