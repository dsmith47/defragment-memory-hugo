+++
author = "Doug Smith"
title = "Core War: Assembly Code as a Game"
date = "2023-19-11"
description = "I found a game that is just an assembly specification. This is what happened next."
toc = false
draft = true

categories = [
  "Games"
]
tags = [
  "Core War",
  "Assembly"
]
+++

# Core War: What is it?

Core War (sometime confusingly also called "Core Wars") was created in 1984 by
D. G. Jones and A. K. Dewdney to simulate a competition over a memory space in
a cpu core by programs executing simultaneously. At a high level we can think
of the "rules" to be:

1. The "Core" is a sequentially-addressed array, each index of which contains
    an instruction.
2. Two (or more) programs are written as sequences of instructions at random
    places of the Core.
3. Each program receives a thread of execution that will focus an instruction,
    execute that instruction, and move on to the next instruction
4. If a program tries to execute an illegal instruction, it fails and is
    removed from competition
5. After a predetermined number of steps are executed, either one program
    remains and is the winner, or the match is a draw

And that's it, just a few low level programs trying to keep themselves running
while trying to interfere with other programs (for instance writing strange
instructions within their execution space) so that they fail.

There's a bit more to it. For instance, programs can have multiple threads of
execution and isn't out unless every single thread fails, but only one thread
can execute per game step as a way to make sure all competitors are doing the
same amount of work, making "parallelism" kind of unique in this context, but
that's more of an implementation detail.

# Tools for the Game: Redcode

TODO: some details for Redcode standard

# Learning Core War

So knowing all the code stuff is nice, but understanding how it plays in the
game is another thing. Core War is a pretty old and niche game, but there are
still resources around for how to play it.
[A series of articles by A.K. Dewdney](https://www.corewars.org/sciam/) are
still distributed online by [CoreWars.org](https://www.corewars.org/) (yep,
they're calling it Core Wars), which archives
[several resources for learning to write competitive programs](https://www.corewars.org/information.html).

And I guess by documenting things that I'm doing trying to understand this
game, I'm working on another resource right now. Let's start digging in to
see what we can find out.