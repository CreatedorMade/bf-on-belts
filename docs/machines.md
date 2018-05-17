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

Here, the machine is named `M`. You can see the `>` on the left points into the machine - taking data off of the belt and placing it inside the machine. The other `>` points away from the machine, and places any output from `M` onto the second belt. For any data to go into a machine, there must be an arrow pointing directly into it. Any arrow not facing into the machine (this includes going past the machine on the side) is considered an output.

Now, sometimes you will want to take input from the user and put it onto a belt, or take data from a belt and display it to the user. This is where `i` and `o` come in. By using an i/o character on an `i`, you can take numerical data from the user and put it on a belt, like so:
```
i>M
```
`o` works in the opposite way, taking data off of a belt and showing it to the user:
```
M>o
```
Remember that there can only ever be one `i` and one `o` in a program.

Now that you know about machines, [it's time to do some coding](https://github.com/CreatedorMade/bf-on-belts/blob/master/docs/coding.md)!
