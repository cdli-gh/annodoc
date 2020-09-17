---
layout: entry
title: Dependency Syntax for Sumerian
---


## Table of contents

## Howto

### Formatting data samples

MTAAC annotations are originally provided in a CoNLL dialect. CoNLL is a family of tabular formats that feature
- one word per line
- within each line, a fixed number of tab-separated fields (columns)
- within each column, one type of annotation
- comments and headers marked by #
- sentences or documents separated by at least one empty line

CoNLL dialects differ with respect to the kind of annotation they provide and the order of columns. The Annodoc visualization provides partial support for two CoNLL dialects, CoNLL-X and CoNLL-U, with a focus on syntactic dependencies. Note that the original column structure of the data may require adjustments when used in this document. Also note that Annodoc supports space as column separator.

CoNLL-X

    ~~~ conllx
    1    Dogs   dog    _    NNS    _    2    nsubj
    2    run    run    _    VBP    _    0    ROOT
    ~~~


~~~ conllx
1    Dogs   dog    _    NNS    _    2    nsubj
2    run    run    _    VBP    _    0    ROOT
~~~

The CoNLL-X format defines 10 columns separated by TAB, but only columns 1 (`ID`), 2 (`WORD`), 4 (`POS`), 7 (`HEAD`) and 8 (`EDGE`) are being used in the visualizations. Empty fields must be marked by _.

The [CoNLL-U](http://universaldependencies.github.io/docs/format.html) format is another CoNLL format format for representing dependency parses,
developed in the 
[Universal Dependencies](universaldependencies.github.io/docs/)
project as a revision of the CoNLL-X format.

    ~~~ conllu
    # this is one sentence
    1    Dogs   dog    NOUN    NNS    _    2    nsubj    _    _
    2    run    run    VERB    VBP    _    0    ROOT     _    _
    
    # this is a second sentence
    1    Cats   cat    NOUN    NNS    _    2    nsubj    _    _
    2    sleep  sleep  VERB    VBP    _    0    ROOT     _    _
    ~~~

~~~ conllu
# this is one sentence
1    Dogs   dog    NOUN    NNS    _    2    nsubj    _    _
2    run    run    VERB    VBP    _    0    ROOT     _    _

# this is a second sentence
1    Cats   cat    NOUN    NNS    _    2    nsubj    _    _
2    sleep  sleep  VERB    VBP    _    0    ROOT     _    _
~~~

The CoNLL-U format defines 10 fields separated by TAB (in Annodoc: space), again, only fields 1 `ID`, 2 `WORD`, 4 `POS`, 7 `HEAD` and 8 `EDGE` are visualized.

As yet another alternative, the Stanford Dependency format can be used:

    ~~~ sdparse
    The quick brown fox jumped
    det(fox-4, The-1)
    amod(fox-4, quick-2)
    amod(fox-4, brown-3)
    nsubj(jumped-5, fox-4)
    ~~~

gives

~~~ sdparse
The quick brown fox jumped
det(fox-4, The-1)
amod(fox-4, quick-2)
amod(fox-4, brown-3)
nsubj(jumped-5, fox-4)
~~~

## Acknowledgements

This page is based on a fork of the [Annodoc](http://www2.lingfil.uu.se/SLTC2014/abstracts/sltc2014_submission_32.pdf) template, originally under (https://github.com/spyysalo/annodoc). See there for documentation.
