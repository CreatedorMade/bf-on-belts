# bf-on-belts
Brainfuck on Belts: because Ruby on Rails is too mainstream

## What is it?
Brainfuck on Belts is a variation on the esoteric programming language [Brainfuck](https://esolangs.org/wiki/Brainfuck), with a bad Ruby on Rails pun thrown in there. If you're in a hurry, just say that it's kinda like [RubE on Conveyor Belts](https://esolangs.org/wiki/RubE_On_Conveyor_Belts).

## About Brainfuck
Brainfuck, or BF if you're being polite, is an... interesting language. In it, you have an array of cells acting as your memory, and a set of characters that let you move your "pointer" around the array and either add to, subtract from or compare the values under it. It only has 8 valid characters - those being `><+-.,[]`. Each program written in it will look something like this:

```brainfuck
++++++++[>++++[>++>+++>+++>+<<<<-]>+>+>->>+[<]<-]>>.>---.+++++++..+++.>>.<-.<.+++.------.--------.>>+.>++.
```

(It's a hello world program)
BoB uses a slightly different version of BF, where there are 4 commands (replacing . and ,) that can each either be used for inputting and outputting. Everything else about it is the same.

## What about the belts?
I thought you'd never ask!
BoB is split into two parts - the belt definition and the program definition. The belt definition creates a set of machines and belts. Belts transport data around, while machines can take data in from the belts, use brainfuck code to evaluate it, and spit it back out onto the belts. The program definition defines the code for each machine.

## Further reading
WIP - Links to the technical pages will show up once I start writing them.
