---
layout: entry
title: Dependency Syntax for Sumerian
---

## Table of contents
- [Status of this document](#status-of-this-document)
- [Background and General Information](#background-and-general-information)
- [Parts of Speech](#parts-of-speech)
- [Syntactic dependencies](#syntactic-dependencies)
	- [Root: root](#root-root)
	- [Incomplete annotation: dep](#incomplete-annotation-dep)
	- [Adjectival modifiers (amod)](#adjectival-modifiers-amod)
	- [Subordinate clauses: acl](#subordinate-clauses-acl)
	- [Subordinating conjunction: mark](#subordinating-conjunction-mark)
	- [Adpositions: case](#adpositions-case)
	- [Apposition: appos](#apposition-appos)
	- [List: list](#list-list)
	- [Nominal modifiers: nmod](#nominal-modifiers-nmod)
	- [Quantifiers: det](#quantifiers-det)
	- [Syntactic coordination: conj, cc](#syntactic-coordination-conj-cc)
	- [Punctuation: punct](#punctuation-punct)
	- [Grammatical roles (morphological case): ABS, ERG, DAT, ABL, ADV, COM, EQU, TERM, LOC, GEN](#grammatical-roles-morphological-case-abs-erg-dat-abl-adv-com-equ-term-loc-gen)
		- [Core arguments: ERG vs. ABS vs. nsubj vs. obj](#core-arguments-erg-vs-abs-vs-nsubj-vs-obj)
		- [Datives](#datives)
		- [Oblique arguments: LOC, TERM, ABL](#oblique-arguments-loc-term-abl)
		- [Adominal dependents: GEN, EQU](#adominal-dependents-gen-equ)
		- ["Functional obliques"](#functional-obliques)
		- [Case of headless phrases](#case-of-headless-phrases)
		- [Genitive case: GEN](#genitive-case-gen)
		- [Equative case: EQU](#equative-case-equ)
		- [Possession](#possession)
	- [Vocative: voc](#vocative-voc)
	- [Dislocation: +disloc](#dislocation-disloc)
	- [Numeral modifiers: nummod](#numeral-modifiers-nummod)
	- [Compound: compound](#compound-compound)
	- [Flat: flat](#flat-flat)
	- [Clausal complement: ccomp](#clausal-complement-ccomp)
	- [Adverbial clause: advcl](#adverbial-clause-advcl)
	- [Parataxis: parataxis](#parataxis-parataxis)
	- [Copula clauses: cop](#copula-clauses-cop)
- [Genre specifics](#genre-specifics)
	- [Scope of dates in Ditilas](#scope-of-dates-in-ditilas)
	- [Transactions and their participants](#transactions-and-their-participants)
	- [Units](#units)
	- [Discontinuous lists](#discontinuous-lists)
	- [Dates](#dates)
	- [Complex numerals](#complex-numerals)
	- [Detached totals](#detached-totals)
- [Changes](#changes)
- [Open issues](#open-issues)
	- [internal structure of functional dependents](#internal-structure-of-functional-dependents)
	- [complex dependencies](#complex-dependencies)
	- [nam-erim2-am3](#nam-erim2-am3)
	- [Suppliers and receivers](#suppliers-and-receivers)
	- [Multiple agents in a transaction](#multiple-agents-in-a-transaction)
	- [Discussion of Date structure](#discussion-of-date-structure)
	- [Dependency syntax: Other uses of the copula](#dependency-syntax-other-uses-of-the-copula)
	- [Hard examples](#hard-examples)
- [Mapping to UD](#mapping-to-ud)
- [How to edit this document](#how-to-edit-this-document)
	- [Formatting example annotations](#formatting-example-annotations)
- [Acknowledgements](#acknowledgements)
	- [Contributors](#contributors)
	- [References](#references)
- [Appendix](#appendix)
	- [List of compound verbs](#list-of-compound-verbs)

## Status of this document

Draft for annotation guidelines for syntax, under development. Currently documents the design decisions taken in the development of syntax pre-annotation tools. The goal is, however, to provide a full-fledged annotation scheme for Sumerian, a small gold corpus and its export to UD v.2 

Known issues/todos:
- inconsistent transcription principles (reflecting different sources for the examples), to be normalized according to CDLI conventions
- incomplete/heterogeneous schemata for POS annotation (reflecting different sources for the examples), to be normalized according to MTAAC conventions
- add overview of all tags
- add mapping to UD v.2
- add sources and literature
- add section on grammar in general
- add section on morphology
- add section on administative texts
- all analyses to be confirmed by an Assyriologist

## Background and General Information

Previous work on syntactic parsing of cuneiform languages is sparse. For Sumerian, we can only build on individual examples with syntactic analysis in the literature, documentation of pilot studies on query-based parsing and information extraction without code or data releases, and initial steps towards the semiautomatic creation of annotations in the Penn Treebank tradition, the Penn Parsed Corpus of Sumerian (PPCS, 2003-2004). At the moment, only about 400 tokens of syntactically annotated text are available from PPCS and its documentation.[^fn-PPCS]

[^fn-PPCS] The original website is down (http://psd.museum.upenn.edu/ppcs/), but cf. http://oracc.museum.upenn.edu/doc/help/languages/sumerian/syntax/index.html, https://github.com/oracc/oracc/tree/master/misc/ssa3/t (sample data),  https://web.archive.org/web/20121025205450/http://psd.museum.upenn.edu/ppcs/MorphologyTable.html,  https://web.archive.org/web/20130121075848/http://psd.museum.upenn.edu/ppcs/   

Sumerian language (also cf. [CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=writing_and_language), [Wikipedia](https://en.wikipedia.org/wiki/Sumerian_language))

* writing ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=cuneiform_writing_system))
	* orthography ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:orthography))
	* sign list ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=ur_iii_neo-sumerian_period))
* transliteration (see [CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:transliteration_and_the_diacritics))
	* CDLI-preferred readings ([CDLI](https://cdli.ucla.edu/methods/sign_reading.html))
* grammar
	* linguistic typology ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:typological_structure))
	* case ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:case))
	* gender ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:gender))
	* number ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:number))
	* verbal stems ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:verbal_stems))
	* pragmatics ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=sumerian:topic_marking))

* text types (see [CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=text_typologies))
	* letters ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=ur_iii_letters&s[]=verb))
	* receipts ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=ur_iii_receipts))
	* administrative archives ([CDLI legacy file](http://cdli.ox.ac.uk/wiki/doku.php?id=3rd_millennium_administrative_archives#ur_iii724_tags))
	* seal inscriptions ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=seal_inscriptions))
	* royal inscriptions ([ETSCRI](http://oracc.museum.upenn.edu/etcsri/))
	* literary texts (mythological, narrative, historical) ([ETCSL](http://etcsl.orinst.ox.ac.uk/))

* math and calendar
	* metrology ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=ur_iii_metrological_systems))
	* Ur III calendars ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=ur_iii_calendars))
	* year names (see [CDLI wiki](https://cdli.ucla.edu/tools/yearnames/yn_index.html))
		* [Ur-Namma](http://cdli.ox.ac.uk/wiki/doku.php?id=year_names_ur-namma)
		* [Shulgi](http://cdli.ox.ac.uk/wiki/doku.php?id=year_names_shulgi)
		* [Amar-Suen](http://cdli.ox.ac.uk/wiki/doku.php?id=amar-suen_year-names)
		* [Shu-Suen](http://cdli.ox.ac.uk/wiki/doku.php?id=year_names_shu-suen)
		* [Ibbi-Suen](http://cdli.ox.ac.uk/wiki/doku.php?id=year_names_ibbi-suen)

A characteristic feature of Sumerian is "Suffixanhäufung" (case stacking): the syntactic head of the noun phrase is typically its first element, but morphological case is marked at the last element of a phrase. If a noun phrase contains a nominal modifier, this tends to follow its syntactic head, and thus, the case markers of the dependent and of the head are accumulated at the modifier.

	ig   e2    lugal-ka-ta
	ig   e     lugal.ak.ak.ta
	door house king.GEN.GEN.ABL
	"From the door of the king's house" (PPCS manual, example 18)

Here, case morphology directly encodes a phrase structure:
	
	[ig   [e     lugal.ak].ak].ta
	[door [house king.GEN].GEN].ABL

We exploit this characteristic by grounding the annotation of syntax in the annotation of morphology. In particular, we use morphological cases as labels for nominal dependents. Annotation is thus reduced to propagate case to the respective syntactic head:

~~~conllu 
1	ig	_	door	_	_	0	ABL	_	_
2	e2	_	house	_	_	1	GEN	_	_
3	lugal-ka-ta	_	king.GEN.GEN.ABL	_	_	2	GEN	_	_
~~~

The mapping of case labels to universal dependency labels is performed as a postprocessing step. Adnominal modifiers with case marking are mapped to `nmod`, oblique cases are  to `obl`, dative to `iobj`, ergative to `nsubj`. The mapping of absolutive is more challenging, as it needs to be disambiguated between `nsubj` (for intransitives) and `obj` (for transitives), see discussion below.

Following the morphological principle in syntactic annotation, these labels are being used only if indicated in the morphology annotation. Morphologically unmarked adnominal modification is annotated as `appos`. The same principle applies to the annotation of clausal co(sub)ordination: Morphologically marked subordination is annotated as `acl`, morphologically or syntactically marked coordination as `conj`, unmarked co(sub)ordination as `parataxis`.

## Parts of Speech

See [Tagsets](https://cdli-gh.github.io/guides/guide_tagsets.html).
Mapping to UD yet to come.

## Syntactic dependencies

MTAAC aims to produce Ur III syntax according to the Universal Dependencies (UD 2018), along with semantic role annotations. One important deviation is that for clausal and nominal arguments, we apply the labels of morphological cases. In a subsequent processing step, these are transformed to UD labels. However, this is lossy, and internally, we work with case labels in order to facilitate their subsequent mapping to semantic role annotations. This document describes the MTAAC scheme and its mapping to UD, building in parts on the PPCS documentation.

MTAAC builds on ETSCRI-style morphosyntax. Unlike PPCS, we do not annotate morphemes. For labelling clausal arguments, MTAAC uses case labels as provided by ETSCRI-style morphosyntax, not the richer PPCS inventory. Unlike UD, the root node may carry a dependency relation other than root. In this way, morphological information can be preserved, e.g., in the examples below.

The annotation scheme is designed with the goal of mappability to UD v.2, however, the specifics of Sumerian require a language-specific schema. The mapping of native labels to UD dependencies is approached here as a post-processing task. 

As Sumerian employs morphology to mark syntactic relations, we adopt a morphology-driven (rather than a semantics-driven) approach to annotation. This does facilitate automated annotation, but entails the following modifications:

- co(sub)ordination: If subordination or coordination is not made explicit in the morphology annotation, we annotate appos (between a noun and its nominal dependents) or parataxis (between verbs [clauses])
- We use morphological annotations for case as labels for syntactic dependencies of nouns, with two exceptions: all locatives are marked LOC, all datives are marked DAT.
- Sumerian does not have the grammatical category ADJ. The label amod is used for relative clauses without clausal arguments. This also applies to all participles (morphologically, Sumerian relative clauses are participles or nominalizations).
- We annotate all subordinate clauses without `mark` as relative clauses (acl). If an adverbial function is evident from the morphology, this involves a case marker, and then a compound label acl+CASE is used. This means that we do not use the dependencies xcomp, and csubj; ccomp is used for direct speech, only. 
- Sumerian does not have the grammatical category ADV. Adverbials are modelled like adjectives, resp. relative clauses, with additional case marking. The dependency `advcl` is used for subordinate clauses whose `mark` indicates an adverbial function (like *tukumbi* "if").

### Root: root

The label `root` designates the top node of a syntax tree. In CDLI annotation, the top node can also carry other labels (for morphological case or syntactic subordination) if these are morphologically marked. For the UD mapping, these are to be replaced by `root`. In most cases, `root` is the main predicate, e.g., V; N.2-SG-POSS.ABS in sealing.

### Incomplete annotation: dep

Should be used for damaged or missing signs whose meaning cannot be ascertained.
In the gold data, dep should be used if a particular source doesn't define the syntactic relations of a particular fragment. This includes, for example, the internal structure of year names according to Jaworski (2009).

### Adjectival modifiers (amod)

(see [MTAAC’S Approach to Sumerian Morphology](https://cdli-gh.github.io/guides/guide_morphology.html))

The model of Sumerian morphology employed at MTAAC approximates that developed by Gabor Zólyomi, a model demonstrated at the ETCSRI project and articulated in Zólyomi’s 2017 grammar. Some conventions relating to word categorization and tag sets invite explanation: i) according to this model, Sumerian adjectives do not constitute a distinct word class. Instead, they are analyzed as non-finite verbal forms; ii) infinitives and participles, morphologically indistinct from other non-finite forms, are not distinguished; iii) a non-finite verbal form without a suffix is marked as tenseless (or absolute), and a null morpheme is supplied. Non-finite forms consisting of STEM + .a are marked as preterite. Non-finite forms consisting of STEM + .ed are marked as present-future. The following chart displays the relevent non-finite tags:

|Form      | ETCSRI        | Zolyomi 2017, 91| MTAAC     | Tense               |
|----------| ------------- |:-------------:  | --------: | -------------------:|
|  dug.ø   | NV2.N5        | stem-TL         | NF.V.ABS  |Tenseless            |
|  dug.a   | NV2.NV4       | stem-PT         | NF.V.PT   |Preterite            |
|  dug.ed  | NV2.NV3       | stem-PF         | NF.V.F    |Present-Future       |

In dependency syntax, these forms are given the label `amod` (if modifying a noun), but only if they carry no clausal arguments on their own. If they do, annotate them as subordinate clause `acl`. Likewise, relative clauses without arguments are annotated as `amod`, as they are morphologically indistinguishable from participles. All "adjectives" are nominalized verbs, and we follow the morphological analysis as to whether they are annotated as a amod or as appos. 

~~~ conllu
1	a	_	water	_	_	0	ABS	_	_
2	dug₃-ga	_	NF.V.PT.ABS	_	_	1	amod	_	_

~~~
“sweet water” (Q000377)

	# Jagersma, Chap. 27 (46)					
	# ‘the year that follows it’ ("next year")					
	# (NATN 109 15; N; 21)					
	1	mu	mu	year	0	root
	2	ab-ús-sa	'a-b-'ús-Ø-'a	VP-3N.OO-be.next.to-3N.S/DO-NOM	1	amod

Semantically, the following would be `acl` but as the verb has no overtly realized arguments, we consider that as `amod`.

	# Jagersma, Chap. 27 (65)						
	# ‘on to the field which he has seized’						
	# (TCS 1:229 7; L; 21)						
	1	a-šà	a.šà.g	field	0	LOC	marked on 2
	2	in-dab5-ba-na	'i-n-dab5-Ø-'a=ane='a	VP-3SG.A-seize-3N.S/DO-NOM=his=LOC	1	amod	no overt arguments, hence amod, not acl

If adjectives (including argument-less relative clauses) appear without nominal head, but with a grammatical role (morphological case) in a clause, use the morphological case for their annotation. Likewise, lexicalized deverbal nominals are annotated like nominal arguments. 

	# Jagersma, Chap. 27 (34)						
	# ‘one in which it is sieved for me’						
	1	gema-an-sim	Ø-ma-n(i)-sim-Ø	VP-1SG.IO-in-sieve-3N.S/DO	0	ABS	

Etymologically, this is a headless relative clause, but it is lexicalized as a noun; according to CDLI conventions, that is originally an `amod`, because it comes without arguments

	# Jagersma, Chap. 27 (36)						
	# ‘one who has died’						
	1	ba-úš	Ø-ba-'úš-Ø	VP-MM-die-3SG/3N.S/DO	0	ABS	

Etymologically, this is a headless relative clause, but it is lexicalized as a noun.

	# Jagersma, Chap. 27 (53)						
	# ‘on whose right and left lions were laying’						
	# (Cyl A 5:16; L; 22)						
	1	zi-da	zi.d-Ø-'a	be.right-NFIN-NOM	4	LOC	morphologically, this is amod+LOC
	2	gabu2-na	gabu2=ane='a	left=his=LOC	1	appos	
	3	piriĝ	piriĝ=Ø	lion=ABS	4	ABS	
	4	ì-nú-nú-a	'i-b(i)-nú-nú-Ø-'a	VP-3N:on-lie-lie-3N.S/DO-NOM	0	acl	

Titles or functionaries can be referred to with (lexicalized) nominalizations, and then, an annotation like a nominal (nmod or appos) would be preferrable. Here, we follow the decision taken in morphology annotation.

### Subordinate clauses: acl

`acl` is primarily applied to finite and non-finite clauses that modify a nominal. In CDLI, however, its annotation is guided by the morphological analysis, i.e., for `NF.V.ABS/PT/F`, `N-NF.V.ABS`, etc.

> The taglist also has `acl:relcl` for `SUB`. Confirm treatment in pre-annotation and whether this can be reliably extrapolated from annotation projection. Current suggestion is to use `acl` also in this case.

Usually, syntactic subordination is morphologically marked, e.g., by means of a nominalization marker. It is thus impossible to distinguish nominalized verbs and relative clauses. All nominalized verbs are annotated as relative clauses (acl, on the use of the amod in place of acl, see below). Several constructions can be distinguished: "full relative clauses" are fully inflected verbs with a nominalization marker (-a), "reduced relative clauses" (participial construction, Mesanepada construction) use uninflected verbs, with the addition of a nominalization marker (-a). The latter are formally identical with the passive participle.

Sumerian does not have a relative pronoun, but certain nominals can serve a similar function. For their analysis, we follow Hayes, p.10ff, 157:

~~~ conllu
1 Ur-{d}Nammu _ _ _ _ 0 root _ _
2 lugal... _ _ _ _ 1 appos _ _ 
3 lu2 _ _ _ _ 1 appos _ _
4 e2 _ _ _ _ 6 ABS _ _
5 {d}En-lil2-la2 _ _ _ _ 4 GEN _ _
6 id-du3-a _ _ _ _ 3 acl _ _
~~~
"Ur-Nammu, the king ..., (the man) who built the temple of Enlil" (Hayes 2000, p.10ff, 157)

Here, lu2 "man" is in apposition to the "matrix noun". The head of the relative clause is lu2. This analysis corresponds to a translation as "the man who built the temple of Enlil". Note that the Sumerian counterpart of "who" in this analysis is not lu2, but the nominalization marker -a in the verb.

Note that lu2 is not a function word, but a regular noun. Accordingly, it can also be understood literally:

~~~ conllu
1 lu₂ _ _ _ _ 7 ABS _ _
2 mu-sar-ra-ba _ _ _ _ 4 LOC _ _
3 šu _ _ _ _ 4 ABS _ _
4 bi₂-ib₂-uru₁₂-a _ _ _ _ 1 acl _ _
5 {d}bil₃-ga-meš₃-e _ _ _ _ 7 ERG _ _
6 nam _ _ _ _ 7 ABS _ _
7 ha-ba-da-kud-e _ _ _ _ 0 root _ _
~~~~
"The man [who erases this inscription] may be cursed by Gilgamesh!" (Q001642)

In this example, there is no other "matrix noun" except for lu2 "man".

Other words can serve similar functions, e.g. ud "day" for temporal clauses:

~~~ conllu
1	{d}bil₃-ga-meš₃	_	_	_	_	9	DAT	_	_
2	...	_	_	_	_	0	_	_	_
3	ud	_	_	_	_	9	LOC	_	_
4	e₂	_	_	_	_	6	ABS	_	_
5	{d}nanna	_	_	_	_	4	GEN	_	_
6	mu-du₃-a	_	_	_	_	3	acl	_	_
7	nam-til₃-la-ni-še₃	_	_	_	_	9	TERM	_	_
8	a	_	_	_	_	9	ABS	_	_
9	mu-na-ru	_	_	_	_	0	root	_	_

~~~~
"Gilgamesh ..., (on the day) when he built the temple of Nanna, for the sake of his life, dedicated (this vase)" (Q001642)

Head of the relative clause is ud "day", a locative argument (marked at the verb) of the main verb, literally thus "on the day that". Note that this is indeed a relative clause in Sumerian, not an adverbial clause as in English. The adverbial function is expressed by the case of the head noun (morphologically marked at the last element of the noun phrase, here, the verb).

Note that there is no inherent difference between subordinate clauses and adjectives. All adjectives are verbs. We thus annotate acl if a relative clause contains clausal arguments, but amod if it does not. The matter is complicated by "compound verbs", which are lexicalized noun-verb combinations with a verbal meaning, e.g., ki ang2 "beloved", literally "place-measuring". As long as the (diachronic) syntactic relation is transparent, these are annotated according to their syntactic function, and thus as acl, not as amod.

~~~ conllu
1	ur-{d}nin-ŋir₂-su	_	_	_	_	0	GEN	_	_
2	en	_	_	_	_	1	appos	_	_
3	ki	_	_	_	_	4	ABS	_	_
4	aŋ₂	_	_	_	_	2	acl	_	_
5	{d}nanše-ka-ke₄	_	_	_	_	2	GEN	_	_

~~~

"(of) Ur-Ningirsu, the beloved priest of Nanshe" (Q001758) 

At the same time, relative clauses are annotated as `amod`, not as `acl` if they have no overtly realized arguments. This includes verbs that translate into adjectives in English.

	# Jagersma, Chap. 27 (46)					
	# ‘the year that follows it’ ("next year")					
	# (NATN 109 15; N; 21)					
	1	mu	mu	year	0	root
	2	ab-ús-sa	'a-b-'ús-Ø-'a	VP-3N.OO-be.next.to-3N.S/DO-NOM	1	amod

However, this also includes verbs that translate into relative clauses in English if no overt arguments occur:

	# Jagersma, Chap. 27 (65)						
	# ‘on to the field which he has seized’						
	# (TCS 1:229 7; L; 21)						
	1	a-šà	a.šà.g	field	0	LOC	marked on 2
	2	in-dab5-ba-na	'i-n-dab5-Ø-'a=ane='a	VP-3SG.A-seize-3N.S/DO-NOM=his=LOC	1	amod	no overt arguments, hence amod, not acl

Note that headless relative clauses can be clausal arguments, and should be marked with the corresponding case:

~~~ conllu
1	2(barig)	_	_	_	_	2	nummod	_	_
2	kasz	_	_	_	_	17	parataxis	_	_
3	elam	_	_	_	_	4	ABL	_	_
4	ki-masz{ki}-me	_	_	_	_	2	acl+DAT	_	_

~~~
"120 liter beer for those (slaves) from Elam" (P315784)

elam ki-masz{ki}-me carries a copula and is thus analyzed as a predicate here.

Note that our definition of "headless relative clause" differs from that of Jagersma (2010), who states that headless relative clauses occur only in lexicalized nominals. This is because a syntactic head realized as morphological argument argument is *not* considered an overt head in dependency annotation. In the following example, the head is realized in the morpheme *-en*, but not as an individual token:

	# Jagersma, Chap. 27 (70)					
	# ‘you, who will build my temple for me’					
	# (Cyl A 9:8; L; 22)					
	1	é-ĝu10	é=ĝu=Ø	house=my=ABS	2	ABS
	2	ma-řú-na	Ø-ma-řú-en-'a	VP-1SG.IO-erect-2SG.S/A:IPFV-NOM	0	acl

Headless relative clauses are relative clauses that serve a nominal function, e.g., by carrying a case marker that cannot be propagated to a nominal head. These are annotated with `acl+CASE` for the respective case.

This includes core arguments:

	# Jagersma, Chap. 5 (23)						
	# ‘the one given strength by Ningirsu’						
	# (ergative) (Ean.11 1:7-8; L; 24)						
	1	á	á=Ø	strength=ABS	2	ABS	
	2	šúm-ma	šúm-Ø-'a	give-NFIN-NOM	0	acl+ERG	marked on 4
	3	/	_	_	2	punct	
	4	{d]nin-ĝír-su-ke4	nin.ĝír.su.k=ak=e	Ningirsu=GEN=ERG	2	GEN	

With an explicit head such as *lu* "man", this would be

	[*lu <-acl- a szumma ningirsuke ] -ERG-> ...

This also includes oblique arguments:

	# Jagersma, Chap. 27 (28)					
	# ‘When the ruler stayed in the Emi, this was brought to the Emi.’					
	# (DP 164 3:5-9; L; 24)					
	1	ensi2	ensi2.k=Ø	ruler=ABS	5	ABS
	2	/	_	_	5	punct
	3	é-mí-a	é.mí='a	Emi=LOC	5	LOC
	4	/	_	_	5	punct
	5	mu-ti-la-a	Ø-mu-n(i)-ti.l-Ø-'a='a	VP-VENT-in-live-3SG.S/DO-NOM=LOC	9	acl+LOC
	6	/	_	_	9	punct
	7	é-mí-šè	é.mí=še	Emi=TERM	9	TERM
	8	/	_	_	9	punct
	9	ba-ře6	Ø-ba-ře6-Ø	VP-MM-bring-3N.S/DO	0	root

With an explicit head such as *ud* "day", this would be

	[*ud <-acl- ensi emia mutila emisze bare ] -LOC-> ...

Analoguously for other cases:

	# Jagersma, Chap. 5 (18)					
	# ‘of (the fact) that Anumu had paid barley’					
	# (NG 127 14; U; 21)					
	1	a-na-ĝu10	a.na.ĝu10=e	Anamu=ERG	3	ERG
	2	[š]e	še=Ø	barley=ABS	3	ABS
	3	áĝ-a	áĝ-Ø-'a=ak	measure.out-NFIN-NOM=GEN	0	acl+GEN

	# Jagersma, Chap. 5 (19)					
	# ‘for buying bitumen’					
	# (MVN 16:1257 obv 1; U; 21)					
	1	esir2-ra	esir2='a	bitumen=LOC	2	LOC
	2	sa10-sa10-dè	sa10:RDP-ed-Ø=e	barter:IPFV-IPFV-NFIN=DIR	0	acl+DIR

	# Jagersma, Chap. 5 (20)					
	# ‘when the ruler stayed in the Emi’					
	# (DP1643:5-7; L;24)					
	1	ensi2	ensi2.k=Ø	ruler=ABS	5	ABS
	2	/	_	_	5	punct
	3	é-mí-a	é.mí='a	Emi=LOC	5	LOC
	4	/	_	_	5	punct
	5	mu-ti-la-a	Ø-mu-n(i)-ti.l-Ø-'a='a	VP-VENT-in-live-3SG.S/DO-NOM=LOC	0	acl+LOC

Note that these are not limited to adverbial (spatio-temporal) interpretations: 

	# Jagersma, Chap. 5 (25)					
	# ‘what Ningirsu has agreed with Irikagena’					
	# (locative) (Ukg.34 1; L; 24)					
	1	{d}nin-ĝír-sú-ke4	nin.ĝír.su.k=e	Ningirsu=ERG	3	ERG
	2	iri-ka-ge-na-da	iri.ka.ge.na.k=da	Irikagena=COM	3	COM
	3	e-da-du11-ga-a	'i-n-da-n-du11.g-Ø-'a='a	VP-3SG-with-3SG.A-say-3N.S/DO-NOM=LOC	0	acl+LOC



Note that headless relative clauses include cases with absolutive case (which is morphologically unmarked):

~~~ conllu
1	PN1	_	PN	_	_	4	ERG	_	_
2	dam-ce3	_	wife.TERM	_	_	3	TERM	_	_
3	ha-tuku	_	have	_	_	4	ccomp	_	_
4	bi2-in-dug4-ga	_	say.NOM	_	_	7	acl+ABS	_	_
5	PN2	_	PN	_	_	7	ABS	_	_
6	PN3	_	PN	_	_	5	appos	_	_
7	nam-erim2-am3	_	swear.COP	_	_	0	root	_	_

~~~

"PN  (and) PN  swore that PN  declared: 'I will marry (her)'" (NG 15:6-9, 16:6-11, example from PPCS manual)

	# Jagersma, Chap. 27 (72)						
	# ‘These (beams) are what went in from the House of Mekulabata's Hill.’						
	# (DP 438 2:2-3; L; 24)						
	1	é	é	house	5	ABL	
	2	du6	du6	hill	1	GEN	
	3	me-kul-ab{ki}-ta-ka-ta	me.kul.ab4.ta=ak=ak=ta	Mekulabata=GEN=GEN=ABL	2	GEN	
	4	/	_	_	5	punct	
	5	ì-ku(DU)-a-am	'i-n(i)-ku4.ř-Ø-'a=Ø='am	VP-in-enter-3N.S/DO-NOM=ABS=be:3N.S	0	acl+ABS

Note that CDLI annotates adverbial clauses without `mark` as relative clauses. We follow a morphology-driven approach to syntax annotation and mark syntactic subordination along with the case of the constituent. If a subordinate clause is headless (and also lacking a "relative pronoun" such as lu2), we mark it as acl+CASE. The adverbial function is not expressed in the subordination, but in the morphological case. While the use of `advcl` and `advmod` is limited in CDLI annotation, these are derived for the UD export as follows:
	
	acl+LOC, TERM, EQU, etc. => advcl
	acl+GEN => acl (modifying a noun)
	acl => acl (in apposition with a noun)

In the following example, an adverbial interpretation of the clause is morphologically expressed by `DIR`. Subordination is not overtly marked, but inferred from the application of a nominal case to a finite clause, hence annotated as `acl+DIR`:

	# Jagersma, Chap. 27 (32)						
	# ‘that a stranger had slept with her without Ur-Lama, (her) husband, knowing it’						
	# (NG 205 21-22; L; 21)						
	1	ur-dlama3	ur.lama3	Urlama	3	ERG	
	2	dam-e	dam=e	husband=ERG	1	appos	
	3	nu-ù-zu-bé	nu='i-n-zu-Ø=be=e	NEG=VP-3SG.A-know-3N.S/DO=its=DIR	6	acl+DIR	acl inferred from clausal
	4	/	_	_	6	punct	
	5	lú-kúr	lú.kúr=Ø	stranger=ABS	6	ABS	
	6	in-da-nú-a	'i-n-da-nú-Ø-'a	VP-3SG-with-lie-3SG.S/DO-NOM	0	acl	

As for `acl+ABS`, `acl+ERG` and `acl+DAT`, these are systematically ambiguous between nominal (UD `nsubj`, `obj`, `iobj`) and clausal interpretation (UD `csubj`, `ccomp`, `xcomp`) and asserting one would be artificial and not grounded in Sumerian grammar. If subordination is morphologically marked, the UD label is thus always chosen in accordance with their case (i.e., nominal interpretation). The UD labels `csubj` and `xcomp` are not being used in CDLI, `ccomp` is restricted to direct speech.

Note that syntactic annotation is morphology-driven. If subordination is not marked in the morphological annotation, we resort to parataxis. Note that subordination morphemes may have gone unwritten (e.g., because of assimilation processes or deficiencies of the writing), but if (unambiguously) so, we expect them to be restored in the morphological annotation.

In year names, `acl` should be used for the syntactic relation between *mu* "year" and the year name. Although this is often not morphologically marked, there are examples that use a nominalizer here:

	# Jagersma, Chap. 5 (46)					
	# ‘the year that Huhnure was destroyed’					
	# (BE 3/1:4 16; N; 21)					
	1	mu	mu	year	0	LOC
	2	hu-ùh-nu-reki	hu.ùh.nu.re=Ø	Huhnure=ABS	3	ABS
	3	ba-hulu-a	Ø-ba-hulu-Ø-'a	VP-MM-destroy-3N.S/DO-NOM	1	acl

Example without morphological marking:

~~~ conllu
1	iti	_	month	_	_	3	date	_	_
2	a2-ki-ti	_	Akiti	_	_	1	appos	_	_
3	mu	_	year	_	_	1	LOC	_	_
4	an-sza-an{ki}	_	Anshan	_	_	5	ABS	_	_
5	ba-hul	_	destroyed	_	_	3	acl	_	_

~~~	
(P109483)

~~~ conllu
1	iti	iti[month]	NOUN	N	Number=Sing	0	date	_	_
2	ses-da-gu7	Sesdagu[1]	PROPN	MN	Number=Sing	1	appos	_	_
3	mu	mu[year]	NOUN	N	Number=Sing	1	LOC	_	_
4	{d}gu-za	guza[chair]	NOUN	N	Number=Sing	6	ABS	_	_
5	{d}en-lil2-la2	Enlil[1]	PROPN	DN	Animacy=Hum|Case=Gen,Abs|Number=Sing	4	GEN	_	_
6	ba-dim2	dim[create]	VERB	V	Number=Sing|Person=3|Voice=Mid	3	acl	_	_

~~~
(P102313)

TODO: check all `ccomp` in the data whether to be replaced by `acl`.

### Subordinating conjunction: mark

Subordinate markers (CNJ). According to Jagersma (2010:82), "[t]here are three subordinating conjunctions, en-na ‘until’, u4-da ‘if’, and tukum-bé ‘if’".

TODO: change to CDLI transcriptions, e.g., *tukumbi* 'if', ...

~~~ conllu
1	lugal-ju10	lugal	king	_	_	7	ERG	_	_
2	tukum-bi	tukum-bi	if	_	_	5	mark	_	_
3	ud-da	ud	day(light)	_	_	5	LOC	_	_
4	kur-ra	kur	land	_	_	5	LOC	_	_
5	i-ni-in-ku4-ku4-de3	kur9	enter	_	_	7	advcl	_	_
6	{d}utu	utu	Utu	_	_	7	COM	_	_
7	he2-me-da-an-zu	zu	know	_	_	0	root	_	_

~~~
"If you (have to) enter the mountain, you should inform Utu (of it)" (example from PPCS manual)

	# Jagersma, Chap. 27 (56)					
	# ‘seed barley, as much as Ur-Kush-Bau calls for’					
	# (AuOr 17-18,218 1 4-5; L; 21)					
	1	še-numun	še.numun	seed.barley	0	root
	2	ur-dkuš7-dba-ú-ke4	ur.kuš7.ba.ú.k=e	Ur.Kush.Bau=ERG	6	ERG
	3	/	_	_	6	punct
	4	en-na	en.na	until	6	mark
	5	gù	gù=Ø	voice=ABS	6	ABS
	6	ba-dé-a	ba-dé-e-'a	3N.IO-pour-3SG.A:IPFV-NOM	1	acl

	# Jagersma, Chap. 15 (30)					
	# ‘if he says “I have no barley”’					
	# (TCS 1:157 7; L; 21)					
	1	u4-da	u4.da	if	3	mark
	2	še	še=Ø	barley=ABS	3	ABS
	3	nu-tuku	nu='i-'-tuku-Ø	NEG=VP-1SG.A-have-3N.S/DO	4	ccomp
	4	íb-bé	'i-b-'e-e	VP-3N.OO-say:IPFV-3SG.A:IPFV	0	root


TODO: clarify whether `CNJ` in morphology can reliably distinguish coordinating and subordinating conjunctions
TODO: list coordinating and subordinating conjunctions

Note that not every expression that translates into a subordination markers in English is to be annotated as such. In *mu ...=ak-sze* "because", this is literally "for[*-sze*/`TERM`] the name [*mu*] of [*-ak*/`GEN`] that (= dependent relative clause)".

	# Jagersma, Chap. 27 (25)						
	# ‘because he had been killed and the estate was destroyed’						
	# (MVN 2:2 case 3; L; 21)						
	1	mu	mu	name	0	TERM	mu ...=ak=sze => because, marked on 5
	2	ba-gaz	Ø-ba-gaz-Ø	VP-MM-kill-3SG.S/DO	1	acl+GEN	marked on 5
	3	é	é=Ø	house=ABS	4	ABS	
	4	hulu-a	hulu-Ø-'a	destroy-NFIN-NOM	2	parataxis	copular predicate, actually, this is a relative clause
	5	ì-me-a-šè	'i-me-Ø-'a=ak=še	VP-be-3N.S-NOM=GEN=TERM	4	cop	



### Adpositions: case

Sumerian does not have prepositions, but it does have a number of nouns that are used to express prepositional functions, e.g., sza3 "heart", also used for to express the meaning of the preposition "in". These are annotated in accordance with their morphology, i.e., as nouns with genitive complement. If no additional case is marked in the morphology annotation, these phrases are considered to be in apposition with the nominal they modify.

~~~ conllu
1	sza3	szag[heart]	N	_	_	0	LOC	_	_
2	ma-da	mada[land]	N	_	_	1	GEN	_	_
3	gir2-su{ki}	Girsu[1][-ak][-ak][-'a]	SN.GEN.GEN.L1	_	_	2	GEN	_	_
4	ugula	ugula[overseer][-ø]	N.ABS	_	_	5	nmod	_	_
5	a-a-kal-la	Ayakala[1]	PN	_	_	1	ABS+orphan	_	_
6	szusz3	kusz[cattle_manager][-ø]	N.ABS	_	_	5	appos	_	_

~~~
"In (= at the heart of) the land of Girsu, overseer Ayakala, cattle manager" (P356065)

This is part of the summary section of an administrative text, with the semantic predicate ("attested by", or "registered by") left implicit (hence the orphan relation). Note that the locative function does not arise from the use of sza3 in a locative sense, but from the morphological analysis of the last word of the noun phrase. Also note that the locative morpheme -'a is not actually written in the surface string, as case marking in administrative texts is often defective.

Note that the construction can also be understood literally:

~~~ conllu
1	šag₄	_	heart	_	_	6	ERG	_	_
2	en-lil₂-la₂-ke₄	_	DN=GEN=ERG	_	_	1	GEN	_	_
3	id2idigna-am₃	_	WN=STM	_	_	1	acl	_	_
4	a	_	water	_	_	6	ABS	_	_
5	dug₃-ga	_	sweet-PT=ABS	_	_	4	amod	_	_
6	nam-de₆	_	MOD-VEN-3.SG.NH.A-bring-3.SG.P	_	_	0	root	_	_

~~~
“The heart of the god Enlil brought sweet water like the river Tigris.” (Q000377)

As these constructions are analyzed in accordance with their morphology rather than their semantic interpretation in English, the UD label "case" is not used for Sumerian.

### Apposition: appos

Sumerian syntax annotation is morphology-driven. If an adnominal noun does not morphologically or syntactically mark its relation with its head, it is marked as appos. Appositions are widely used and cover interpretations such as implicit identity, implicit coordination, implicit meronymy, implicit genitive, implicit equative or implicit copula.

implicit identity

~~~ conllu
1	an	_	_	_	_	0	DAT	_	_
2	lugal	_	_	_	_	1	appos	_	_
3	diŋir-re-ne	_	_	_	_	2	GEN	_	_
4	lugal-a-ni	_	_	_	_	1	appos	_	_

~~~
"An, king of the gods, his king" (Q000937)

Implicit identity can be made explicit with a copula or equative (see below).

implicit conjunction

~~~ conllu
1	lugal	_	_	_	_	0	appos	_	_
2	ki-en-gi	_	_	_	_	1	GEN	_	_
3	ki-uri-ke₄	_	_	_	_	2	appos	_	_

~~~
"king of Sumer (and) Akkad" (Q000953)

Implicit conjunction can be made explicit with a conjunction:

	# Jagersma, Chap. 5 (82a)					
	# ‘prebendal and rented land (lit. “land of prebend and rent”)’					
	# (STH 1:40 4:9; L; 24)					
	1	gana2	gana2	land	0	root
	2	šuku	šuku.ř	prebend	1	GEN
	3	apin-lá	apin.lá=ak	rent=GEN	2	appos

	# Jagersma, Chap. 5 (82b)					
	# ‘prebendal and rented land’					
	# (MVN 6:309 rev 1:14; L; 22)					
	1	gana2	gana2	land	0	root
	2	šuku	šuku.ř	prebend	1	GEN
	3	ù	ù	and	1	cc
	4	apin-[lá]	apin.lá=ak	rent=GEN	1	conj

Implicit conjunction also covers cases of implicit disjunction:

	# Jagersma, Chap. 5 (84)					
	# ‘They did not pass two or three days with him.’					
	# (Cyl A 23:2; L; 22)					
	1	u4	u4.d	day	5	ABS
	2	2	2	2	1	nummod
	3	u4	u4.d	day	1	appos
	4	3	3=Ø	3=ABS	3	nummod
	5	nu-ma-da-ab-zal	nu='i-m(u)-ba-n-da-b-zal-Ø	NEG=VP-VENT-MM-3SG-with-3N.A-pass-3N.S/DO	0	root
	
Note that explicit disjunction is clausal, not adnominal: It uses a modal form of the verb *me* "be" (Jagersma 2010, p. 100). In those cases, annotate `parataxis`:

	# Jagersma, Chap. 5 (85)					
	# ‘whether he be a lamentation priest, or a brewer, or a steward, or an overseer: when he paid a silver tax for (lit. “placed on”) the fleece of a semi-weaned lamb’					
	# (Ukg. 1 4:26-31; L; 24)					
	1	[...]	_	_	4	dep
	2	/	_	_	4	punct
	3	gala	gala=Ø	lamentation.priest=ABS	4	ABS
	4	hé-ĝá-a	ha='i-m(e)-Ø	MOD=VP-be-3SG.S	0	root
	5	/	_	_	4	punct
	6	lú-bappir3	lú.bappir3.k=Ø	brewer=ABS	7	ABS
	7	[hé]	ha='i-m(e)-Ø	MOD=VP-be-3SG.S	4	parataxis
	8	/	_	_	7	punct
	9	agrig	agrig=Ø	steward=ABS	10	ABS
	10	hé	ha='i-m(e)-Ø	MOD=VP-be-3SG.S	7	parataxis
	11	/	_	_	10	punct
	12	ugula	ugula=Ø	overseer=ABS	13	ABS
	13	hé	ha='i-m(e)-Ø	MOD=VP-be-3SG.S	10	parataxis
	14	/	_	_	4	punct
	15	bar	bar	fleece	20	LOC
	16	sila4	sila4	lamb	16	GEN
	17	gaba-ka-ka	gaba=ak=ak='a	breast=GEN=GEN=LOC	16	GEN
	18	/	_	_	4	punct
	19	kù	kù.g=Ø	silver=ABS	20	ABS
	20	a-ĝá-ĝá-a	'a-b(i)-ĝar:RDP-e-'a='a	VP-3N:on-place:IPFV-IPFV.3SG.A-NOM=LOC	4	acl+LOC

Note that implicit conjunction also covers cases of implicit meronymy as in the following examples:

	# Jagersma, Chap. 27 (76)						
	# ‘In Bazizi’s house there is one chariot with two ... It is so that my man saw it.’						
	# (FAOS 19 Ad 8 9-12; A; 23)						
	1	é	é	house	9	LOC	
	2	ba-zi-zi-ka	ba.zi.zi=ak='a	Bazizi=GEN=LOC	1	GEN	
	3	/	_	_	9	punct	
	4	1	1	1	4	nummod	
	5	ĝišgigir2	gigir2	chariot	9	ABS	marked on 7
	6	é-UMBINxLU	é.UMBINxLU	??	5	appos	implicit conjunction (meronymy)
	7	2	2=Ø	2=ABS	6	nummod	
	8	/	_	_	9	punct	
	9	al-ĝál	'a-ĝál-Ø	VP-be.there-3N.S/DO	0	root	
	10	/	_	_	9	punct	
	11	lú-ĝu10	lú=ĝu=e	man=my=ERG	13	ERG	
	12	igi	igi=Ø	eye=ABS	13	ABS	
	13	im-mi-du8-àm	'i-m(u)-bi-n-du8-Ø='am	VP-VENT-3N.OO-3SG.A-spread-3N.S/DO=be:3N.S	9	parataxis	

	# Jagersma, Chap. 5 (48)					
	# ‘his seven-cornered house (lit. “his seven-corners house”)’					
	# (St D 2:11; L; 22)					
	1	é	é	house	0	ABS
	2	ub	ub	corner	1	appos
	3	imin-na-né	imin=ane=Ø	seven=his=ABS	2	nummod

	# Jagersma, Chap. 5 (49)					
	# ‘the Samana-demon (having) the mouth of a lion’					
	# (Studies Borger p.73 2; ?; 21)					
	1	sa-ma-na	sa.ma.na	Samana	0	root
	2	ka	ka.g	mouth	1	appos
	3	piriĝ-ĝá	piriĝ=ak	lion=GEN	2	GEN

implicit genitive or equative
~~~ conllu
1	kišib₃	_	_	_	_	6	ABL	_	_
2	ur-dšul-pa-e₃-ka	_	_	_	_	1	GEN	_	_
3	bešeŋ	_	_	_	_	5	LOC	_	_
4	ur-dba-u₂-ka	_	_	_	_	3	appos	_	_
5	i₃-in-ŋal₂-la-ta	_	_	_	_	1	acl	_	_
6	tur-re-dam	_	_	_	_	0	root	_	_

~~~
“These (various animals) are to be subtracted from the sealed tablet of Uršulpae that is in the basket of Urbau.” (P113923)

The overt morphology (according to annotation) of ur-dba-u₂-ka provides the locative marker, but the genitive remains implicit. As for the annotation of implicit genitives as `appos` or `GEN`, we rely on morphology annotation. If the genitive is restored in morphology annotation, the dependency will be labelled GEN.

The pattern applies to both adnominal cases, i.e., `GEN` and `EQU`. Note that equatives forms nominal sentences, an implicit equative can thus always also be interpreted as implicit copula. We thus do not annotate implicit equatives as such. Instead, apply the annotation of implicit copula.

implicit copula
~~~ conllu
1	{d}amar-{d}suen	_	_	_	_	0	ABS	_	_
2	ki	_	_	_	_	3	ABS	_	_
3	aŋ₂	_	_	_	_	1	acl+appos	_	_
4	urim₅{ki}-ma	_	_	_	_	3	GEN	_	_

~~~
"Amar-Suen, beloved of Ur" (name of a statue, Q000985)

This can also be interpreted as having an implicit copula (expected to be marked at 20, cf. Hayes 2000). An alternative annotation is as implicit copula. When annotating a text with a given translation, follow the interpretation of the translation:

~~~ conllu
1	{d}i-bi2-	_	Ibbi-	_	_	8	voc	_	_
2	{d}zuen	_	Suen	_	_	1	flat	_	_
3	...	_	...	_	_	1	appos	_	_
4	da-da	_	Dada	_	_	8	ABS	_	_
5	ensi2	_	ensi	_	_	4	appos	_	_
6	nibru{ki}	_	of.Nippur	_	_	4	GEN	_	_
7	...	_	...	_	_	4	appos	_	_
8	arad2-zu	_	servant	_	_	0	root	_	_

~~~
"Ibbi-Suen, ..., Dada, ensi of Nippur, ..., is your servant." (Hayes p. 274, Ibbi-Sin 7)

Implicit equatives also include (implicit) modification:

	# Jagersma, Chap. 5 (50)					
	# ‘for two two-year-old cows (lit. “two two-years cows”)’					
	# (MVN 18:130 5; D; 21)					
	1	2	2	2	2	nummod
	2	áb	áb	cow	0	TERM
	3	mu	mu	year	2	appos
	4	2-šè	2=še	two=TERM	3	nummod


Note that implicit addition in complex numerals is *not* annotated by `appos`, but by `nummod`:

~~~ conllu
1	3(gesz2)	3(gesz)[sixty]	NUM	NU	_	4	nummod	_	_
2	1(u)	1(u)[ten]	NUM	NU	_	1	nummod	_	_
3	7(disz)	7(disz)[one]	NUM	NU	_	1	nummod	_	_
4	udu	udu[sheep]	NOUN	N	Number=Sing	0	root	_	_

~~~
"197 (180+10+7) sheep" (P102315)

Appositions and most case-marked nominal dependents are post-modifying, i.e., the syntactic head of a noun phrase should be its first element. For exceptions to this rule established on semantic grounds (epithets/titles and units), premodifying nominals are marked as `nmod`.

Note that `appos` is overloaded and may require disambiguation. If an element is head of both an identity-marking apposition and a conjunction-marking apposition, it is recommended to use `list` for implicit conjunction. This is a very frequent pattern in administrative texts, but also occurs in contracts:

~~~ conllu
1	a-gu-a	_	Agua,	_	_	17	ABS	_	_
2	ugula-gesz2-da	_	the overseer of a crew of 60 men	_	_	1	appos	_	_
3	a-da-mu	_	Adamu,	_	_	1	list	_	_
4	dumu	_	the son	_	_	3	appos	_	_
5	x-x	_	of X,	_	_	4	GEN	_	_
6	szu-a-ba	_	Shu-Aba,	_	_	1	list	_	_
7	a-zu	_	the physician,	_	_	6	appos	_	_
8	im-ti-dam	_	Imtidam,	_	_	1	list	_	_
9	aszgab	_	the leather worker,	_	_	8	appos	_	_
10	a2-bi2-a-ti	_	Abiati,	_	_	1	list	_	_
11	szu-e2-a	_	Shuea,	_	_	1	list	_	_
12	dumu	_	the son	_	_	11	appos	_	_
13	EDIN-szi-la-at	_	of Edenshilat,	_	_	12	GEN	_	_
14	da-a-da-a	_	and Dada,	_	_	1	list	_	_
15	dumu	_	the son	_	_	14	appos	_	_
16	a-hu-szu-ni	_	of Ahushuni	_	_	15	GEN	_	_
17	lu2-inim-ma-bi-me-esz2	_	are the relevant witnesses	_	_	0	parataxis	_	_

~~~
"Agua the overseer of a crew of 60 men, Adamu, the son of X, Shu-Aba the physician, Imtidam the leather worker, Abiati, Sguea, the son of Edenshilat, and Dada, the son of Ahushuni, are the relevant witnesses." (P123217)

In rare cases, a phrase in a longer sequence of complex appositions may copy the case marker of its head although it does not mark the end of the phrase. 

According to Jagersma (2010:92), "if the head is followed by two or more appositions, the case marker is sometimes placed after every apposition and thus repeated several times. This happens chiefly when the number of appositions is particularly large. Take, for instance, the following example, which gives only the first two appositions out of a series of twelve, all of them with an ergative case marker:"

	# Jagersma, Chap. 5 (29)						
	# ‘Eannatum, the ruler of Lagash, the one nominated by Enlil, (...)’						
	# (Ean.3 1:7-3:5; L; 25) The noun phrase and its parts 93						
	1	é-an-na-túm	é.an.na.túm	Eannatum		ERG	marked on 5 and 10
	2	/	_	_	1	punct	
	3	ensi2	ensi2.k	ruler	1	appos	
	4	/	_	_	3	punct	
	5	lagas{ki}-ke4	lagas=ak=e	Lagash=GEN=ERG	3	GEN	
	6	/	_	_	1	punct	
	7	mu	mu=Ø	name=ABS	7	ABS	
	8	pà-da	pà.d-Ø-'a	call-NFIN-NOM	1	acl	(not acl+ERG)
	9	/	_	_	8	punct	
	10	{d}en-líl-ke4	en.líl=ak=e	Enlil=GEN=ERG	8	GEN	

	# Jagersma, Chap. 5 (57)					
	# ‘An, Enlil, (fifteen other gods), and my personal god Ningishzida’					
	# (St B 8:44-9:4; L; 22)					
	1	an-e	an=e	An=ERG	0	ERG
	2	/	_	_	1	punct
	3	den-líl-e	en.líl=e	Enlil=ERG	1	appos
	4	/	_	_	1	punct
	5	(...)	_	_	1	dep
	6	/	_	_	1	punct
	7	diĝir-ĝu10	diĝir=ĝu	god=my	8	nmod
	8	dnin-ĝiš-zi-da-ke4	nin.ĝiš.zi.da.k=e	Ningishzida=ERG	1	appos

In such cases, annotate `appos` *despite the morphology*. Note that automated annotation will most likely represent such cases as multiple independent arguments with the same role. For dependencies other than `LOC`, all cases of verbs with multiple dependencies of the same type must be manually inspected.

### List: list

The `list` relation holds between entitites of the same kind and expresses the meaning of an implicit conjunction. We anticipate two main applications. 
In administrative texts, lists of commodities which are not marked by an explicit conjunction should be connected by `list`, not by `appos`.

~~~ conllu
1	83	_	83	_	_	2	nummod	_	_
2	gud	_	bulls	_	_	0	root	_	_
3	niga	_	barley-fattened	_	_	2	appos	_	_
4	32	_	32	_	_	5	nummod	_	_
5	gud	_	bulls	_	_	2	list	_	_
6	u2	_	grass-fattened	_	_	5	appos	_	_
7	...	_	...	_	_	2	list	_	_

~~~
"83 barley-fattened bulls, 32 grass-fattened bulls, ..." (no CDLI, Kang 252, Hayes 2000, p. 367)

Note that `list` should *not* be used to connect transactions. We assume that transactions are inherently sentential, so, use `parataxis`.

Another use of `list` is as a means to disambiguate identity-marking and conjunction-marking apposition in a series of entities of the same kind: 
If an element is head of both an identity-marking apposition and a conjunction-marking apposition, it is recommended to use `list` for implicit conjunction. The commodity-linking function is an instance of this pattern, but this also occurs in contracts:

~~~ conllu
1	a-gu-a	_	Agua,	_	_	17	ABS	_	_
2	ugula-gesz2-da	_	the overseer of a crew of 60 men	_	_	1	appos	_	_
3	a-da-mu	_	Adamu,	_	_	1	list	_	_
4	dumu	_	the son	_	_	3	appos	_	_
5	x-x	_	of X,	_	_	4	GEN	_	_
6	szu-a-ba	_	Shu-Aba,	_	_	1	list	_	_
7	a-zu	_	the physician,	_	_	6	appos	_	_
8	im-ti-dam	_	Imtidam,	_	_	1	list	_	_
9	aszgab	_	the leather worker,	_	_	8	appos	_	_
10	a2-bi2-a-ti	_	Abiati,	_	_	1	list	_	_
11	szu-e2-a	_	Shuea,	_	_	1	list	_	_
12	dumu	_	the son	_	_	11	appos	_	_
13	EDIN-szi-la-at	_	of Edenshilat,	_	_	12	GEN	_	_
14	da-a-da-a	_	and Dada,	_	_	1	list	_	_
15	dumu	_	the son	_	_	14	appos	_	_
16	a-hu-szu-ni	_	of Ahushuni	_	_	15	GEN	_	_
17	lu2-inim-ma-bi-me-esz2	_	are the relevant witnesses	_	_	0	parataxis	_	_

~~~
"Agua the overseer of a crew of 60 men, Adamu, the son of X, Shu-Aba the physician, Imtidam the leather worker, Abiati, Sguea, the son of Edenshilat, and Dada, the son of Ahushuni, are the relevant witnesses." (P123217)

As other examples show, the `list` relation stands here for an implicit conjunction:

	# Jagersma, Chap. 5 (64)					
	# ‘PN1, the chief scribe, and PN2, the surveyor, claim this (land).’					
	# (MVN 6:319 rev 1:3-7; L; 21)					
	1	PN1	PN1	PN1	10	ERG
	2	/	_	_	1	punct
	3	dub-sar-mah	dub.sar.mah	chief.scribe	1	appos
	4	/	_	_	1	punct
	5	PN2	PN2	PN2	1	conj
	6	/	_	_	5	punct
	7	lú-éš-gíd-bé	lú.éš.gíd=be=e	surveyor=and=ERG	5	appos	morphological conjunction!
	8	/	_	_	10	punct
	9	inim	inim=Ø	word=ABS	10	ABS
	10	bí-ĝar-éš	Ø-bi-n-ĝar-eš	VP-3N:on-3SG.A-place-3PL	0	root


TODO: Check `conj` vs. `list` in taglist

	There are some cases where some conclusive phrases are put to describe different goods mentioned above, for example, sheep, goats, donkeys, the delivery/ offering/ expenditure/ wage. It is more convenient to use `conj` or `list` in these cases.

### Nominal modifiers: nmod

In CDLI annotation, nmod is exclusively used for prenominal nominal modifiers. Postnominal nominal modifiers are marked according to their case or as appos.

Sumerian NPs usually place the head of the NP at their left periphery. For semantic reasons, we deviate from this analysis for units and epithets (incl. titles, etc.):

	# Jagersma, Chap. 5 (31)					
	# ‘two and a halve shekels of silver, Aba’s debt’					
	# (NATN 131 obv 13; N; 21)					
	1	2	2	2	3	nummod
	2	½	½	½	1	nummod
	3	giĝ4	giĝ4	shekel	4	nmod
	4	kù-babbar	kù.babbar	silver	0	ABS
	5	ur5	ur5	debt	4	appos
	6	a-ba	a.ba=ak=Ø	Aba=GEN=ABS	5	GEN

For units, the quantified commodity is to be annotated as syntactic head. Numeral modifiers adjacent to the unit are annotated as dependents of the unit, not the commodity. If the commodity stands *between* numeral and unit, numerals modify the commodity.

~~~ conllu
1	sukkal	_	minister	_	_	2	nmod	_	_
2	an-sig₇-ga-ri-a	_	PN.ABS	_	_	0	ABS	_	_

~~~
"Minister Ansiga-ria" (Q000370)

	# Jagersma, Chap. 5 (43)					
	# ‘lord Ningirsu (ergative)’					
	# (Cyl A 23:16; L; 22)					
	1	en	en	lord	2	nmod
	2	dnin-ĝír-su-ke4	nin.ĝír.su.k=e	Ningirsu=ERG	0	ERG

Note that the epithet also applies to proper names other than personal names, e.g., locations (cities, countries, fields, rivers, etc.):

	# Jagersma, Chap. 5 (41)					
	# ‘the land Lagash (ergative)’					
	# (Cyl A 12:23; L; 22)					
	1	ki	ki	land	2	nmod
	2	lagaski-e	lagas=e	Lagash=ERG	0	ERG

	# Jagersma, Chap. 5 (42)					
	# ‘from the mountain land Dilmun’					
	# (VS 14:30 2:4; L; 24)					
	1	kur	kur	mountains	2	nmod
	2	dilmunki-ta	dilmun=ta	Dilmun=ABL	0	ABL

	# Jagersma, Chap. 5 (70)						
	# ‘as ... barley of the field Ennegubade and the field Ugig’						
	# (Nik 1:74 3:1-3; L; 24)						
	1	še	še	barley	0	TERM	marked on 8
	2	(...)	_	_	1	dep	
	3	/	_	_	1	punct	
	4	ašag	ašag	field	5	nmod	epithet
	5	en-né-gù-ba-dé	en.né.gù.ba.dé	Ennegubade	1	GEN	
	6	/	_	_	5	punct	
	7	ašag	ašag	field	8	nmod	
	8	ù-gig-bé-da-šè	ù.gig=be=da=ak=še	Ugig=and=COM=GEN=TERM	5	conj	

	# Jagersma, Chap. 5 (73)						
	# ‘the river Tigris and the river Euphrates’						
	# (Cyl B 17:10; L; 22)						
	1	íd	íd	river	2	nmod	epithet
	2	idigna	idigna	Tigris	0	root	
	3	íd	íd	river	4	nmod	
	4	buranun-bé-da	buranun=be=da	Euphrates=and=COM	2	conj	
	
Note that in the latter example, we follow the existing transliteration as to whether *id* is a determinative (written `{id}idigna`) or an epithet (written `id idigna`). Note that the PPCS manual features example Jagersma 5:73 with determinative interpretation:

	~~~ conllu
	1	{id2}idigna	idigna	Tigris	_	_	6	ERG	_	_
	2	{id2}buranuna-bi-da	buranuna	Euphrates.CONJ.ERG	_	_	1	conj	_	_

	~~~

	(EE 28, example from PPCS manual

The epithet rule is not limited to formal, lexicalized titles, but applies to all cases in which a proper name come to stand in an identity-marking apposition relation with a modifying noun:

	# Jagersma, Chap. 5 (30)					
	# ‘for his master who loves him, Ningirsu’					
	# (Ent.28 5:14-15; L; 25)					
	1	lugal	lugal	master	5	nmod
	2	ki	ki=Ø	place=ABS	3	ABS
	3	an-na-áĝ-ĝá-né	'a-nna-n-'áĝ-Ø-'a=ane	VP-3SG.IO-3SG.A-measure.out-3N.S/DO-NOM=his	1	acl
	4	/	_	_	5	punct
	5	{d}nin-ĝír-su-ra	nin.ĝír.su.k=ra	Ningirsu=DAT	0	DAT

The epithet rule does not apply to year names, as these are propositional:

	# Jagersma, Chap. 5 (45)					
	# ‘from the year “Urbilum was destroyed” to the year “Huhunure was destroyed”’					
	# (ITT 3:4913 6-7; L; 21)					
	1	mu	mu	year	0	ABL
	2	ur-bí-lumki	ur.bí.lum=Ø	Urbilum=ABS	2	ABS
	3	ba-hulu-ta	ba-hulu-Ø=ta	MM-destroy-3N.S/DO=ABL	1	acl
	4	/	_	_	1	punct
	5	mu	mu.	year	1	TERM
	6	hu-nu-reki	hu.nu.re=Ø	Huhunure=ABS	7	ABS
	7	ba-hulu-šè	Ø-ba-hulu-Ø=še	VP-MM-destroy-3N.S/DO=TERM	5	acl

TO BE CONFIRMED: Are months treated like epithets?

	# Jagersma, Chap. 5 (44)						
	# ‘in the month of Sikiba’						
	# (Nik 1:229 1:4; L; 24)						
	1	iti	iti.d	month	2	nmod	check treatment of month names
	2	siki-ba-a	siki.ba='a	wool.distribution=LOC	0	LOC	

In the subsequent mapping to UD, case-marked adnominal dependents of nominal heads are mapped to `nmod`. Most prominently, this includes genitives.

### Quantifiers: det

There are no determiners in Sumerian. The label det is used for postnominal quantifiers (themselves nominal). [TO BE CONFIRMED]

~~~ conllu
1	niŋ₂	_	thing	_	_	4	ABS	_	_
2	na-me	_	some.ABS	_	_	1	det	_	_
3	a₂-be₂	_	arm.3.SG.NH.POSS.ABL	_	_	4	ABL	_	_
4	la-ba-ra-e₃	_	NEG-MID-ABL-leave-3.SG.S	_	_	0	root	_	_

~~~
"Nothing escaped their clutches." (Q000375)
	
### Syntactic coordination: conj, cc

Conjunction can be expressed morphologically or syntactically.

Morphologically marked conjunction is *-bi(-da)* (Jagersma: *-bé(-da)*), and typically occurring between nouns. Originally, *-bi* marks possession and *-da* marks comitative (Hayes p.356). The comitative marking is not systematically applied, so that *-bi* is sometimes glosses as conjunction. In either case, annotate as `conj`. If the comitative does occur, do not annotate `COM`. 

	# Jagersma, Chap. 5 (70)						
	# ‘as ... barley of the field Ennegubade and the field Ugig’						
	# (Nik 1:74 3:1-3; L; 24)						
	1	še	še	barley	0	TERM	marked on 8
	2	(...)	_	_	1	dep	
	3	/	_	_	1	punct	
	4	ašag	ašag	field	5	nmod	epithet
	5	en-né-gù-ba-dé	en.né.gù.ba.dé	Ennegubade	1	GEN	
	6	/	_	_	5	punct	
	7	ašag	ašag	field	8	nmod	
	8	ù-gig-bé-da-šè	ù.gig=be=da=ak=še	Ugig=and=COM=GEN=TERM	5	conj	

The variants *-bi-da* and *-bi* are exchangeable:

~~~ conllu
1	{id2}idigna	idigna	Tigris	_	_	6	ERG	_	_
2	{id2}buranuna-bi-da	buranuna	Euphrates.CONJ.ERG	_	_	1	conj	_	_
3	gud	gud	bull	_	_	6	EQU	_	_
4	gal-gin7	gal	big.EQU	_	_	3	amod	_	_
5	jiri3-bi	jiri3	foot.their	_	_	6	ABS	_	_
6	nam-mi-in-gub	gub	stand	_	_	0	root	_	_

~~~

"The Tigris and the Euphrates stood like great bulls" (EE 28, example from PPCS manual, with *-bi-da*)

	# Jagersma, Chap. 5 (63)					
	# ‘the Tigris and the Euphrates’					
	# (FAOS 5/2 Luzag. 1 2:6-7; N; 24)					
	1	idigna	idigna	Tigris	0	root
	2	/	_	_	1	punct
	3	buranun-bé	buranun=be	Euphrates=and	1	conj

(same?) example by Jagersma, glossed with *-bé*.

	# Jagersma, Chap. 5 (73)						
	# ‘the river Tigris and the river Euphrates’						
	# (Cyl B 17:10; L; 22)						
	1	íd	íd	river	2	nmod	epithet
	2	idigna	idigna	Tigris	0	root	
	3	íd	íd	river	4	nmod	
	4	buranun-bé-da	buranun=be=da	Euphrates=and=COM	2	conj	

	# Jagersma, Chap. 5 (62)					
	# ‘for Ningirsu and Shara’					
	# (Ent. 28 1:5-6; L; 25)					
	1	dnin-ĝír-su	nin.ĝír.su.k	Ningirsu	0	DAT
	2	/	_	_	1	punct
	3	dšara2-bé	šara2=be=r(a)	Shara=and=DAT	1	conj
	
If applied to a clausal argument, *bi-da* can express a circumstantial meaning. For these cases, we annotate `acl+COM`, not `conj`.

~~~ conllu
1	dug4-ga-ni-zid-da	_	_	_	_	9	LOC	_	_
2	ab-ba-ni	_	_	_	_	4	ABS	_	_
3	ama-ni	_	_	_	_	4	ABS	_	_
4	nu-u3-zu-bi	_	_	_	_	1	acl+COM	_	_
5	nig2-{d}ba-u2	_	_	_	_	9	ERG	_	_
6	ab-ba-	_	_	_	_	5	appos	_	_
7	Ha-la-{d}ba-u2-ka-ke4	_	_	_	_	5	GEN	_	_
8	mu-lugal	_	_	_	_	9	ABS	_	_
9	ba-ni-pad3-da-sze3	_	_	_	_	0	parataxis	_	_
10	Ha-la-{d}ba-u2-ka-ke4	_	_	_	_	11	ERG	_	_
11	ba-tag4	_	_	_	_	9	parataxis	_	_

~~~

""

TBC: head is preceding nominal or clause?

Syntactically marked conjunction *u3* (nominal conjunction):

~~~ conllu
1	e₂	_	N	_	_	0	ABS	_	_
2	lal₃	_	N.ABS	_	_	8	ABS	_	_
3	i₃-nun	_	N.ABS	_	_	2	conj	_	_
4	u₃	_	STEM	_	_	2	cc	_	_
5	ŋeštin	_	N.ABS	_	_	2	conj	_	_
6	ki	_	N	_	_	8	LOC	_	_
7	sizkur₂-ra-ka-na	_	N.GEN.3-SG-H-POSS.L1	_	_	6	GEN	_	_
8	nu-silig-ge	_	NEG.NV.PF.ABS	_	_	1	acl	_	_

~~~
"the temple (where) honey, butter and wine in his place of sacrifice shall not cease" (Q001792)

> Note: The taglist uses the POS tag `CNJ`, compare with morphology annotation

If nominal conjunction is not explicitly expressed or has been restored in morphology annotation, use `appos`.

Syntactically marked conjunction *u3* (clausal conjunction):

~~~ conllu
1	PN1	_	PN	_	_	6	ERG	_	_
2	arad	_	slave	_	_	1	appos	_	_
3	PN2-ke4	_	PN.GEN.ERG	_	_	2	GEN	_	_
4	u3	_	and	_	_	1	cc	_	_
5	PN3-ke4	_	PN.ERG	_	_	1	conj	_	_
6	in-ba-a-ne	_	divide	_	_	0	root	_	_
7	u3	_	and	_	_	10	cc	_	_
8	egir	_	after	_	_	10	TMP	_	_
9	ab-ba-ne-ne	_	father.their	_	_	10	ABS	_	_
10	i3-ba-a-ne	_	divide	_	_	6	conj	_	_
~~~

"PN , slave of PN  and PN  divide (the inheritance), and after they divide their father('s estate)" (NG 7 17-21, example from PPCS manual)

If clausal conjunction is not explicitly expressed or has been restored in morphology annotation, use `parataxis`. 

> But note the "tag list" (GDrive syntax folder)
> `conj` "Several elements in the same function (including two verbal chains, nouns, nmods, etc). 

For the unmarked enumeration of transferred goods on a list, use `list`, not `conj`, unless a conjunction is used:

> But note the "tag list":
> There are some cases where some conclusive phrases are put to describe different goods mentioned above, for example,   sheep, goats, donkeys, the delivery/ offering/ expenditure/ wage. It is more convenient to use conj in these cases."

TODO: Check treatment of `appos` versus `conj` in case of implicit conjunction.

TODO: Check `conj` vs. `list` in taglist

	There are some cases where some conclusive phrases are put to describe different goods mentioned above, for example, sheep, goats, donkeys, the delivery/ offering/ expenditure/ wage. It is more convenient to use `conj` or `list` in these cases.

TODO: confirm and validate where to attach `cc`

### Punctuation: punct

No punctuation in Sumerian. However, breaks (new line, different column, different side) are sometimes used to separate different thoughts. If these are encoded explicitly as part of the text (as done, for example, by Jagersma 2010), the recommended dependency is `punct`. Likewise, if a Sumerian transcript includes modern punctuation signs.

	# Jagersma, Chap. 5 (26)					
	# ‘with Lugalkesh, the scribe’					
	# (DP 116 10:3-4; L; 24)					
	1	lugal-kèš{ki}	lugal.kèš	Lugalkesh	0	COM
	2	/	_	_	1	punct
	3	dub-sar-da	dub.sar=da	scribe=COM	1	appos
	
In general, the head of `punct` should be the highest element in the tree that can be reached without crossing another dependency relation.

### Grammatical roles (morphological case): ABS, ERG, DAT, ABL, ADV, COM, EQU, TERM, LOC, GEN

As a general rule, the syntactic relation of nominal dependents with their head is described by the morphological case associated with it. If no case is provided, adnominal nouns are marked nmod (if premodifying) or appos (if postmodifying).
As labels for dependencies, we use the case labels employed in morphological annotation, with the exception of locatives (all represented as LOC) and datives (all represented as DAT). Note that locatives include both spatial and temporal relationships.

Where case marking is postulated in the morphology annotation, we follow that analysis, regardless of whether the morpheme is realized in the surface string. In particular, this includes the annotation of administrative texts, where case marking is systematically lacking.

#### Core arguments: ERG vs. ABS vs. nsubj vs. obj

In CDLI annotation, do not try to map to `nsubj` or `obj` but follow the morphological analysis and annotate for case (i.e. `ABS` and `ERG`). Mappings (https://docs.google.com/document/d/1rTnDPM6CnLu-2msZ_Seh1umnu9xYb0Tel-Y31VpjnP8/edit)

	nsubj	ERG;ABS
	nsubj:passive	ABS
	obj	ABS

For the sake of UD conversion, disambiguation of `ABS` labels is not decided yet. As a first approximation, we could just map `ABS` to `obj` and `ERG` to `nsubj` (as a design decision, subject to subsequent adjustment) as there does not seem to be a reliable way to detect transitives.

TODO: check behaviour of pre-annotator and annotation projection

TODO: check treatment of ERG and ABS in other ergative UD languages

Note that absolutives in vocative use are annotates as `vocative` (not `ABS`) in both CDLI and UD

#### Datives

In morphology, labels are `DAT-H` and `DAT-NH`. Suggestion: Simplify as `DAT` (to better align with annotation projection)

> Taglist originally said to map `DAT-H` to `iobj`, only.
 
Terminative-locatives (if annotated as such) in dative function are treated as oblique arguments, not as datives.

#### Oblique arguments: LOC, TERM, ABL

In CDLI annotation, use morphological case as labels. In UD export, map to `obl`. For better alignment with annotation projection, use `LOC` in place of `L1`, `L2-NH` and `L3-NH`, etc.

TODO: Check treatment in pre-annotation.

#### Adnominal dependents: GEN, EQU

Adnominal cases are predominantly `GEN` or `EQU` and annotated according to their morphological case. In UD export as `nmod`. If no morphological case is annotated, use `nmod` for pre-modifying nominals, `appos` for post-modifying nominals.

	N; GEN；N.3-SG-POSS (Its weight, size……..)
	N-N.3-SG-POSS

> Taglist doesn't make the difference between `appos` and `nmod` explicit. TODO: confirm treatment in pre-annotation and in annotation projection.

The relation N (head noun) + N.GEN can be used to create genitive attribute, sometimes considered a compound construction where N.GEN is adjectivally modifying the head noun, rather than being possessed ‘of’. (Krecher 1987, p.72) An example here from our texts may be: 

	nu-banda3 gu4[-ak]
	
While the the relationship between *nubanda* and *gu* may be either (or both) gentival and compound (according to Krecher’s thought), we annotate it as genitive only.

According to Jagersma (2010, p.90), "[a] noun phrase can also contain another noun phrase in the locative (§7.7.2), directive (§7.6.2), terminative (§7.8.2), or ablative (§7.10)".

	# Jagersma, Chap. 5 (74)					
	# ‘Dudu, the administrator, together with his wife and children will eat this.’					
	# (DP 224 6:5-9; L; 24)					
	1	du-du	du.du	Dudu	10	ERG
	3	saĝĝa	saĝĝa	administrator	1	appos
	5	dam	dam	wife	1	ABL
	6	dumu-né-ta	dumu=ane=ta=e	child=his=ABL=ERG	5	appos
	10	ì-gu7-ne	'i-b-gu7-enē	VP-3N.DO-eat-3PL.A:IPFV	0	root

While this is an undebatable example, there can also be ambiguity as to whether ablatives, terminatives, etc. are adnominal or clausal arguments (the following analyses according to Jagersma):

	# Jagersma, Chap. 5 (11)						
	# ‘with five hides per (lit.“in”) two shekels of silver’						
	# (Nik 1:230 5:2-3; L; 24)						
	1	kù	kù.g	silver	0	LOC	marked on 3
	2	giĝ4	giĝ4	shekel	1	nmod	unit, would be nmod if preposed
	3	2-a	2='a	two=LOC	2	nummod	
	4	/	_	_	1	punct	
	5	kuš	kuš	hide	1	ABL	marked on 5
	6	5-ta	5=ta	five=ABL	5	nummod	

	# Jagersma, Chap. 5 (45)					
	# ‘from the year “Urbilum was destroyed” to the year “Huhunure was destroyed”’					
	# (ITT 3:4913 6-7; L; 21)					
	1	mu	mu	year	0	ABL
	2	ur-bí-lumki	ur.bí.lum=Ø	Urbilum=ABS	2	ABS
	3	ba-hulu-ta	ba-hulu-Ø=ta	MM-destroy-3N.S/DO=ABL	1	acl
	4	/	_	_	1	punct
	5	mu	mu.	year	1	TERM
	6	hu-nu-reki	hu.nu.re=Ø	Huhunure=ABS	7	ABS
	7	ba-hulu-šè	Ø-ba-hulu-Ø=še	VP-MM-destroy-3N.S/DO=TERM	5	acl

Both examples are not fully clear because context is not given. In an alternative analysis, both arguments could also be considered oblique arguments of a clause, with the relation between them established by the verb. If both interpretations are possible, annotate morphologically marked arguments other than genitives as clausal rather than adnominal arguments.

#### "Functional obliques"

Agents in a transaction without morphological marks for their grammatical structure.

	PN.GEN/ N.GEN (giri/ kiszib of a person or occupation)
	giri PN occupation N 
	kiszib PN = obl to verb

In UD export, annotated as `obl`. CDLI labels should be human-readable English short-hands, guided by common translations, e.g., `via` for *giri3*. TODO: Check annotation projection and current treatment in pre-annotation.

#### Case of headless phrases

In headless phrases, concatenate the dependency label of the phrase with the dependency of the (implicit) head, separated by `+`

~~~ conllu
1	dur-an-ki-ka	dur-an-ki	Dur-an-ki	_	_	3	LOC	_	_
2	dur2	dur2	rump	_	_	3	ABS	_	_
3	ba-an-jar	jar	to.place	_	_	0	root	_	_
4	jectug2	jectug2	ear	_	_	3	GEN+ERG	_	_
5	dajal-la-ke4	dajal	to.be.wide	_	_	4	amod	_	_

~~~
"(The one) of wide ear sat in the Duranki" (EnA 11, example from PPCS manual)

Here, *jectug2* is the (head of the explicit) genitive phrase, its (implicit) head serves as ergative argument of the clause. In UD mapping, preserve the grammatical function of the implicit head only, here `nsubj`.

#### Genitive case: GEN

Along with equative, the genitive is an adnominal case (not resumed by any dimensional prefix) indicating possession, origin or affiliation.
In the mapping to UD, represented as `nmod`.

The anticipatory genitive (`GEN+disloc`, see `disloc`) involves a dislocation. As this can be iterated (anticipatory genitive of an anticipatory genitive), we annotate the head in an opportunistic fashion: Where this is adjacent to the semantic head, annotate the semantic head, where it is detached, annotate the head of the clause as head. In UD, the first use should be `nmod`, the second should be `disloc`.

#### Equative case: EQU

Along with genitive, the equative (equitative) case, marked by *gin7*, is an adnominal case and not resumed by any dimensional prefix. It can be used to create nominal sentences. 

~~~ conllu
1	a-ba	_	who	_	_		root	_	_
2	szesz-gu10-gin7	_	like.my.brother	_	_	1	EQU	_	_

~~~
"Who is like my brother?" (Hayes, p.312, TCS 1,200)

As a general rule, nominal sentences without explicit morphological marks in the text (or their restauration in the morphology annotation) should be annotated as having an implicit copula, i.e., either as `appos` (if an appositional/equational reading is preferred, first nominal is head), or as clause (second nominal is copular predicate and head, first nominal is `ABS`). In a sequence of clauses, the copular annotation is preferred:

~~~ conllu
1	di-til-la	_	Ditila	_	_	0	root	_	_
2	{m}szag4-szu-nigin2	_	Shagshunigin	_	_	7	ABS	_	_
3	dumu-u2-sze3-he2-gin	_	daughter.of.Ushehegin	_	_	2	appos	_	_
4	udul	_	cowherd	_	_	3	appos	_	_
5	ur-{d}nansze	_	Ur-Nanshe	_	_	7	ERG	_	_
6	dumu-ba-szi-szag4-ra-gi-ke4	_	son.of.Bashishagragi	_	_	5	appos	_	_
7	ba-an-tuku	_	married	_	_	1	parataxis	_	_
8	...	_	...	_	_	7	_	_	_
9	ur-{d}ig-alim	_	Ur-Igalim	_	_	11	ABS	_	_
10	dumu-lu2-gu10	_	son.of.Lugu,	_	_	9	appos	_	_
11	maszkim	_	bailiff	_	_	7	parataxis	_	_

~~~
(Hayes p.327, NSGU 1)


TBC: In the mapping to UD, equative rendered as xcomp or nmod?

#### Possession

Annotation of possession requires co-indexing of arguments. This is not covered by the dependency annotation as this leads to non-projective structures. Argument co-indexing is left as a future extension for the DEPRELS column of CoNLL-U.

> Note: The taglist on the syntax folder at GDrive recommended `nmod` also for possessives. 

### Vocative: voc

The vocative identifies the addressee of the following statements with a noun phrase without case marking.

~~~ conllu
1	{d}gilgamec2	gilgamec2	Gilgamec	_	_	3	voc	_	_
2	en-ce3	en3-ce3	how long	_	_	3	TERM	_	_
3	i3-nu2-de3-en	nu2	to lie down	_	_	0	root	_	_

~~~

"Gilgamesh! how long will you sleep?" (GH 81, example from PPCS manual)

Also used for absolutive arguments before the non-verbal clause in seals:

"In seal inscriptions, the initial nominal phrase contains the name of the king as a vocative. The vocative normally has no marking in Sumerian ... [, but t]here are a few cases where the vocative is marked by .e; this is presumably an extension in use of the lcoative-terminative case." (Hayes, p. 275)

~~~ conllu
1	{d}i-bi2-	_	Ibbi-	_	_	8	voc	_	_
2	{d}zuen	_	Suen	_	_	1	flat	_	_
3	...	_	...	_	_	1	appos	_	_
4	da-da	_	Dada	_	_	8	ABS	_	_
5	ensi2	_	ensi	_	_	4	appos	_	_
6	nibru{ki}	_	of.Nippur	_	_	4	GEN	_	_
7	...	_	...	_	_	4	appos	_	_
8	arad2-zu	_	servant	_	_	0	root	_	_

~~~
"Ibbi-Suen, ..., Dada, ensi of Nippur, ..., is your servant." (Hayes p. 274, Ibbi-Sin 7)

### Dislocation: +disloc

Anticipatory genitives preposed to the clause are attached the additional label `disloc`. If they are adjacent to the nominal they modify, annotate them as nominal dependents. If they are not adjacent to the nominal they modify, annotate them as dependents of the syntactic head of the clause. In UD mapping, the former should become `nmod`, the latter should become `disloc`.

~~~ conllu
1	za3-mi2	za3-mi2	hymn.GEN	_	_	2	GEN+disloc	_	_
2	mu-ru-bi-im	murub4	middle.its.COP	_	_	0	root	_	_

~~~

"(It) is the middle of the hymn" (Gudea CylA 30:16, example taken from PPCS manual)

~~~ conllu
1	e2-a	e2	house.GEN	_	_	5	GEN+disloc	_	_
2	{d}en-ki-ke4	en-ki	Enki.ERG	_	_	5	ERG	_	_
3	jic-hur-bi	jic-hur	plan.its.LT	_	_	5	DAT	_	_
4	si	si	horn	_	_	5	ABS	_	_
5	mu-na-sa2	sa2	to.equal	_	_	0	root	_	_

~~~

"Enki prepared the plan of the house for him" (Gudea CylA 17:17, example taken from PPCS manual)

### Numeral modifiers: nummod

The label `nummod` is assigned on semantic grounds (regardless of morphology) to every numeral that modifies a nominal or verb. Possible morphological tags include `NU` but also numerals with a verbal (copular) component such as `NU.GEN.COP-3-SG`, `NU.ABS.COP-3-SG`, etc.

~~~ conllu
1	...	_	NU	_	_	2	nummod	_	_
2	...	_	N	_	_	0	root	_	_

~~~
(premodifying numeral)

	# Jagersma, Chap. 5 (47)					
	# ‘fifteen full-grown oxen (having) healthy eyes’					
	# (VS 14:66 1:1; L; 24)					
	1	15	15	15	2	nummod
	2	gu4	gu4.ř	bull	0	root
	3	gal-gal	gal-gal	big-big	2	amod
	4	igi	igi	eye	5	ABS
	5	silim	silim-Ø	be.healthy-NFIN	2	acl

~~~ conllu
1	...	_	N	_	_	0	root	_	_
2	...	_	NU.GEN.COP-3-SG	_	_	1	nummod	_	_

~~~
(postmodifying numeral)

	# Jagersma, Chap. 5 (7)					
	# ‘Bau’s septuplets (lit.“the seven twins of Bau”)’					
	# (Cyl B 11:11; L; 22)					
	1	dumu-maš	dumu.maš	twin	0	ABS
	2	7	imin	seven	1	nummod
	3	dba-ú	ba.ú=ak=Ø	Bau=GEN=ABS	1	GEN

	# Jagersma, Chap. 5 (48)						
	# ‘his seven-cornered house (lit. “his seven-corners house”)’						
	# (St D 2:11; L; 22)						
	1	é	é	house	0	ABS	marked on 3
	2	ub	ub	corner	1	appos	
	3	imin-na-né	imin=ane=Ø	seven=his=ABS	2	nummod	

Also, adverbial numerals (numeral oblique arguments) are annotated `nummod`, regardless of their morphological case:

	# Jagersma, Chap. 7 (324)						
	# ‘that after Kuda(‘s death) fifteen years ago (lit. “since fifteen with the years”), Urbagara took him (a slave) as his share (in the inheritance)’						
	# (NG 34 6-7; L; 21)						
	1	eger5	eger5	back	7	ABL	
	2	ku5-da-ta	ku5.da=ak=ta	Kuda=GEN=ABL	1	GEN	
	3	mu-da	mu=da	year=COM	7	COM	
	4	15-ta	15=ta	15=ABL	7	nummod	morphologically marked as ABL
	5	/	_	_	7	punct	
	6	ur-ba-gara2-ke4	ur.ba.gara2.k=e	Urbagara=ERG	7	ERG	
	7	in-ba-a	'i-n-ba-Ø-'a	VP-3SG.A-portion.out-3SG.S/DO-NOM	0	acl	

(numeral [oblique] argument)

(TBC: How is the following example to be analyzed -- this seems to be hypercorrect (!?) morphological marking to underline that it relates to *eger5* ?)

	# Jagersma, Chap. 4 (34)						
	# ‘subsequently (lit “for the second one”)’						
	# (Cyl A 9:5; L; 22)						
	1	2-kam-ma-šè	min-kamma=še	two-ORD=TERM	0	nummod	morphologically marked as TERM

This extends to headless numerals:

	# Jagersma, Chap. 27 (73)						
	# ‘This is what the gardeners turned over in the second transfer (lit. “turned on the hands in that of the second one”).’						
	# (VS 14:113 2:2-4; L; 24)						
	1	2-kam-ma-ka	2-kamma=ak='a	2-ORD=GEN=LOC	6	nummod	(not nummod+GEN+LOC)
	2	/	_	_	6	punct	
	3	nu-kiri6-ke4-ne	nu.kiri6.k=enē=e	gardener=PL=ERG	6	ERG	
	4	/	_	_	6	punct	
	5	šu-a	šu='a	hand=LOC	6	LOC	
	6	bí-gi4-a-am6	Ø-bi-n-gi4-eš-'a=Ø='am	VP-3N:on-3SG.A-turn-3PL-NOM=ABS=be:3N.S	0	acl+ABS	or root

This also extends to numerals that are predicates of copula clauses:

	# Jagersma, Chap. 5 (16)					
	# ‘This is of the six of them.’					
	# (VS 14:172 8:9; L; 24)					
	1	6-a-ne-ne-kam	6=anēnē=ak='am	six=their=GEN=be:3N.S	0	nummod

And to numerals that carry clausal modifiers:

	# Jagersma, Chap. 5 (22)					
	# ‘These are the second ones that were brought to the palace.’					
	# (VS 14:48 2:4-6; L; 24)					
	1	2-kam-ma	min-kamma	two-ORD	0	nummod
	2	/	_	_	1	punct
	3	é-gal-šè	é.gal=še	palace=TERM	5	TERM
	4	/	_	_	5	punct
	5	ře6-a-am6	ře6-Ø-'a=Ø='am	carry-NFIN-NOM=ABS=be:3N.S	1	acl

Furthermore, `nummod` is used for parts of a numeral, annotated as dependents of the first element in a numeral

> Note: Earlier, we used `compound` and `flat` for the internal structure of complex numerals. But this is inconsistent with the annotation of *la2* "minus" as `acl` (should be `flat` as well, then). Hence, another relation.

### Compound: compound

Used for the nominal part of a compound verb (if a list of compound verbs is provided). Without such a list, this is annotated according to its grammatical structure (if transparent).

There are many other compound constructions in Sumerian: not only compound verbs, but compound nouns and  “adjective-like compound constructions”.

An example of a N - ADJ compound is: 

	s i p a z i(- d) "loyal-shepherd

An example of a N - VERB/Adj (or ‘dub-sar’) compound:

	k i n g a I "director of labours" (or the like)

literally "someone who is great with respect to the labours" (certainly not "the great work" or "the great assembly',);

In discussing the syntax of these sort of compound constructions, Krecher states that they are built “just like compounds without however ceasing to be two words” (Joachim Krecher, 1987, ASJ 9, 1987. p. 70).

In the CDLI corpus, most (or all?) compound nouns such as dub-sar (dub sar) will appear segmented as a single unit, to be tagged as a noun rather than a compound noun. While realizing there are compound noun, we will nevertheless treat them as a single unit syntactically. This is not without precedent in digital databases:  dub-sar constructions are analyzed as compound nouns in Zolyomi 2017, 92 — often consisting of a noun + non-finite verbal form ((dub=ø sar-ø : tablet=ABS write-TL) “he who writes tablets”. However, at ETCSRI, dub-sar is simply tagged N1 (noun phrase one – head), i.e. analyzed as a noun. If any compound nouns appear in the CDLI corpus, they should be marked using UD’s `compound` tag.

> Note: The earlier use of `compound` for complex numbers is deprecated.

TODO: list of compound verbs

### Flat: flat

Use for expressions whose internal structure is opaque, e.g., proper names that are not to be further substructured. To be avoided whenever possible.

~~~ conllu
1	bad3-mar-tu	_	the.Martu.wall	_	_	0	ABS	_	_
2	mu-ri-iq	_	Muriq	_	_	1	appos	_	_
3	ti-id-ni-im	_	Tidnim	_	_	2	flat	_	_

~~~
"the Martu-wall (whose name is) Muriq Tidnim" (Shu-Sin 9)

In the following text, a name otherwise treated as a single token is split to different lines, `flat` can be used as a means of repair in this case.

~~~ conllu
1	{d}i-bi2-	_	Ibbi-	_	_	8	voc	_	_
2	{d}zuen	_	Suen	_	_	1	flat	_	_
3	...	_	...	_	_	1	appos	_	_
4	da-da	_	Dada	_	_	8	ABS	_	_
5	ensi2	_	ensi	_	_	4	appos	_	_
6	nibru{ki}	_	of.Nippur	_	_	4	GEN	_	_
7	...	_	...	_	_	4	appos	_	_
8	arad2-zu	_	servant	_	_	0	root	_	_

~~~
"Ibbi-Suen, ..., Dada, ensi of Nippur, ..., is your servant." (Hayes p. 274, Ibbi-Sin 7)

> Note: the earlier use of `flat` for the second part of a number (`NU`; `NU.GEN.COP-3-SG`) is deprecated.

TODO: fix numerical `flat` in pre-annotation.

### Clausal complement: ccomp

Used for direct speech and quotations; the clause following “someone said that”:

~~~ conllu
1	lu2	lu2	person	_	_	5	ERG	_	_
2	iri-ce3	iri	town.TERM	_	_	4	TERM	_	_
3	je26-e	je26	I	_	_	4	ABS	_	_
4	ga-jen	jen	go	_	_	5	ccomp	_	_
5	nu-mu-un-na-ab-be2	dug4	NEG.say	_	_	0	root	_	_

~~~

"No one said: 'I will go to the city'" (L2 272, example from PPCS manual)

~~~ conllu
1	PN1	_	PN	_	_	7	ERG	_	_
2	dam-ce3	_	wife.TERM	_	_	3	TERM	_	_
3	ha-tuku	_	have	_	_	4	ccomp	_	_
4	bi2-in-dug4-ga	_	say.NOM	_	_	7	acl	_	_
5	PN2	_	PN	_	_	7	ABS	_	_
6	PN3	_	PN	_	_	5	appos	_	_
7	nam-erim2-am3	_	swear.COP	_	_	0	root	_	_

~~~
"PN  (and) PN  swore that PN  declared: 'I will marry (her)'" (contract; NG 15:6-9, 16:6-11, example from PPCS manual)


~~~ conllu
1	kiszib-ba	_	seal	_	_	5	GEN+disloc	_	_
2	lugal-gu10	_	king	_	_	4	voc	_	_
3	gesztug3-nig2-sag5-ga-ka-ne2	_	ear.of.favor	_	_	4	LOC	_	_
4	ga-an-ti-il	_	keep.alive	_	_	5	ccomp	_	_
5	mu-bi	_	name	_	_	0	parataxis	_	_

~~~
"The name of this seal is: 'Oh my king, let me keep him alive at his ear of favor.'" (seal; Hayes p.291, Shulgi 47)

Commonly used in Ur III letters:

~~~ conllu
1	ba-lu5-lu5	_	to.Balulu	_	_	2	DAT	_	_
2	u3-na-a-dug4	_	speak	_	_	0	root	_	_
3	dam	_	wife	_	_	6	DAT	_	_
4	gu-za-ni-ra	_	of.Guzani	_	_	3	GEN	_	_
5	szu	_	(compound)	_	_	6	ABS	_	_
6	ha-bar-re	_	release	_	_	2	ccomp	_	_
7	na-mi-gur-re	_	not.argue	_	_	6	parataxis	_	_

~~~
"To Balulu speak; the wife of Guzani have him  release; let him not argue." (letter; Hayes p.304, TCS 1,46; Michaelowski 126)

~~~ conllu
1	ni-kal-la-ar	_	to.Nikala	_	_	2	DAT	_	_
2	u3-na-a-dug4	_	speak	_	_	0	root	_	_
3	en-u2-a	_	Enua	_	_	4	ABS	_	_
4	na-an-ba-an-du3	_	not.detain	_	_	2	ccomp	_	_
5	lu2-ne2	_	his.man	_	_	7	ERG	_	_
6	szu	_	(compound)	_	_	7	ABS	_	_
7	he2-am3-ba-re	_	release	_	_	4	parataxis	_	_

~~~
"To Nikala speak; let him not detain Enua; let his man release him." (Hayes p.308, TCS 1,193)

Note that year names should not be annotated as `ccomp` (although they could be considered direct speech), but as `acl` (as they are sometimes morphologically marked as such).

### Adverbial clause: advcl

`advcl` is used for subordinate clauses with an explicit `mark` that indicates an adverbial function, e.g., *tukumbi* "if":

~~~ conllu
1	lugal-ju10	lugal	king	_	_	7	ERG	_	_
2	tukum-bi	tukum-bi	if	_	_	5	mark	_	_
3	ud-da	ud	day(light)	_	_	5	LOC	_	_
4	kur-ra	kur	land	_	_	5	LOC	_	_
5	i-ni-in-ku4-ku4-de3	kur9	enter	_	_	7	advcl	_	_
6	{d}utu	utu	Utu	_	_	7	COM	_	_
7	he2-me-da-an-zu	zu	know	_	_	0	root	_	_

~~~
"If you (have to) enter the mountain, you should inform Utu (of it)" (example from PPCS manual)

Circumstantial clauses created by the copula can be annotated as `advcl` (TBC).

~~~ conllu
1	{d}nanna	_	for.Nanna	_	_	13	DAT	_	_
2	...	_	...	_	_	0	_	_	_
3	{d}amar-{d}zuen	_	Amar-Sin	_	_	13	ERG	_	_
4	...	_	...	_	_	0	_	_	_
5	ud-ul-li2-a-la	_	from.of.old	_	_	7	GEN.ABL	_	_
6	gi6-par4-bi	_	its.giparu	_	_	7	ABS	_	_
7	nu-du3-am3	_	not-built	_	_	13	advcl	_	_
8	en	_	en-priestess	_	_	9	ABS	_	_
9	nu-un-til3-la-am3	_	not.taken.up.residence	_	_	13	advcl	_	_
10	{d}amar-{d}zuen	_	Amar-Sin	_	_	13	ERG	_	_
11	...	_	...	_	_	0	_	_	_
12	gi6-par4-kug-ga-ni	_	pure.giparu	_	_	13	ABS	_	_
13	mu-na-du3	_	build	_	_	0	root	_	_

~~~
"For Nanna, Amar-Sin -- from ancient times, its giparu not having built, no en-priestess having taken up residence -- built its giparu." (Amar-Suen 11, following Hayes, p.225)

Taglist:
> taglist: advcl - Adverbial clauses, subordinate clause with or without subordinate mark, like tukumbi (if)
> comment IK: look into it ;)

TODO: compare with MTAAC preannotation, ETSCRI preannotation and annotation projection

### Parataxis: parataxis

Morphologically and syntactically unmarked sequence of clausal arguments (or expressions that imply a clausal structure, e.g., transactions).

Also to be used for copular biclausal constructions (Zolyomi 2017, p. 144), as found, for example in P248792 and P100065.

Also used for pisagdubak, notes (usually NU), the sealing, when non-sentential units are to be connected by means of a sentential interpretation:

~~~ conllu
1	5	_	5	_	_	2	nummod	_	_
2	ma-na	_	minas	_	_	0	root	_	_
3	gi-na	_	standard	_	_	2	amod	_	_
4	{d}szu-{d}zuen	_	Shu-Sin	_	_	2	parataxis	_	_
5	lugal-kalag-ga	_	mighty.king	_	_	4	appos	_	_
6	lugal-urim5{ki}-ma	_	king.of.Ur	_	_	4	appos	_	_
7	lugal-an-ub-da	_	king	_	_	4	appos	_	_
8	limmu2-ba	_	of.the.four.quarters	_	_	7	GEN	_	_

~~~
"5 standard minas. Shu-Sin, the mighty king, king of Ur, king of the four quarters" (Shu-Sin 17)

This is a weight inscription without any explicit verb. The sentential interpretation (implicit in this text) is "(This is a weight of) 5 minas; (it is authorized by) Shu-Sin ...".

~~~ conllu
1	di-til-la	_	Ditila	_	_	0	root	_	_
2	{m}szag4-szu-nigin2	_	Shagshunigin	_	_	7	ABS	_	_
3	dumu-u2-sze3-he2-gin	_	daughter.of.Ushehegin	_	_	2	appos	_	_
4	udul	_	cowherd	_	_	3	appos	_	_
5	ur-{d}nansze	_	Ur-Nanshe	_	_	7	ERG	_	_
6	dumu-ba-szi-szag4-ra-gi-ke4	_	son.of.Bashishagragi	_	_	5	appos	_	_
7	ba-an-tuku	_	married	_	_	1	parataxis	_	_

~~~
"Ditila. Ur-Nanshe, the son of Bashishagragi, has married Shagshunigin, the daughter of Ushehegin the cowherd" (Hayes p.327, NSGU 1)

Ditila is a summary of a completed legal case. The initial phrase ditila is considered as an independent statement with a sentential interpretation, thus following sentences are connected by `parataxis`, referring to ditila as their head.

Note that the elements conjoined by `parataxis` can be subject to further means of syntactic co(sub)ordination:

~~~ conllu
1	di-til-la	_	Ditila	_	_	0	root	_	_
2	{m}szesz-kal-la	_	Sheshkala	_	_	7	ERG	_	_
3	dumu-ur-{d}lamar-ka-ke4	_	son.of.Ur-Lamar	_	_	2	appos	_	_
4	arad2-	_	slave	_	_	7	ccomp	_	_
5	ur-{d}sahar-{d}ba-u2-ka	_	of.Ur-Sahar-Bau	_	_	4	GEN	_	_
6	nu-u3-me-en3	_	not.COP	_	_	4	cop	_	_
7	bi2-in-dug4	_	said	_	_	1	parataxis	_	_
8	ur-{d}lamar	_	to.Ur-Lamar	_	_	20	LOC	_	_
9	ab-ba-szesz-kal-la-ke4	_	father.of.Sheshkala	_	_	8	appos	_	_
10	e2-	_	in.the.house	_	_	20	LOC	_	_
11	ur-{d}sahar-{d}bau-u2	_	of.Ur-Sahar-Bau	_	_	10	GEN	_	_
12	dumu	_	son	_	_	11	appos	_	_
13	na-mu-ka	_	of.Namuka	_	_	12	GEN	_	_
14	sze-ba	_	barley.rations	_	_	20	ABS	_	_
15	siki-ba	_	wool.rations	_	_	14	appos	_	_
16	szu	_	for.the.hand	_	_	20	ABL	_	_
17	al-la	_	of.Alla	_	_	16	GEN	_	_
18	dub-sar-ta	_	scribe	_	_	17	appos	_	_
19	nam-arad2-sze3	_	because.of.arad2.status	_	_	20	TERM	_	_
20	ba-na-sum	_	given	_	_	30	acl	_	_
21	u3	_	and	_	_	20	cc	_	_
22	ur-{d}lamar-ke4	_	to.Ur-Lamar	_	_	27	ERG	_	_
23	szesz-kal-la	_	Sheshkala	_	_	27	ABS	_	_
24	arad2	_	slave	_	_	23	appos	_	_
25	ki	_	on.premises	_	_	27	LOC	_	_
26	ur-{d}sahar-{d}ba-u2-ka-am3	_	of.Ur-Sahar-Bau	_	_	25	GEN	_	_
27	i3-tud-da	_	born	_	_	20	conj	_	_
28	lu2-dug3-ga	_	Luduga	_	_	30	ABS	_	_
29	du-du-mu	_	Dudumu	_	_	30	appos	_	_
30	nam-erim2-am3	_	swear.oath	_	_	7	parataxis	_	_

~~~
"Ditila. Sheshkala, the son of Ur-Lamar, said: 'I am not the slave of Ur-Sahar-Bau!'. It is an oath of Luguda and Dudumu that barley rations and wool rations had been given to Ur-Lamar, the father of Sheshkala, in the house of Ur-Sahar-Baz, the son of Namu, on the authority of Alla the scribe, because of his status as slave, and that Sheshkala the save was born to Ur-Lamar on the very premises of Ur-Sahar-Bau."" (Hayes p.334, NSGU 32)

In this analysis (according to Hayes), two paratactically linked clauses ("Barley rations and wool rations have been given to Ur-Lamar ..." and "Sheshkala the slave was born to Ur-Lamar on the premises of Ur-Sahar-Bau") form a complex relative clause (morphologically marked at i3-tud-da, at the end of the second clause) that is an argument to (the content of) the oath that Luguda and Dumudu swore. Only the oath is a complete sentence.

? special treatment of seals

taglist suggests `admin` for the relationship between the text and the sealing
	
> comment CC: IMHO, the label vague and may be misinterpreted. If at all, it must be more specific, because also the transaction agents serve certain administrative functions, why not `seal`? Linguistically, I see  no argument for not having that as a parataxis, but we could do `parataxis:seal` 

Discussion on taglist: 

> taglist: parataxis	for pisagdubak; notes (usually NU); the sealing 
> comment IK: replace with something else?
> comment Jinyan Wang: `admin`?
> comment CC: only if we can detect those reliably
> taglist (reverse list): parataxis for pisagdubak[filing_basket], `admin` for the relation between text and sealing 

TODO: check treatment in pre-annotation and annotation projection.

### Copula clauses: cop

The head of a copula clause is the (head of the) nominal predicate, that is either the phrase at which the copula is morphologically marked, or the phrase that precedes an independent copula element. An independent copula is to be annotated as `cop`.

Note that the (nominal) head of a copula may be a deverbal noun, i.e., a relative clause (`acl` or `amod`).

The predicate of a copular clause is its head. The morphological case of a copular predicate is *not* annotated. This also includes cases in which the head has a more complex structure, e.g., do not annotate the genitive relation in the following example:

	# Jagersma, Chap. 5 (21)						
	# ‘They are the ones of Geme-Bau.’						
	# (Nik 1:7 2:4; L; 24)						
	1	geme2-{d}ba-ú-ka-me	geme2.ba.ú.k=ak=Ø=me-eš	Geme-Bau=GEN=ABS=be-3PL.S	0	root	copular predicate is a headless absolutive NP with a genitive argument

## Genre specifics

The description so far focused on prose text. Administrative texts require a slightly different treatment.

### Scope of dates in Ditilas

Ditilas represent a summary of a closed legal case, e.g., a marriage, with the typical structure:

	1. heading "ditila"
	2. summary of the case
	3. statement of an oath
	4. name of bailiff
	5. list of judges
	6. date
	
We assume that the heading is inherently sentential ("This is a Ditila") and the `root` of the text, the other sections being separate clauses connected with `parataxis`. The date takes ditila as its head, not to any of the more adjacent clauses. This practice should be followed whenever a dated statement takes scope over a range of subsequent clauses (high attachment).

Note: If the annotation of dates would ever change to parataxis, the head of the date would be the list of judges.

### Transactions and their participants

Dependency relations specific to administrative texts include
- giri3, kiszib
- total, date, agent
- list
- compound (in nominals)

Administrative texts often exhibit a list-like character without clear sentential structure. 

~~~ conllu
1	1(disz)	_	1	_	_	2	nummod	_	_
2	gu4	_	bull	_	_	0	root	_	_
3	niga	_	barley-fattened	_	_	2	appos	_	_
4	ma2	_	ship	_	_	2	TERM	_	_
5	an-na	_	An[.GEN.TERM]	_	_	4	GEN	_	_
6	sza3	_	in	_	_	2	LOC	_	_
7	unu{ki}-ga	_	Uruk.GEN[.LOC]	_	_	6	GEN	_	_
8	giri3	_	transmitter	_	_	2	giri3	_	_
9	bar-bar-re	_	B.	_	_	8	GEN	_	_
10	zi-ga	_	disembursement-from	_	_	2	ziga	_	_
11	be-li2-du10	_	B.	_	_	9	GEN	_	_
12	iti	_	month	_	_	13	nmod	_	_
13	a2-ki-ti	_	Akiti	_	_	2	date	_	_
14	mu	_	year	_	_	13	LOC	_	_
15	an-sza-an{ki}	_	Anshan	_	_	16	ABS	_	_
16	ba-hul	_	destroyed	_	_	14	acl	_	_

~~~	
(P109483)

> Note: confirm `ziga` role in the annotation

This text describes a single transaction, but without any explicit verbal element. The obligatory part of a transaction statement is the object being transferred. This is thus modelled as root. A transaction involves a number of functional roles, some of which are partially understood, only. These are identified by morphological case labels (if provided by the morphology annotation, here TERM, LOC), Sumerian technical terms (here ziga, giri3), or semantic role labels (date, agent [= unmarked receiver or supplier], total).

~~~ conllu
1	83	_	83	_	_	2	nummod	_	_
2	gud	_	bulls	_	_	0	root	_	_
3	niga	_	barley-fattened	_	_	2	appos	_	_
4	32	_	32	_	_	5	nummod	_	_
5	gud	_	bulls	_	_	2	list	_	_
6	u2	_	grass-fattened	_	_	5	appos	_	_
7	20	_	18	_	_	8	nummod	_	_
8	la1	_	_	_	_	7	compound	_	_
9	2	_	_	_	_	7	compound	_	_
10	ab2	_	cows	_	_	2	list	_	_
11	mu	_	years	_	_	10	appos	_	_
12	2	_	two	_	_	11	nummod	_	_
13	niga	_	barley-fattened	_	_	10	appos	_	_
14	4	_	4	_	_	15	nummod	_	_
15	ab2	_	cows	_	_	2	list	_	_
16	mu	_	years	_	_	15	appos	_	_
17	2	_	two	_	_	16	nummod	_	_
18	u2	_	grass-fattened	_	_	15	appos	_	_
19	4	_	4	_	_	20	nummod	_	_
20	amar	_	calves	_	_	2	list	_	_
21	ga	_	milk-fed	_	_	20	appos	_	_
22	szu-nigin2	_	total	_	_	2	total	_	_
23	141	141	_	_	_	24	nummod	_	_
24	gud-hi-a	_	assorted.cattle	_	_	22	appos	_	_
25	zig3-ga	_	disembursement	_	_	24	amod	_	_
26	ud	_	of.day	_	_	22	date	_	_
27	30	_	29	_	_	26	nummod	_	_
28	la1	_	_	_	_	27	compound	_	_
29	1-kam	_	_	_	_	27	compound	_	_
30	iti	_	month	_	_	31	nmod	_	_
31	Sze-kar-ra-gal2	_	Shekaragal	_	_	26	LOC	_	_
32	mu	_	year	_	_	31	LOC	_	_
33	Si-mu-ru-um{ki}	_	Simurum	_	_	39	ABS	_	_
34	Lu-lu-bu-um{ki}	_	Lulubum	_	_	33	appos	_	_
35	a-ra2	_	ninth.time	_	_	39	dep	_	_
36	10	_	_	_	_	35	nummod	_	_
37	la1	_	_	_	_	36	compound	_	_
38	1-kam	_	_	_	_	36	compound	_	_
39	ba-hul	_	destroyed	_	_	32	acl	_	_

~~~
(no CDLI, Kang 252, Hayes 2000, p. 367)

The `list` relation holds between entitites of the same kind, here, the objects of transaction. Note that `list` should *not* be used to connect transactions. We assume that transactions are inherently sentential, so, use `parataxis`. The total is connected by a total relation

The internal structure of complex numerals is represented by `nummod` (design decision; chosen here in favour of `compound` or `flat` which would be equally possible).

Note that the morphology and the relation of a-ra2 (35) may be revised.

Note that administrative texts *can* actually use overt verbs, in this case, the verb is the root, and the object of the transition is assumed to be a terminative argument.

~~~ conllu
1	1	_	1	_	_	2	nummod	_	_
2	lulim	_	deer	_	_	16	TERM	_	_
3	nitab	_	male	_	_	2	appos	_	_
4	2	_	2	_	_	5	nummod	_	_
5	lulim	_	deer	_	_	2	list	_	_
6	munus	_	female	_	_	5	appos	_	_
7	1	_	1	_	_	9	nummod	_	_
8	amar	_	calf	_	_	9	nmod	_	_
9	lulim	_	deer	_	_	2	list	_	_
10	munus	_	milk-fed	_	_	9	appos	_	_
11	ga	_	female	_	_	9	appos	_	_
12	ba	_	dead.	_	_	13	ABS	_	_
13	usz2 ...	_	_	_	_	2	acl	_	_
14	{d}Szu-gi-uru-gu10	_	Shulgiurugu	_	_	16	ERG	_	_
15	szu	_	received	_	_	16	ABS	_	_
16	ba-ti	_	_	_	_	0	root	_	_

~~~
Archi and Pomponio 347, Hayes p.371, not in CDLI

As for roles of agents such as *giri3 PN* (by the means of PN), and *kiszib PN* (by the seal of PN), we use the dependencies `giri3`, `kiszib`, etcs., and mark these as syntactic heads, with the proper name in genitive. In the UD mapping, these labels then become `obl`.

~~~ conllu
1	[n]	_	NUM	NU	_	3	nummod	_	_
2	...	_	_	_	_	_	1	_	_	_
3	udu	udu[sheep]	NOUN	N	Number=Sing	10	ABS	_	_
4	ur-{d}lamma	Urlamma[1]	PROPN	PN	Animacy=Hum|Number=Sing	10	DAT	_	_
5	...	_	_	_	_	_	4	_	_	_
6	ki	ki[place]	NOUN	N	Number=Sing	10	ABL	_	_
7	{d}szara2-kam-ta	Szarakam[1]	PROPN	PN	Animacy=Hum|Case=Gen,Abl|Number=Sing	6	GEN	_	_
8	ur-{d}lamma	Urlamma[1]	PROPN	PN	Animacy=Hum|Number=Sing	10	ERG	_	_
9	...	_	_	_	_	_	8	_	_	_
10	i3-dab5	n]	VERB	V	Number=Sing|Person=3|VerbForm=Fin	0	_	_	_
11	giri3	giri[foot]	NOUN	N	Number=Sing	10	giri3	_	_
12	ka5-a-mu	Kayamu[1]	PROPN	PN	Animacy=Hum|Case=Gen|Number=Sing	11	GEN	_	_
13	iti	iti[month]	NOUN	N	Number=Sing	10	date	_	_
14	ezem-me-ki-gal2	Ezemmekegal[1]	PROPN	MN	Number=Sing	13	appos	_	_
15	mu	mu[year]	NOUN	N	Number=Sing	13	LOC	_	_
16	{d}gu-za	guza[chair]	NOUN	N	Number=Sing	18	ABS	_	_
17	{d}en-lil2-la2	Enlil[1]	PROPN	DN	Animacy=Hum|Case=Gen,Abs|Number=Sing	16	GEN	_	_
18	ba-dim2	dim[create]	VERB	V	Number=Sing|Person=3|Voice=Mid	15	acl	_	_

~~~
(P102314)

TBC for other roles: the respective person designated is assumed to represent the syntactic head, with the technical term treated like epithet or unit identifier

### Units

In a list of commodities, the conventional structure is `number -nummod-> unit -nmod-> product`. For the sequence `number product unit`, we annotate the unit as an `appos` to the product that is the head. The objective is to have the product systematically as head.

~~~ conllu
1	a-bi-a-ti	_	to.Abiati	_	_	2	DAT	_	_
2	u3-na-a-dug4	_	speak	_	_	0	root	_	_
3	1	_	1	_	_	4	nummod	_	_
4	sze	_	barley	_	_	7	ABS	_	_
5	gur	_	gur	_	_	4	appos	_	_
6	za-ri-iq	_	to.Zarriq	_	_	7	DAT	_	_
7	he2-na-ab-sum-mu	_	give	_	_	2	ccomp	_	_

~~~

"To Abiati speak: 1 gur of barley to Zarriq let him give." (Hayes p.319, TCS 1,13)

Occasionally, units are postposed. To be confirmed: Annotate these as `nmod` (according to their function) or `appos` (according to their syntax)? 

	# Jagersma, Chap. 5 (11)						
	# ‘with five hides per (lit.“in”) two shekels of silver’						
	# (Nik 1:230 5:2-3; L; 24)						
	1	kù	kù.g	silver	7	LOC	marked on 3
	2	giĝ4	giĝ4	shekel	1	appos	unit, would be nmod if preposed
	3	2-a	2='a	two=LOC	2	nummod	
	4	/	_	_	7	punct	
	5	kuš	kuš	hide	1	ABL	marked on 5
	6	5-ta	5=ta	five=ABL	5	nummod	


### Discontinuous lists

Annotation is projective (there must be no crossing edges). If a list is interrupted by a clausal argument and then continued, attach the second list as an independent argument of the head of the first list, using the same dependency label as that one had. In the following example, the *gu4* does thus not continue the list of sheep that came before. 

~~~ conllu
1	[n]	_	NUM	NU	_	4	nummod	_	_
2	n	_	NUM	NU	_	1	nummod	_	_
3	5(u)	5(u)[ten]	NUM	NU	_	1	nummod	_	_
4	udu	udu[sheep]	NOUN	N	Number=Sing	15	ABS	_	_
5	ur-{d}lamma	Urlamma[1]	PROPN	PN	Animacy=Hum|Number=Sing	15	DAT	_	_
6	ensi2	ensik[ruler]	NOUN	N	Animacy=Hum|Number=Sing	5	appos	_	_
7	1(gesz2)	1(gesz)[sixty]	NUM	NU	_	9	nummod	_	_
8	1(u)	1(u)[ten]	NUM	NU	_	7	nummod	_	_
9	gu4	gud[ox]	NOUN	N	Number=Sing	15	ABS	_	_
10	_	_	_	_	_	9	list	_	_
11	ki	ki[place]	NOUN	N	Number=Sing	15	ABL	_	_
12	{d}szara2-kam-ta	Szarakam[1]	PROPN	PN	Animacy=Hum|Case=Gen,Abl|Number=Sing	11	GEN	_	_
13	ur-{d}lamma	Urlamma[1]	PROPN	PN	Animacy=Hum|Number=Sing	15	ERG	_	_
14	...	_	_	_	_	13	_	_	_
15	i3-dab5	n]	VERB	V	Number=Sing|Person=3|VerbForm=Fin	0	root	_	_

~~~
(P102314)

### Dates

For morphological annotation, see [Month Names and Year Names](https://cdli-gh.github.io/guides/month_names.html)

Head of a date phrase is the first element (day, month or year). Days are identified by numbers, using the nummod relationship. The head of a day phrase is thus u3 "day". Months are identified by proper names, so that iti "month" is modelled like an epithet, with the month name as head. Year names are normally sentential, we consider the word "mu" as syntactic head, and the actual year name a relative clause.

Dates are connected by means of the `date` dependency on semantic grounds. We see that as a specialization of `LOC` (resp. `L1`, in morphology) and in the UD mapping, both would be mapped to `obl`.

~~~ conllu
1	iti	_	month	_	_	0	date	_	_
2	a2-ki-ti	_	Akiti	_	_	1	appos	_	_
3	mu	_	year	_	_	1	LOC	_	_
4	an-sza-an{ki}	_	Anshan	_	_	5	ABS	_	_
5	ba-hul	_	destroyed	_	_	3	acl	_	_

~~~	
(P109483)

~~~ conllu
1	ud	_	day	_	_	0	date	_	_
2	30	_	29	_	_	1	nummod	_	_
3	la1	_	_	_	_	2	acl	_	_
4	1-kam	_	_	_	_	3	nummod	_	_
5	iti	_	month	_	_	6	nmod	_	_
6	Sze-kar-ra-gal2	_	Shekaragal	_	_	1	LOC	_	_
7	mu	_	year	_	_	6	LOC	_	_
8	Si-mu-ru-um{ki}	_	Simurum	_	_	14	ABS	_	_
9	Lu-lu-bu-um{ki}	_	Lulubum	_	_	8	appos	_	_
10	a-ra2	_	ninth.time	_	_	14	dep	_	_
11	10	_	_	_	_	10	nummod	_	_
12	la1	_	_	_	_	11	acl	_	_
13	1-kam	_	_	_	_	12	nummod	_	_
14	ba-hul	_	destroyed	_	_	_	_	7	acl	_	_

~~~
(no CDLI, Kang 252, Hayes 2000, p. 367)

Days, months and years are internally connected by a LOC (temporal) relationship because of their semantics.

Dates can be written discontinuously:
~~~ conllu
1	1	_	1	_	_	3	nummod	_	_
2	amar	_	calf	_	_	3	nmod	_	_
3	lulim	_	deer	_	_	14	root	_	_
4	munus	_	milk-fed	_	_	3	appos	_	_
5	ga	_	female	_	_	3	appos	_	_
6	ba	_	dead.	_	_	7	ABS	_	_
7	usz2	_	_	_	_	3	acl	_	_
8	ud	_	_	_	_	14	date	_	_
9	25-kam	_	_	_	_	8	nummod	_	_
10	ki	_	from 	_	_	14	LOC	_	_
11	Lu2-digir-ra-ta	_	Ludigira	_	_	10	GEN	_	_
12	{d}Szu-gi-uru-gu10	_	Shulgiurugu	_	_	14	ERG	_	_
13	szu	_	received	_	_	14	ABS	_	_
14	ba-ti	_	_	_	_	0	root	_	_
15	iti	_	Month 	_	_	16	nmod	_	_
16	Ki-sig2-{d}Nin-a-zu	_	Kisig-Ninazu	_	_	20	date	_	_
17	mu	_	year	_	_	16	LOC	_	_
18	Sza-asz-ru{ki}	_	Shashru	_	_	19	ABS	_	_
19	ba-hul	_	destroyed	_	_	17	acl	_	_

~~~
(no CDLI, Archi and Pomponio 347, Hayes p.371)

In this case, create multiple date relations with the respective root element.

TODO: consolidate guidelines and data:
- taglist recommends `appos` for `MN` (month name), with head being the word *iti* (month)
	- this is also implemented in the MTAAC pre-annotation
	- the examples above use `LOC` for dependencies within dates and `date` for the head element of a date
- taglist recommends `appos` for the clause after *mu*
	- apply `acl` systematically, check in the data
- check treatment in pre-annotation and annotation projection

### Complex numerals

Complex numerals can include *la2* 'minus', morphologically analyzed as `NF.V.ABS/PT/F` (=`acl`) here. Note that the numeral following *la2* is formally an absolutive argument: this is `NU1 la2 NU2 (NU2 is hung out from NU1)`, so la2=NF.V.ABS=acl; NU2= nsubj:passive.
As a design decision, annotation follows the semantic function of numerals as nummod.

~~~ conllu
1	1(gesz2)	1(gesz)[sixty]	NUM	NU	_	4	nummod	_	_
2	la2	la[hang]	VERB	V	_	1	acl	_	_
3	1(disz)	1(disz)[one]	NUM	NU	_	2	nummod	_	_
4	udu	udu[sheep]	NOUN	N	Number=Sing	12	ABS	_	_

~~~
`59 sheep' (P102313)

### Detached totals

As for the number at the end of administrative text, this is the total number of the animals recorded above, we take it as a note, and we tag it as `parataxis`.

~~~ conllu
1	1(gesz2)	1(gesz)[sixty]	NUM	NU	_	4	nummod	_	_
2	la2	la[hang]	VERB	V	_	1	acl	_	_
3	1(disz)	1(disz)[one]	NUM	NU	_	2	nummod	_	_
4	udu	udu[sheep]	NOUN	N	Number=Sing	12	ABS	_	_
5	8(disz)	8(disz)[one]	NUM	NU	_	6	nummod	_	_
6	masz2	masz[goat]	NOUN	N	Number=Sing	4	appos	_	_
7	szu	szu[hand]	NOUN	N	Number=Sing	8	appos	_	_
8	la2-a	la[entrust]	VERB	V	_	4	acl	_	_
9	ki	ki[place]	NOUN	N	Number=Sing	12	ABL	_	_
10	ab-ba-sa6-ga-ta	Abbasaga[1]	PROPN	PN	Animacy=Hum|Case=Gen,Abl|Number=Sing	9	GEN	_	_
11	be-li2-a-zu	Beli’azu[1]	PROPN	PN	Animacy=Hum|Case=Erg|Number=Sing	12	ERG	_	_
12	i3-dab5	n]	VERB	V	Number=Sing|Person=3|VerbForm=Fin	0	_	_	_
13	iti	iti[month]	NOUN	N	Number=Sing	12	date	_	_
14	ses-da-gu7	Sesdagu[1]	PROPN	MN	Number=Sing	13	appos	_	_
15	mu	mu[year]	NOUN	N	Number=Sing	13	LOC	_	_
16	{d}gu-za	guza[chair]	NOUN	N	Number=Sing	18	ABS	_	_
17	{d}en-lil2-la2	Enlil[1]	PROPN	DN	Animacy=Hum|Case=Gen,Abs|Number=Sing	16	GEN	_	_
18	ba-dim2	dim[create]	VERB	V	Number=Sing|Person=3|Voice=Mid	15	acl	_	_
19	1(gesz2)	1(gesz)[sixty]	NUM	NU	_	12	_	_	_
20	7(disz)	7(disz)[one]	NUM	NU	_	19	nummod	_	_

~~~
(P102313)


## Changes

These are revisions of the original approach to annotation, which need to be changed either above or in the gold data.

- units: Change modelling in gold data to `number -nummod-> product <-appos- unit` (instead of `number -nummod-> [product -nmod-> unit]`). Check whether there are any such cases in the guidelines. 
- acl: originally, the morphological feature was used for annotation (e.g., SUB, TL, etc.). Replace globally with `acl`. This is done here but must be applied to gold data. Note that the GDrive tag list preserves `SUB`, mapped to `acl:relcl`
- connect transactions by parataxis (not by list, as this is used for numbered products and could be conflated)
- change internal structure of complex numerals to appos (add there "implicit addition") rather than compound; for la2, see morphology guidelines 
- TODO: synchronize with (https://cdli-gh.github.io/guides/month_names.html), (https://cdli-gh.github.io/guides/verbal_chain_slot_system.html), (https://cdli-gh.github.io/guides/lists.html)
- TODO: add material from https://drive.google.com/drive/folders/1bYRho0QkHCiTE-ajPlvJTTmM8bViI4da
- iti+month name: current pre-annotation: iti is head, month in apposition (fix in docu and data)
- complex numbers: head is nummod, internal relation produced by pre-annotation is also nummod; change guidelines and examples (currently compound); add comment that an alternative analysis would be with `appos` (with appos for implicit addition), but that (as a design decision), this is not done here.
- TODO: "11. As for giri3 PN (by the means of PN), and kishib PN (by the seal of PN), we tag giri3/kishib as obl, mark dependent as GEN (in data and doc)" => tag giri3 as "via" (giri3 being [nominal] head), kiszib3 as "under" (kiszib3 being [nominal] head) with genitive complement ("under the seal of ...")
- double-check ziga role, cf. analysis in P102314
- advcl does exist (tukumbi)
- year name: annotate as `acl`, not as `ccomp` (because there are instances where this is explicitly marked) not as `appos` (because they are clausal)
- ABS heads of copular clause: annotate (head of) copular predicate as root, e.g.

	# Jagersma, Chap. 4 (22)						
	# ‘These are the barley rations and barley supplies of Bau’s men.’						
	# (STH 1:4 2:3; L; 24)						
	1	še-ba	[še.ba	[ration.barley	0	root	ABS => copular predicate
	2	še-ĝar	še.ĝar	supply.barley	1	appos	implicit conjunction
	3	lú	[lú	[man	1	GEN	
	4	{d}ba-ú-ke4-ne-kam	[ba.ú=ak]=enē=ak]=Ø]='am	[Bau=GEN]=PL=GEN]=ABS]=be:3N.S	3	GEN	


## Open issues

### `advmod`

So far, we posit that adverbials don't really exist, and it seems most adverbials can be analyzed differently, e.g., *eger* as a nominal with an oblique case (`LOC` for spatial interpretation "on the other side" or `ABL` for temporal interpretation "after(wards)"). 
This is in line with Jagersma, p.83:

> Sumerian lacks a distinct word class of adverbs. It expresses adverbial meanings in other ways,
mostly with adjectives, verbal affixes, or noun phrases. As Poebel (1923: §388) already observed,
the most common way is by means of a noun phrase. Thus, the Sumerian equivalent of
an English time adverb is a noun phrase in a case which can have a temporal meaning – the
locative, ablative, or terminative.

	# Jagersma, Chap. 4 (30)					
	# ‘then (lit.“on this day”)’					
	# (Ent.8 7:7; L; 25)					
	1	u4-ba	u4.d=be='a	day=this=LOC	0	LOC

	# Jagersma, Chap. 4 (32)			
	# ‘Later (lit.“on the back”) Namhani, the scribe said:(...).’			
	# (NG 69 8-9; U; 21)			
	1	eger-a	eger='a	back=LOC
	2	nam-ha-né	nam.ha.né	Namhani
	3	dub-sar-e	dub.sar=e	scribe=ERG
	4	/	_	_
	5	(...)	_	_
	6	bí-in-du11	Ø-bi-n-du11.g-Ø	VP-3N.OO-3SG.A-say-3N.S/DO

	# Jagersma, Chap. 4 (38)					
	# ‘there (lit.“in the place of this”)’					
	# (Cyl A 10:26; L; 22)					
	1	ki-ba	ki=be='a	place=its=LOC	0	LOC

	# Jagersma, Chap. 8 (57)			
	# ‘on the reverse of our tablet’			
	# (UET 6/2:150 1; Ur; OB)			
	1	eger	eger	back
	2	dub-me-ka	dub=mē=ak='a	tablet=our=GEN=LOC

	# Jagersma, Chap. 4 (33)			
	# ‘afterwards (lit.“from its back”)’			
	# (NG 103 8; L; 21)			
	1	eger5-bé-ta	eger5=be=ta	back=its=ABL


	# Jagersma, Chap. 7 (274)			
	# ‘after stock-taking (lit. “from the back of stock-taking”)’			
	# (Nik 1:156 3:4; L; 24)			
	1	eger4	eger4	back
	2	gurum2-ma-ta	gurum2=ak=ta	stock.taking=GEN=ABL

"Noun phrases with non-finite verbal forms as their heads can also be used to express adverbial
meanings" (Jagersma, p. 84)

	# Jagersma, Chap. 4 (39)					
	# ‘He brought it to him into the temple joyfully (lit.“in being happy”).’					
	# (Cyl A 7:30; L; 22)					
	1	é-a	é='a	house=LOC	3	LOC
	2	húl-la	húl-Ø='a	be.happy-NFIN=LOC	3	acl+LOC
	3	ì-na-ni-ku4	'i-nna-ni-n-ku4.r-Ø	VP-3SG.IO-in-3SG.A-enter-3N.S/DO	0	root

Note that the dependency label `ADV` does not refer to adverbial function, but it refers to a morphological case (*adverbial case*). Its UD equivalent is thus `obl`, not `advmod`.

	# Jagersma, Chap. 4 (40)						
	# ‘He built his master’s temple in the right way.’						
	# (Cyl A 24:8; L; 22)						
	1	é	é	house	4	ABS	
	2	lugal-na	lugal=ane=ak=Ø	master=his=GEN=ABS	1	GEN	
	3	zi-dè-éš	zi.d=eš	rightness=ADV	4	ADV	note that this is not advmod, but adverbial case
	4	mu-řú	Ø-mu-n-řú-Ø	VP-VENT-3SG.A-erect-3N.S/DO	0	root	


TODO: provide a list of "adverbials"

In accordance with the principle to annotate numerals as `nummod`, the following should be annotated without case: 

	# Jagersma, Chap. 4 (34)						
	# ‘subsequently (lit “for the second one”)’						
	# (Cyl A 9:5; L; 22)						
	1	2-kam-ma-šè	min-kamma=še	two-ORD=TERM	0	nummod	more correct would be nummod+TERM


### heads of copular clauses with clausal predicate

TOFIX: predicate should be head of copular predicate. In the cases below, this is not the element that carries the copula, but the adjacent (often ABS) argument. The analyses below are thus partially wrong.

	1	še	še	barley
	2	šuku-řá	šuku.ř=ak	subsistence=GEN
	3	/	_	_	
	4	lú	lú	man	
	5	amar-ki	amar.ki	Amarki	
	6	/	_	_		
	7	ugula	ugula=ak	foreman=GEN	
	8	/	_	_	
	9	ba-ug7-ge-a-kam	Ø-ba-'ug7-eš-'a=ak=Ø='am	VP-MM-die:PLUR-3PL.S/DO-NOM=GEN=ABS=be:3N.S

Jagersma, Chap. 27 (10)						
‘This is the subsistence barley of Amarki the foreman’s men who have died.’						(VS 14:39 1:2-5; L; 24)					

What's the head of the clause, here? Without the final copula *'am* in (9), everything is a modification of *sze* in (1):

	[sze <-GEN- lú Amarki <-acl- baugea]
	
But with the copula, *sze* in (1) actually becomes the ABS argument of the outer copular clause (marked on 9 as its final dependent):

	[sze <-GEN- lú Amarki ] -ABS-> baugeakam

With this annotation, we completely loose the information about the relation between the *lú Amarki* and *baugea* (they are the subjects).

The "correct" annotation would require sub-token dependencies:

	[sze <-GEN- lù Amarki <-acl- baugea] -ABS-> -am

Suggestion: Follow the interpretation of the copula as an emphatic particle that modifies the final dependent of *sze*. This means to annotate the relative clause, not the copular clause

	[sze <-GEN- lú Amarki <-acl- baugea]

If this phrase requires a clausal interpretation, we assume that it is a nominal clause (despite the overt copula!), so that *sze* would be head of the clause.

### internal structure of functional dependents

analysis of *giri3 XY "gave"*

	[giri3 -nmod-> XY] -obl-> "gave"

semantically, that makes a lot of sense, but it is inconsistent with the idea of having morphology-driven syntactic annotation. the case is not always missing, and at least these, should really be

	[giri3 <-GEN- XY.GEN] -obl-> "gave"

discussion:
- the annotation of `GEN` as `obl` stated in the taglist
- TODO: check treatment in pre-annotation and annotation projection

### complex dependencies

Clarify whether dependencies with compound labels (`GEN+disloc`, `acl+TERM`, `GEN+TERM`, etc.) can be reliably identified from pre-annotation and annotation projection. Otherwise, simplify.

### nam-erim2-am3

This is a frequent formula in ditilas, roughly meaning "it is an oath". According to Hayes (p.346 and elsewhere), this is nominal, with the preceding (agentive) noun presumably in genitive. According to the general structure of ditilas, however, we would expect a sentential element here. In the absence of a theory-guided decision, we annotate this in accordance with the English translation as an (implicit) copula. Hayes (p.346) suggests the person swearing the oath to be the genitive argument of the nominal element in the copular predicate. As the genitive is unmarked, we follow the previous analysis in the PPCS and annotate it as copular argument, instead. (Note that PPCS annotated copular arguments as ERG, whereas we annotate these as ABS.)

~~~ conllu
1	PN1	_	PN	_	_	4	ERG	_	_
2	dam-ce3	_	wife.TERM	_	_	3	TERM	_	_
3	ha-tuku	_	have	_	_	4	ccomp	_	_
4	bi2-in-dug4-ga	_	say.NOM	_	_	7	acl+ABS	_	_
5	PN2	_	PN	_	_	7	ABS	_	_
6	PN3	_	PN	_	_	5	appos	_	_
7	nam-erim2-am3	_	swear.COP	_	_	0	root	_	_

~~~

"PN  (and) PN  swore that PN  declared: 'I will marry (her)'" (NG 15:6-9, 16:6-11, example from PPCS manual)


~~~ conllu
1	di-til-la	_	Ditila	_	_	0	root	_	_
2	{m}szesz-kal-la	_	Sheshkala	_	_	7	ERG	_	_
3	dumu-ur-{d}lamar-ka-ke4	_	son.of.Ur-Lamar	_	_	2	appos	_	_
4	arad2-	_	slave	_	_	7	ccomp	_	_
5	ur-{d}sahar-{d}ba-u2-ka	_	of.Ur-Sahar-Bau	_	_	4	GEN	_	_
6	nu-u3-me-en3	_	not.COP	_	_	4	cop	_	_
7	bi2-in-dug4	_	said	_	_	1	parataxis	_	_
8	ur-{d}lamar	_	to.Ur-Lamar	_	_	20	LOC	_	_
9	ab-ba-szesz-kal-la-ke4	_	father.of.Sheshkala	_	_	8	appos	_	_
10	e2-	_	in.the.house	_	_	20	LOC	_	_
11	ur-{d}sahar-{d}bau-u2	_	of.Ur-Sahar-Bau	_	_	10	GEN	_	_
12	dumu	_	son	_	_	11	appos	_	_
13	na-mu-ka	_	of.Namuka	_	_	12	GEN	_	_
14	sze-ba	_	barley.rations	_	_	20	ABS	_	_
15	siki-ba	_	wool.rations	_	_	14	appos	_	_
16	szu	_	for.the.hand	_	_	20	ABL	_	_
17	al-la	_	of.Alla	_	_	16	GEN	_	_
18	dub-sar-ta	_	scribe	_	_	17	appos	_	_
19	nam-arad2-sze3	_	because.of.arad2.status	_	_	20	TERM	_	_
20	ba-na-sum	_	given	_	_	30	acl	_	_
21	u3	_	and	_	_	20	cc	_	_
22	ur-{d}lamar-ke4	_	to.Ur-Lamar	_	_	27	ERG	_	_
23	szesz-kal-la	_	Sheshkala	_	_	27	ABS	_	_
24	arad2	_	slave	_	_	23	appos	_	_
25	ki	_	on.premises	_	_	27	LOC	_	_
26	ur-{d}sahar-{d}ba-u2-ka-am3	_	of.Ur-Sahar-Bau	_	_	25	GEN	_	_
27	i3-tud-da	_	born	_	_	20	conj	_	_
28	lu2-dug3-ga	_	Luduga	_	_	30	ABS	_	_
29	du-du-mu	_	Dudumu	_	_	30	appos	_	_
30	nam-erim2-am3	_	swear.oath	_	_	7	parataxis	_	_

~~~
"Ditila. Sheshkala, the son of Ur-Lamar, said: 'I am not the slave of Ur-Sahar-Bau!'. It is an oath of Luguda and Dudumu that barley rations and wool rations had been given to Ur-Lamar, the father of Sheshkala, in the house of Ur-Sahar-Baz, the son of Namu, on the authority of Alla the scribe, because of his status as slave, and that Sheshkala the save was born to Ur-Lamar on the very premises of Ur-Sahar-Bau."" (Hayes p.334, NSGU 32)


### Suppliers and receivers

~~~ conllu
1	a-bi-a-ti	_	to.Abiati	_	_	2	DAT	_	_
2	u3-na-a-dug4	_	speak	_	_	0	root	_	_
3	1	_	1	_	_	4	nummod	_	_
4	sze	_	barley	_	_	7	ABS	_	_
5	gur	_	gur	_	_	4	appos	_	_
6	za-ri-iq	_	to.Zarriq	_	_	7	DAT	_	_
7	he2-na-ab-sum-mu	_	give	_	_	2	ccomp	_	_

~~~

"To Abiati speak: 1 gur of barley to Zarriq let him give." (Hayes p.319, TCS 1,13)

If no verb is provided, mark suppliers as ERG, receivers as DAT and commodities as ABS.

### Multiple agents in a transaction

When we have not only one obl, we use not use `conj` to link them together, but treat them as independent arguments. E.g., in

~~~ conllu
1	...	_	_	_	_	_	_	_	_
2	u4	_	N	_	_	1	date	_	_
3	...	_	NU	_	_	2	nummod	_	_
4	ki	_	N	_	_	1	obl	_	_
5	...ta	_	PN.GEN	_	_	4	GEN	_	_
6	kiszib	_	N	_	_	1	obl	_	_
7	...	_	PN.GEN	_	_	6	GEN	_	_

~~~
"on the 4th day, from the place of PN, through the seal of PN"

Current approach to provide different labels for these agents. Without explicit verb, the head is the transferred good. In UD mapping, these relations become `obl`. CDLI labels yet to be determined. TODO: consult annotation projection and pre-annotation.

### Discussion of Date structure

1. Problems about temporal indication, day, month and year:

~~~ conllu
1	...	_	...	_	_	_	_	_	_
2	u4	_	N	_	_	_	_	_	_
3	2(u)	_	NU	_	_	_	_	_	_	
4	3-kam	_	NU.GEN.COP-3-SG	_	_	_	_	_	_

~~~
"For the day,"

Different possible analyses for (implicit) morphology of *3-kam*.

A. if we take it as “on the 23rd day” and we need add a L1, we have 

~~~ conllu
1	...	_	...	_	_	_	_	_	_
2	u4	_	N	_	_	1	obl	_	_
3	2(u)	_	NU	_	_	2	nummod	_	_	
4	3-kam[-'a]	_	NU.GEN.COP-3-SG.L1	_	_	2	flat	_	_

~~~

B. if we take it as an interjected phrase, “the 23rd day”, we have:

~~~ conllu
1	...	_	...	_	_	_	_	_	_
2	u4	_	N	_	_	1	discourse	_	_
3	2(u)	_	NU	_	_	2	nummod	_	_	
4	3-kam	_	NU.GEN.COP-3-SG	_	_	3	flat	_	_

~~~


C. if we take it as an interjected norminal clause, “(it is the 23rd day)”, we have:

~~~ conllu
1	...	_	...	_	_	_	_	_	_
2	u4	_	N	_	_	1	parataxis	_	_
3	2(u)	_	NU	_	_	2	nummod	_	_	
4	3-kam[-0]	_	NU.GEN.COP-3-SG.ABS	_	_	3	flat	_	_

~~~

The manual morphology annotations goes with option (A). 
For syntax annotation, we differ from this original concept by having `date` as a dependency (to be able to retrieve all examples for future revisions) and to replace `flat` by `nummod` (for all numerals). TODO: check pre-annotation and annotation projection. 

For the month, the situation is similar, and we need to decide the relationship between the iti and MN.
For the year, the situation is more complicated, because not only we need to decide the case of ‘mu’, but also the relationship between ‘mu’ and the clause followed.
We also need to decide whether MU and ITI are in `conj` relationship.
(At the moment, they are internally connected by `LOC`, as it refers to a month *in* or *of* a particular year. This is semantically motivated, but it has no morphological basis.)

There is another structure of temporal indication, 

~~~ conllu
1	iti	_	_	_	_	_	_	_	_
2	X[-ta],	_	_	_	_	_	_	_	_
3	u4	_	_	_	_	_	_	_	_
4	NU[-kam]	_	_	_	_	_	_	_	_
5	zal-la-’a	_	_	_	_	_	_	_	_

~~~

"After the NUth day passed from the month" (obl phrase)

In this case, we ignore the copula, we define NU-am3 as NU, not V:

~~~ conllu
1	iti	_	_	_	_	_	_	_	_
2	X[-ta],	_	_	_	_	_	_	_	_
3	u4	_	_	_	_	_	_	_	_
4	NU-am3	_	_	_	_	_	_	_	_
5	zal-la-’a	_	_	_	_	_	_	_	_

~~~

Note: this is consistent with the application of `nummod` to all occurrences of numerals.

### Dependency syntax: Other uses of the copula

Emphatic copula/standard marker ("STM")

~~~ conllu
1	šag₄	_	heart	_	_	6	ERG	_	_
2	en-lil₂-la₂-ke₄	_	DN=GEN=ERG	_	_	1	GEN	_	_
3	id2idigna-am₃	_	WN=STM	_	_	1	STM	acl?	_
4	a	_	water	_	_	6	ABS	_	_
5	dug₃-ga	_	sweet-PT=ABS	_	_	4	amod	_	_	
6	nam-de₆	_	MOD-VEN-3.SG.NH.A-bring-3.SG.P	_	_	0	root	_	_

~~~						
“The heart of the god Enlil brought sweet water like the river Tigris.”	(Q000377)					

The third word contains the "standard marker"; this actually contains the copula, but lexicalized into a cleft-like construction. This is evident from the ergative case that the subject receives from the verb in line 6. However, it does not depend on szag, because otherwise, the ergative marker would have been placed after the STM. Nevertheless, it is analyzed as an acl here.

An alternative (and shallower) analysis would be to interpret the copula literally, and to postulate a parataxis relation ("The heart of Enlil is (like) the Tigris; he brought sweet water.") However, the ergative of sza3 remains unexplained, then. 

The most consistent way to annotate such cases would be to interpret the copula like a morphological case (or, if non-clitic, as a ,focus particle). Requires deeper study. This is, however, not relevant to administrative texts.

Both these models violate the underlying morphology.

Hayes mentions that copula seems to be able to replace any case marker (but can also appear in combination with them).

### Hard examples

Collect examples here that are not satisfactorily analyzed, yet.

A headless relative clause serving as predicate of a copula sentence whose root is on the same token:

	# Jagersma, Chap. 27 (71)						
	# ‘It is (the) one that lives with PN, the fattener.’						
	# (DP 338 1:2-4; L; 24)						
	1	PN	PN	PN	5	COM	marked on 3
	2	/	_	_	1	punct	
	3	gurušta-da	gurušta=da	fattener=COM	1	appos	
	4	/	_	_	5	punct	
	5	mu-da-lu5-ka-am6	Ø-mu-n-da-lu5.k-Ø-'a=Ø='am	VP-VENT-3SG-with-live-3N.S/DO-NOM=ABS=be:3N.S	0	root	
	
Token 5 is acl+ABS serving as predicate (= head) of the copular clause (to be marked on token 5). Could be annotated as clause (`root`, `parataxis` etc., depending on context) or as argument (`acl+ABS`). In either case, the attachment of token 1 to the inner (relative) clause rather than to the outer (copular) clause can only be inferred from the inner relative clause not being annotated as `amod` (resp. `ABS` because `amod+ABS` is to be reduced to `ABS`).

	# Hayes p.354, NSGU 15								
	1		1	di-til-la		Ditila	0	root	
	2		2	dug4-ga-ni-zid		Duganizid,	5	ERG	
	3		2	dumu-		the son	2	appos	
	4		2	szesz-kal-la-ke4		of Sheshkala	3	GEN	
	5		3	igi-ni		testified and said	16	acl	nominalizer marked at bi-in-dug4-ga -- I'm not sure whether this is the verb of a nominal complement
	6		3	in-{ga2}gar{ar}		and said	5	parataxis	
	7		4	mu-lugal		"By the name of the king,		ABS	"It is hard to say how mu-lugal ties in syntacically with the rest of the sentence. Perhaps, mu-lugal is the subject of a nominal sentence and what follows is a predicate." (Hayes p.355)
	8		5	nin-dub-sar		Nindubsar,	12	ABS	
	9		5	dumu-		the daughter	8	appos	
	10		5	ka5-a		of Kaa,	9	GEN	
	11		6	dam-sze3		as a wife	12	TERM	
	12		6	HA-tuku		let me take her."	7	acl	
	13		6	bi2-in-dug4-ga			6	ccomp	nominalizer extends to the testimony
	14		7	nin-nam-ha-ni		of Ninnamhani	16	ABS	Hayes postilates genitive here, we use ABS (copular argument)
	15		8	ur-{d}lamar		and Ur-Lamar	14	appos	
	16		9	nam-erim2-am3		it is an oath.	1	parataxis	
	17		10	dug4-ga-ni-zid		Duganizid	19	ERG	
	18		11	nin-dub-sar		Nindubsar	19	ABS	
	19		11	ba-an-tuku		married.	16	parataxis	
	20		12	mu-lugal		By the name of the king	31	TERM	mu...sze3 "because" (acl+GEN+TERM), marked on ba-ni-gad3-da-sze3
	21		12	dug4-ga-ni-zid-da		to Duganizid,	29	LOC	instead of earlier DAT
	22		13	ab-ba-ni		while (Duganizig's) father	24	ABS	
	23		13	ama-ni		and mother	24	ABS	not appos, but double ABS according to Hayes p.356
	24		13	nu-u3-zu-bi		were unaware,	21	acl+COM	-bi stands for -bi-da, morph. conjunction; for clausal arguments, not annotated as conjunction, but as acl+COM
	25		14	nig2-{d}ba-u2		Nig-Bau	29	ERG	before, we annotated the swearer as ABS, but here, we take mu-lugal to be ABS, hence ERG. find a systematic solution
	26		14	ab-ba-		father	25	appos	
	27		14	Ha-la-{d}ba-u2-ka-ke4		of Hala-Bau	25	GEN	
	28		15	mu-lugal		By the name of the king	29	ABS	case unclear
	29		15	ba-ni-pad3-da-sze3		had sworn	20	acl+GEN	mu...sze3 "because" (acl+GEN+TERM)
	30		16	Ha-la-{d}ba-u2-ka-ke4		Hala-Bau 	31	ERG	Hayes gives no case, but -e is ERG (the action isn't agentive, though)
	31		16	ba-tag4		was set aside.	19	parataxis	
	32		17	ur-ki-gu-la		Ur-Kigula	33	ABS	
	33		17	maszkim		was bailiff.	31	parataxis	
	#		#	(space)					
	34		18	lu2-{d}szara2		Lu-Shara,	38	ABS	
	35		19	lu2-{d}ib-gal		Lu-Ibgal,	34	appos	
	36		20	lu2-digir-ra		Ludigira,	34	appos	
	37		21	ur-{d}isztaran		and Ur-Isztaram	34	appos	
	38		22	di-kur5-bi-me		were the relevant judges.	33	parataxis	
	39		23	mu		The year	1	date	
	40		24	...		...	39	ccomp	



## Mapping to UD

incomplete

	(top-level node)	=>	root
	ABL	=>	obl
	ABS	=>	nsubj; nsubj:passive; obj
	acl	=>	acl
	advcl	=>	advcl
	advmod	=>	advmod
	appos	=>	appos
	cc	=>	cc
	ccomp	=>	ccomp
	compound	=>	compound
	conj	=>	conj
	DAT	=>	iobj
	ERG	=>	nsubj
	GEN	=>	nmod
	giri3	=>	obl
	kiszib	=>	obl
	LOC	=>	obl
	mark	=>	mark
	nmod	=>	nmod
	nummod	=>	nummod
	parataxis	=>	parataxis
	TERM	=>	obl
	vocative	=>	vocative

tbc: does compound exist? is the list complete?

## How to edit this document

### Formatting example annotations

MTAAC annotations are originally provided in a CoNLL dialect. CoNLL is a family of tabular formats that feature
- one word per line
- within each line, a fixed number of tab-separated fields (columns)
- within each column, one type of annotation
- comments and headers marked by #
- sentences or documents separated by at least one empty line

CoNLL dialects differ with respect to the kind of annotation they provide and the order of columns. The Annodoc visualization provides partial support for two CoNLL dialects, CoNLL-X and CoNLL-U, with a focus on syntactic dependencies. Note that the original column structure of the data may require adjustments when used in this document. We generally use the CoNLL-U template.

The [CoNLL-U](http://universaldependencies.github.io/docs/format.html) format is another CoNLL format format for representing dependency parses,
developed in the 
[Universal Dependencies](universaldependencies.github.io/docs/).

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

The CoNLL-U format defines 10 columns separated by TAB (in Annodoc: space), again, only fields 1 `ID`, 2 `WORD`, 4 `POS`, 7 `HEAD` and 8 `EDGE` are visualized.

Note that Annodoc supports either space or tab as column separator, but no mixture. Furthermore, exactly ten columns are required, it is not admissable to omit the trailing empty columns.
Also note that Annodoc *requires* numerical IDs, starting with 1. CDLI IDs must be replaced, fragments from actual annotations must be adjusted in their ID and HEAD information.
Furthermore, a CoNLL-U snippet must be ended with an empty line

As an alternative, the Stanford Dependency format can be used:

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

funded by T-AP (NEH, SSHRC, DFG); MTAAC 

### Contributors
CC, EPP, IK, JW, LR, ...

This page is based on a fork of the [Annodoc](http://www2.lingfil.uu.se/SLTC2014/abstracts/sltc2014_submission_32.pdf) template, originally under (https://github.com/spyysalo/annodoc). See there for documentation.

### References
- PPCS (2004), PPCS (Penn Parsed Corpus of Sumerian): A Brief Introduction to the Syntactic Annotation System of the PPCS, version of 6/14/04, available from https://www.yumpu.com/en/document/view/12162126/ppcs-penn-parsed-corpus-of-sumerian-a-brief-introduction-to-the- and https://web.archive.org/web/20070708210654if_/http://psd.museum.upenn.edu/ppcs/ppcs-manual.pdf, author is Fumi Karahashi
- Joachim KRECHER (1987), Morphemless Syntax in Sumerian as Seen on the Background of Word-Composition in Chukchee, ASJ 9, 1987
- Zolyomi 2017

## Appendix

### List of compound verbs

	ki  ag
	igi bar
	a de2
	szu de6
	en.nu.ug3 du3
	szu du7
	igi du8
	di dug4
	mi2 dug4
	szu dug4
	szu.tag dug4
	a2 e3
	pa e3
	ad gi4
	ki-bi gi4
	sa gi4
	szu gi4
	ma2 gid2
	szu gid2
	igi gal2
	kiri4 szu gal2
	zi sza3 gal2
	giri3-sze3 gar
	igi gar
	inim gar
	ki gar
	szu gar
	gisz hur
	ki hur
	igi il2
	sag il2
	nam kud
	nam.erim2 kud
	szu nigin
	szu ra
	na ri
	a ru
	si sa2
	szu-sze3 si
	szu sud
	gesztug2 sum
	ki sur
	gisz tag
	ki tag
	szu tag
	szu tag4
	en3 tar
	nam tar
	szu ti
	a tu5
	gisz tuku
	ma2 u5
	szu us2
