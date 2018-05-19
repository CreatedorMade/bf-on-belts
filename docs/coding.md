# Coding
Let's write some brainfuck

## Before you start
A word of caution: brainfuck is a really confusing language. Before you start coding in BoB, you will want to [know how to code in brainfuck](https://esolangs.org/wiki/Brainfuck).

## Machine VMs
Each machine basically runs its own BF virtual machine. Each machine has a looping 8-byte array, so computations done with them must be pretty basic and require only 8 bytes of space. The values within the 8 cells are unsigned 16-bit - they go from 0 to 65535 and will loop around upon going bast either boundary.

## Machine i/o
Machines run on a modified version of brainfuck. In this version, `.,` (input and output, respectively) are replaced with `wasdWASDijkl`.

Each of these characters corresponds to a direction. `w`, `W` and `i` all face up, `a`, `A` and `j` all face left, etc. Whether they input or output depends on how the machine is set up in the belt definition. Their functions are as follows:

Lowercase `wasd` are the push i/o characters. When one is used, the machine goes to sleep until it receives input on that side or is able to output on that side. When data is input, it is taken off of the belt stored in the cell under the pointer (be aware that this overwrites the data in that cell). When data is output, the cell under the pointer isn't modified at all - the data is just copied onto the belt. Since machines are able to grab and put data faster than belts can transport it, it's a good idea to use these characters - they ensure that no matter what, the data WILL get into or out of the machine one way or another. No data loss will ever occur using these characters (unless you belt the data into the void, of course).

Uppercase `WASD` are the grab i/o characters. When one is used, the machine will not go to sleep. It will simply try to grab or put, then continue. Because of this, data loss may occur. In the event that there is no data to input (i.e. the belt is empty), the cell under the pointer will NOT change. In the event that the belt is occupied and there is no space to output, nothing happens - the machine simply won't output. In any other circumstances, these characters act exactly like their lowercase counterparts. These characters are dangerous to use, because they can result in loss of data in some circumstances. Only use them when it's not important if the data gets in or out.

And finally, there's `ijkl` - the i/o conditionals. Unlike `wasd`, these don't actually do any i/o - they simply check if i/o is possible. When using one, the machine will look at the belt and determine whether it can input or output. When inputting, if there is data on the belt that is ready to be input, the cell under the pointer will be incremented by 1. When outputting, the same will happen if there is space on the belt to place output. Use these when you want to avoid unnecessary sleeping by checking if i/o is possible before actually doing it. Bear in mind that a belt tick may occur between the usage of `ijkl` and any subsequent usage of `wasd`, so always use lowercase `wasd` to avoid losing data in the event of.

## Timing
Now, timing is also a pretty important part of BoB. Belt transport isn't instant - for each tile of belt between any two machines, it will take a piece of data an extra tick to reach its destination. Machine programs also run on ticks - in one tick, a machine reads and executes sixteen letters in its program. This means that simple programs will evaluate almost immediately, but longer ones will take longer to "consume" data from the belts. Always optimize your machines to prevent this happening.

One more thing for you to keep in mind: data that reaches a machine will stay on the belt until the machine it's reached uses an i/o command to "suck" it in, so if you're not careful, you'll end up with buildups of data at the end of each belt that can block other machines' outputs and lead to a "data jam".

And finally, a note on machine states: machines can either be running, sleeping (waiting for i/o) or dead. Machines will die when their program finishes, so be sure to use infinite loops like `+[> (code) <]` unless it's important that they stop at some point. Dead machines will remain in the program, but will not execute code and as such will not consume input or generate output. The actual BoB execution environment will end when either A) all machines die or C) all machines are either dead or waiting for input AND there is no `i` (or the `i` has finished reading input) AND there is no data on any belts.

## With that in mind

## A basic CAT
A CAT program takes any input it's given and outputs it back to the user. Here's a full BoB CAT program:
```
i>M>o
M:+[>ad<]
```
(Just doing `i>o` does not work, because there are no machines and thus it will generate a compiler error. If you wanted to do this, just use brainfuck.)

Let's break this down. The belt definition is on top, and the program for `M` is defined on the bottom.

It works like so. Data from the user comes in through the `i` and is passed into machine `M`. `M` is running this brainfuck code:
```
1 +        #add one to the first bit
2 [        #loop while bit 1 is not 0 (which is forever since bit 1 is never modified after line 1)
3  >      #move to bit 2 so as not to modify bit 1, which might end the loop
4  a      #wait for input from the left and store it in bit 2
5  d      #output the value of bit 2 on the right
6  <      #move back to bit 1 so that it's evaluated in the loop command
7 ]        #since the pointer is over bit 1 and bit 1 is not storing 0, the program loops back to line 2
```
So, once it receives its input, it copies the data from the left out onto the belt on the right, sending it to the `o`, which outputs it to the user.

## Programs without input
Programs don't always need user input. Here's one that loops, constantly outputting a number that increases by 1:
```
M>o
M:+[>+d<]
```
Try breaking down the code yourself!

## Machines as splitters
If you've been wondering why there are no ways to split belts in the belt definition, it's because you can do it with machines. Here's a splitter (i.e. it splits incoming data between two outgoing belts):
```
    >>>...
    A
i>>>S
    V
    >>>...
S:+[>awas<]
```
You can see that it alternates between sending data upwards and sending it downwards.

## Some other example programs
Obligatory Hello World implementation
```
M>o
M:++++++++[>++++[>++>+++>+++>+<<<<-]>+>+>->>+[<]<-]>>d>---d+++++++dd+++d>>d<-d<d+++d------d--------d>>+d>++d
```
I'll let you figure out what this one does (it took a while to program)
```
V<<
V A
G>S>o
G:+>+<[>[->>+>+<<<]>>>[-<<<+>>>]<<[->+<]>d<<[->+<]w>>[-]<]
S:+[>awd<]
```

And there you have it! That was the complete Brainfuck on Belts programming specification. Now that you're a master, let's [actually run your code](https://github.com/CreatedorMade/bf-on-belts/blob/master/docs/running.md)!
