+++
author = "Doug Smith"
title = "C++ Core Guidelines: Introduction"
date = "2023-10-30"
description = "My motivation for reading C++ Core Guidelines and summarizing its introduction"

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

So I've been starting to look at career moves that require more systems-level
programming, and as a result I'm circling back to studying C++. I've done a lot
with C++ in the past, but as I've spent more time making other languages work
for my professional/personal studies, I've undoubtably forgotten some good
tricks and missing some new developments.
<!-- more -->
Almost immediately I encounter my first C++ learning challenge: what reference
material do I use to (re-)learn the more granular bits? I haven't been able to
find an obvious consensus on good books for every C++ developer to read (unlike
the evangelization of, say, Effective Java). This divergence I think justifies
my "book" choice for this task: 
[C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
by [Bjarne Stroustrup](https://www.stroustrup.com/) and 
[Herb Sutter](https://herbsutter.com/). It's not quite book-length, but its
more up to date than any of the 2000s-era books I'v had recommended, and
anything from Stroustrup on C++ seems likely to have some relevant technical
detail.

# Introduction

The Introductoin starts with some boilerplate covering patch notes from
previous versions and philosophical aims of the guide. Notably, their stated
goal is to encourage use of certain C++ extensions as a substitute for more
dangerous practices. The rules I remember best in Effective Java are all of the
form "Prefer _____ over _____", so I'm already feeling comfortable with the
format. The intro also points out that rules aren't meant to be read serially.
Because I have no specific program to check parameters and because of the format
of this blog, I will present them serially, but feel free to jump around the
posts or skip to the article itself and navigate its links, I think the
implication is that they won't be strictly dependant on each other.

The introduction alse contains a statement of values for what kind of code
they're written to enforce: a "strongly-typed" and "memory-safe" application.

That sounds like it plays to C++'s strengths and guards against its weaknesses;
I think I'm in the right place.