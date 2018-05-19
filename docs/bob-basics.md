# Brainfuck on Belts Basics
You gotta start somewhere

## Getting started
BoB files are, as discussed in the readme, split into two parts - the belt definition and the program definition. Any file will look like this:

```
<belt definition>
<machine name 1>:<minified brainfuck code>
<machine name 2>:<minified brainfuck code>
...
<machine name n>:<minified brainfuck code>
```
In this segment, we'll focus on the belt definition.

## Building the belts
The belt definition is its own language, basically. In it, you have 5 different control characters that are used to make the belts, those being `AV<>+`. Here, `AV<>` - the arrows - are the most important characters - they represent belts, as well as i/o for the machines. `+` is a bridge, where two belts cross each other but no data transfer occurs between them. Think of it as one belt "going above" another.

Any belt will be a line of arrows leading into a machine or onto another belt. Here are some examples of belts:

```
>>>>>>>   Pretty straighforward, it's a line

>>>>>>V   Multiple inputs, one output
A  A  V

   >>V
>V A >>   Wavy design, is like a straight line but longer
 >>A
```

Belts don't have to be in single lines, however. Here's a more complex system of belts, to give you an idea of the possibilities:

```
V   V
>>V<<
  V
>>+>>
  V
  V
```
Belts can be in any configuration - merging is allowed, but data takes up space on the belts, so it's not recommended.

Now that you know about belts, it's time to [learn about machines](https://github.com/CreatedorMade/bf-on-belts/blob/master/docs/machines.md)!
