# Running
Let's get this brainfuck ball rolling

## Using bob.jar
If you don't have Java installed, you'll want to do that now. First thing you'll need to run your BoB program is bob.jar - find it in the root directory of this repository, and download it. Your browser may tell you not to keep it, as .jar files are potentially harmful. Don't worry, I promise it isn't a virus `;)`.

Now that you have the BoB realtime interpreter, all you need to do is open up a command prompt in the directory the jar is located in (`shift+right click > Open command window here` on Windows) and type in the following text:
```
java -jar bob.jar your-filename-here
```
This will run interpreter with your code. In the event that there is a compiler error, it will tell you exactly what's wrong. If there's nothing wrong, however, your code will run and you'll see something like this:
```
Brainfuck on Belts realtime interpreter by Anaerek

10      : 1
11      : 2
12      : 3
13      : 5
14      : 8
15      : 13
...
```
In this case, the numbers on the left are the tick markers - they count the number of ticks since the program has started. The numbers on the right are the output - they're the actual data that the program produced.

## Arguments
You can specify a speed for your program to run at. This is useful when it generates infinite output very quickly - by turning the speed down, you can actually keep track of the vast amount of data generated. Do this by appending a number to the end of the command. The interpreter will run at that many ticks per second (unless it can't keep up).

Now, if you want to input some data into your program (using the `i` tile), simply write some numbers after the speed argument (which is required with input - if you want to act like it's not there, set it to 0). These will be placed onto the `i` tile in your program, in order. For example:
```
java -jar bob.jar adder.txt 100 5 9
```
Would input the numbers 5 and 9 into the program. If the program's name is anything to go by, it might produce 14 as an output.

## Halting
Sometimes, a program just doesn't end. If you have an infinite loop or an especially stubborn machine, the interpreter will just go on and on and on. In this case, you can force it to stop using the command line force stop key (`ctrl+c` on basically any platform).

And there you go! You now know how to write and run programs in Brainfuck on Belts! Now take this knowledge and try to write something useful, I dare you.
