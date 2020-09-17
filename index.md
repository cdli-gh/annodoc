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

[CoNLL-X]

    ~~~ conllx
    1    Dogs   dog    _    NNS    _    2    nsubj
    2    run    run    _    VBP    _    0    ROOT
    ~~~


~~~ conllx
1    Dogs   dog    _    NNS    _    2    nsubj
2    run    run    _    VBP    _    0    ROOT
~~~

The CoNLL-X format defines 10 columns separated by TAB, but only columns 1 (`ID`), 2 (`WORD`), 4 (`POS`), 7 (`HEAD`) and 8 (`EDGE`) are being used in the visualizations. Empty fields must be marked by _.

The [CoNLL-U] format is another CoNLL format format for representing dependency parses,
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

The CoNLL-U format defines 10 fields separated by TAB (in Annodoc: space):

 1. ID: Word index, integer starting at 1 for each new sentence; may be a range for tokens with multiple words.
 2. FORM: Word form or punctuation symbol.
 3. LEMMA: Lemma or stem of word form.
 4. CPOSTAG: Google universal part-of-speech tag from the [universal POS tag](http://universaldependencies.github.io/docs/u/pos/index.html) set.
 5. POSTAG: Language-specific part-of-speech tag; underscore if not available.
 6. FEATS: List of morphological features from the [universal feature inventory](http://universaldependencies.github.io/docs/u/feat/index.html) or from a defined language-specific extension; underscore if not available.
 7. HEAD: Head of the current token, which is either a value of ID or zero (0).
 8. DEPREL: [Universal Stanford dependency relation](http://universaldependencies.github.io/docs/u/dep/index.html) to the HEAD (root iff HEAD = 0) or a defined language-specific subtype of one.
 9. DEPS: List of secondary dependencies (head-deprel pairs).
10. MISC: Any other annotation.

For the complete documentation on the CoNLL-U format, please see
<http://universaldependencies.github.io/docs/format.html>.

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
