# Machines
Like computers but dumber

## Placing machines
Machines are placed in the belt definition - any character that isn't a belt (`AV><+`), colon `:`, letter `i` or letter `o` is considered a machine. That character is the machine's name, and is used later to define code for it. Here, we have a machine that takes some input from somewhere and puts it onto a belt:
```
>>>>>M>V
       V
       V
       V
       V
```

Here, the machine is named `M`. You can see the `>` on the left points into the machine - taking data off of the belt and placing it inside the machine. The other `>` points away from the machine, and places any output from `M` onto the second belt. For any data to go into a machine, there must be an arrow pointing directly into it. Any arrow not facing into the machine (this includes going past the machine on the side) is considered an output. Blank spaces adjacent to the machine will count as outputs, but will simply destroy the data placed on them.

## Inputs
Now, sometimes you will want to take input from the user and put it onto a belt, or take data from a belt and display it to the user. This is where `i` and `o` come in. By using an `i`, you can take numerical data from the input buffer and put it on a belt, like so:
```
i>M
```
There can only ever be one `i` in a program. It's okay if there isn't one, but there can never be two or more.

When you use an `i`, the compiler turns it into a belt. So the previous program looks (sort of) like this in runtime memory:
```
in:true
inX:0
inY:0
world:[[>,>,M]]
```
This means that you can place an `i` inline with a belt, and it will function normally. For example, `M>i>o` becomes `M>>>o` in memory. Just remember to never place more than one belt leading away from an `i`, because these belts determine the direction the `i` faces in runtime - so having more than one may result in unpredictable behaviour during compile time.

## Outputs
`o` works in the opposite way, taking data off of a belt and showing it to the user:
```
M>o
```
Unlike `i`, `o` does not compile into a belt. Instead, it compiles into a special tile that destroys all data on top of it (after printing it to the console, of course). In a setup like this:
```
M>o>E
```
Data from M will get destroyed by the `o` before it makes it to E, so keep that in mind.

## Destroying data
Belts have another special use: they can destroy data. Belts do not have to face onto other belts, or into machines - they can face directly into the edge of the grid, or onto an empty tile. Data that is belted off the edge of the grid or onto an empty tile is destroyed irrecoverably, which can be useful in some situations and disastrous in others. Always keep this in mind when designing belts.

Now that you know about machines and i/o, [it's time to do some coding](https://github.com/CreatedorMade/bf-on-belts/blob/master/docs/coding.md)!
