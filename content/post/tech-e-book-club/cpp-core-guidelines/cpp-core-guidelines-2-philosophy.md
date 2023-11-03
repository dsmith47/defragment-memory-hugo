+++
author = "Doug Smith"
title = "C++ Core Guidelines: Introduction"
date = "2023-10-31"
description = "Guiding philosophy on C++"
draft = True

categories = [
  "Tech E Book Club"
]
tags = [
  "C-langs"
]
series = [
  "C++ Core Guidelines"
]
+++

# Philisophy

The first proper section lays out some guiding philosophies for writing good
C++. This is a combination of C++ specific advice and just good general
pratice in programming languages, so I won't cover everything exhaustively,
but here's the list for completness.

1. Express ideas directly in code
2. Write in ISO Standard C++
3. Express intent
4. Ideally, a program should be statically type safe
5. Prefer compile-time checking to run-time checking
6. What cannot be checked at compile time should be checkable at run time
7. Catch run-time errors early
8. Don't leak any resources
9. Don't waste time or space
10. Prefer immutable data to mutable data
11. Encapsulate messy constructs, rather than spreading through the code
12. Use supporting tools as appropriate
13. Use support libraries as appropriate

To talk about them more, I've packaged these ideas into a few broad categories.

## Be a Good (Object-Oriented) Programmer

1 and 3 are just good advice in any programming language. Methods, classes, and
variables should be self-documenting if at all possible, b/c comments can get
seperated from the logic it documents, but you can't seperate logic from
itself. I do think "Compilers don't read comments... and neither do many
programmers..." is a pretty funny way to state this imperative, though.

6 and 7 are reminders to check boundaries and "if you're going to fail, fail
fast".

9 contains is a reminder that "time and space you spend well to achieve a
goal is not wasted", attached to a general reminder to be efficient. I think
it was probably good to precede this with 8, don't leak any resources, because
that is probably the one place where quality-of-life at other stages in
development won't matter.

10 is a reminder to prefer immutability when you don't intend to mutate
something.

11 Is about abstracting tricky functions into their own objects/functions,
and 13 extends this into selecting supporting libraries that have already done
the encapsulating/testing for you.

Calling this section "Be a good programmer" maybe seems a bit dismissive of
the utility of these principles in C++, so I want to take a minute to say the
opposite. These things make you a competent object-oriented programmer, and C++
very much likes object abstraction, so to use C++ competently you need to be
aware of these preferences and know how to use the C++ constructs that support
them. Do you know how to make a value constant? How about making an object 
immutable? How readable is the code you're writing, and how would you make it
more readable? I needed to refresh a lot of my own C++ knowledge to understand
the examples provided here b/c while every OO language favors these points to
some extent, they do so through different constructs. A C++ guide needs to talk
about OO principles in order to talk about the C++ features that undergird
these fundamentals.


## Take Advantage of Static Typing and your Compiler

4 reduces to "make programs type safe" which is worth encouraging over the
unholy pointer-casting mess I used to churn out for school.

5 took me a little bit of time to understand, because compile-time checking
combines static typing (mentioned above) with a feature I was less familiar
with: static assertions. As a quick aside, static assertions apply some logic
at compile time (like sizing a data type), rather than spending time executing
instructions in the final binary.

12 encourages you to use other tools like static analyzers to enforce coding
standards, which isn't necessarily a compiler-advantage, but it any tool that
you run your code through provides some pre-compile utility that should benefit
the final program.

## Be Aware that this is a lower-level language

2 enforces the ISO whenever possible, which makes sense b/c it's the portable
logic. However, I hadn't meditated on the implications of this when writing
system-specific code that uses non-ISO extensions. Of course anything outside
of the ISO should be abstracted away behind and interface so that funcitonality
doesn't make the rest of your code too architecture-specific. It's obvious that
this makes your code easier to extend to other architectures later.

In most programming language I wouldn't think about this, because the libraries
that handle that abstraction are already implemented for me (often in C/C++).



I think this subset contains some of the best C++-specific points in this
section. While a lot of the time your C++ logic is implementing Java objects
with more memory management, you have the features and responsabilities of
an object-specific architecture.
