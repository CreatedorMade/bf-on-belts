# Coding
Let's write some brainfuck

## Before you start
A word of caution: brainfuck is a really confusing language. Before you start coding in BoB, you will want to [know how to code in it](https://esolangs.org/wiki/Brainfuck).

## The details
Each machine basically runs its own BF virtual machine. Each machine has a looping 8-byte array, so computations done with them must be pretty basic and require only 8 bytes of space. Now, the brainfuck part of BoB is slightly modified - here, `.` and `,` are replaced with `wasd`, where each letter corresponds to a direction. `w` is up, `s` is down, `a` is left and `d` is right. Each letter will either act as an input or output - it all depends on how the machine is set up in the belt definition.

Now, timing is also a pretty important part of BoB. Belt transport isn't instant - for each tile of belt between any two machines, it will take a piece of data an extra tick to reach its destination. Machine programs also run on ticks - in one tick, a machine reads and executes one letter in its program.

On the subject of timing and i/o, you will find that your machines will go to sleep when you use any of the `wasd` characters. This is because they are either waiting for input to come in on the belt, or waiting for space on the belt to place output. If you do not want them to sleep while performing i/o, use `WASD` instead. This is dangerous, however, because if there is no data to input, the byte under the pointer will not be changed - and when outputting, if there is no space on the belt to output, nothing happens and the data never makes it onto the belt. Also, data that reaches the end of a belt will stay there until the machine it's reached uses an i/o command to "suck" it in, so if you're not careful, you'll end up with buildups of data at the end of each belt that can block other machines' outputs and lead to a "data jam".

And finally, a note on machine states: machines can either be running, sleeping (waiting for i/o) or dead. Machines will die when their program finishes, so be sure to use infinite loops like `+[> (code) <]`. Dead machines will remain in the program, but will not execute code and as such will not consume input or generate output. The actual BoB execution environment will end when either A) the user stops it, B) all machines die or C) all machines are either dead or waiting for input AND there is no `i` AND there is no data on any belts.

## A basic CAT
A CAT program takes any input it's given and outputs it back to the user. Here's a full BoB CAT program:
```
i>=>M>=>o
M:+[>ad<]
```
Let's break this down. The belt definition is on top, and the program for `M` is defined on the bottom.

It works like so. Data from the user comes in through the `i` and is passed into machine `M`. `M` is running this brainfuck code:
```
+        #add one to the first bit
[        #loop while bit 1 is not 0 (which is forever since bit 1 is never modified after line 1)
  >      #move to bit 2 so as not to modify bit 1, which might end the loop
  a      #wait for input from the left and store it in bit 2
  d      #output the value of bit 2 on the right
  <      #move back to bit 1 so that it's evaluated in the loop
]        #since the pointer is over bit 1 and bit 1 is storing 1, the program loops back to line 2
```
So, once it receives its input, it copies the data from the left out onto the belt on the right, sending it to the `o`, which outputs it to the user.

## Programs without input
Programs don't always need user input. Here's one that loops, constantly outputting a number that increases by 1:
```
M>=>o
M:+[>+d<]
```
Try breaking down the code yourself!

## Machines as splitters and mergers
If you've been wondering why there are no ways to split and merge belts in the belt definition, it's because you can do it with machines. Here's a splitter (i.e. it splits incoming data between two outgoing belts):
```
    ===...
    A
i>=>S
    V
    ===...
S:+[>awas<]
```
And a merger:
```
...===
     V
     M>=>o
     A
...===
M:+[>[-]W[d][-]S[d]<]
```
The merger's code is particularly tricky because it uses nested loops. It will also not output any data if the data on the belt is 0, so keep that in mind. It's a good example of using `WASD` instead of `wasd` - since data might not come in on either side, it will happily keep going along rather than waiting for data that never arrives.

## Some other example programs
Obligatory Hello World implementation
```
M>=>o
M:++++++++[>++++[>++>+++>+++>+<<<<-]>+>+>->>+[<]<-]>>d>---d+++++++dd+++d>>d<-d<d+++d------d--------d>>+d>++d
```
I'll let you figure out what this one does (it took a while to program)
```
=====
V   A
G>=>S>=>o
G:+[>[+d][->+<]w[->>+>+<<<]>>>[-<<<+>>>]<<[->+]>d[-]<<<]
S:+[>awd<]
```
