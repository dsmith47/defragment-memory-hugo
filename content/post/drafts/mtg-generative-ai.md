+++
author = "Doug Smith"
title = "Magic: the Generating"
date = "2023-19-11"
description = "Putting generative AI to work on game design for one of the world's most storied trading card games."
toc = false
draft = true

categories = [
  "Projects"
]
tags = [
  "ML/AI",
  "Computational Creativity"
]
+++

I find AI in board games an interesting space. The nature of the patterns
and probabilities inherent to AI models gels nicely with a certain set of
games, games can tolerate incompleteness of an output if it is novelty 
(see discussions of bugs and house rules), and the whole space is relatively
low-stakes in the sense that a "failed" result (which I guess here means
something that isn't fun to interact with), isn't likely to cause any human
suffering.

All of these features make Computational Creativity and Interactive Media a
fun space for hobbyist play, and I have some of my own theses I'd like to test
out. But first, let's do some backgroun on one of the older GAI-for-games
projects I'm familiar with.

# The Storied History of AI-generated MTG cards

TODO: the original mtg-rnn thread
TODO: RoboRosewater and descendents
TODO: any info you can find on the relevant thesis

# Running the MTG Generative AI Project Today

Most of the projects above all coalesced aroung and drew from two projects: the
RNN model at [mtg-rnn](https://github.com/billzorn/mtg-rnn)
and a string encoding/decoding toolset at
[mtgencode](https://github.com/billzorn/mtgencode)
(which I guess could either parse as "Magic: the Gathering encode" or 
"Magic: the Gencode", but I digress).

I've prepared some instructions based on how I got things up and running, but
if they don't make sense, the [repo README](https://github.com/billzorn/mtgencode)
provides a set of high level instructions that you can use for additional
guidance (they're old, but you'll get it working if you assume errors are
workflow errors that you need to fix before moving on).

## py2 to py3

The first problem you'll have is that this project hasn't gotten a lot of
community attention lately, and hasn't since the Python2 deprecation. As a
result the linked script won't run as-is. You'll need to convert the python
scripting for [mtgencode](https://github.com/billzorn/mtgencode) from Python2
into Python3.

You can use [my fork](https://github.com/dsmith47/mtgencode-ds47) if you want
to skip this step, but in case you want to work from the base here are some
notes:
* Python supports a py2to3 tool that will automate most of the conversion
  of this repositorty.
* Using automated tooling will result in some tabs-to-spaces errors due to
  formatting in the script. IME python3 is pretty good about calling out these
  whitespace errors, but if you see a broken block that doesn't make sense,
  double-check for that.
* py2to3 doesn't seem to handle this script's use of `sorted()`` functions (py2 
  uses a `cmp` method while py3 just specifies the `key` to convert elements 
  into comparables).
* py2to3 doesn't handle the change in file writing strings vs. bytes (you can't
  simply write the output of `Str.encode()` anymore).
* My first decoding run on rnn output resulted in errors with script encoding,
  it appears that the output was only parseable in the `windows-1252` format.

## Access Training Data

TODO: notes on data source

## Encode Input and Run Code

TODO: explain commands for training the model

## Looking at the New Cards

TODO: tooling for making the text output legible
TODO: tooling that could be used to template a card