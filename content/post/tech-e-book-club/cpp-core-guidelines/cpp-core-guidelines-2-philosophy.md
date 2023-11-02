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

## Take Advantage of Static Typing and your Compiler

4 reduces to "make programs type safe" which is worth encouraging over the
unholy pointer-casting mess I used to churn out for school.

5 took me a little bit of time to understand, because compile-time checking
combines static typing (mentioned above) with a feature I was less familiar
with: static assertions. As a quick aside, static assertions apply some logic
at compile time (like sizing a data type), rather than spending time executing
instructions in the final binary.

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
