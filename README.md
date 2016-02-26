# bats-core

[![GitHub license](https://img.shields.io/badge/license-CC0-blue.svg)](https://raw.githubusercontent.com/ztombol/bats-core/master/LICENSE)
[![Build Status](https://travis-ci.org/ztombol/bats-core.svg?branch=master)](https://travis-ci.org/ztombol/bats-core)

`bats-core` is a supporting library providing common functions to test
helper libraries written for [Bats][bats].

Features:
- [output formatting](#output-formatting)

See the [shared documentation][bats-docs] to learn how to install and
load this library.

If you want to use this library in your own helpers or just want to
learn about its internals see the developer documentation in the [source
files](src).


## Output formatting

Many test helpers need to produce human readable output. This library
provides a simple way to format simple messages and key value pairs, and
display them on the standard error.


### Simple message

Simple messages without structure, e.g. one-line error messages, are
simply wrapped in a header and a footer to help them stand out.

```
-- ERROR: assert_output --
`--partial' and `--regexp' are mutually exclusive
--
```


### Key-Value pairs

Some helpers, e.g. [assertions][bats-assert], structure output as
key-value pairs. This library provides two ways to format them.

When the value is one line long, a pair can be displayed in a columnar
fashion called ***two-column*** format.

```
-- output differs --
expected : want
actual   : have
--
```

When the value is longer than one line, the key and value must be
displayed on separate lines. First, the key is displayed along with the
number of lines in the value. Then, the value, indented by two spaces
for added readability, starting on the next line. This is called
***multi-line*** format.

```
-- command failed --
status : 1
output (2 lines):
  Error! Something went terribly wrong!
  Our engineers are panicing... \`>`;/
--
```

Sometimes, for clarity, it is a good idea to display related values also
in this format, even if they are just one line long.

```
-- output differs --
expected (1 lines):
  want
actual (3 lines):
  have 1
  have 2
  have 3
--
```

<!-- REFERENCES -->

[bats]: https://github.com/sstephenson/bats
[bats-docs]: https://github.com/ztombol/bats-docs
[bats-assert]: https://github.com/ztombol/bats-assert
