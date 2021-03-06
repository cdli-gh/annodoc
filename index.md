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

Draft for annotation guidelines for syntax, under development. Currently documents the design decisions taken in the development of syntax pre-annotation tools. The goal is, however, to provide a full-fledged annotation scheme for Sumerian, a small gold corpus and its export to UD v.2.

At the moment, this document summarizes
- decisions previously taken in morphological annotation and annotation experiments
- design decisions of automated pre-annotation and projection tools (morphology-based pre-annotation, transaction parser, annotation projection)
- examples from the literature to extend or revise both aforementioned 

Note that it requires substantial internal consolidation before it can be used for actual annotation.

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

	# Jagersma, Chap. 7 (56)						
	# ‘planks for (“of”) boats of thirty gur and boats of fifteen gur’						
	# (MVN 20:93 obv.5 rev. 2; U;21).						
	1	{ĝiš}mi-rí-za	[mi.rí.za	[plank	0	root	
	2	má	[má	[boat	1	GEN	marked on 8
	3	30	[30	[30	4	nummod	
	4	gur	gur=ak]	gur=GEN]	2	GEN	
	5	ù	ù	and	2	cc	
	6	má	má	boat	2	conj	
	7	15	[15	[15	8	nummod	
	8	gur-ka	gur=ak]=ak]	gur=GEN]=GEN]	6	GEN	

A note on parsing: Although Sumerian morphology encodes many syntactic relations explicitly, syntactic parsing cannot be simply reduced to morphological parsing because the scope of a particular morpheme (markers of case, possession, number or syntactic subordination) needs to be recovered. 

	# Jagersma, Chap. 7 (66)						
	# ‘from the room of Shulshaganak which is built in the gate of Bau’						
	# (VS 27:2 3:3-5; L; 24)						
	1	é	é	room	0	ABL	marked on 7
	2	dšul-šà-ga-na-ka	DN=ak	DN=GEN	1	GEN	
	4	a-bul5-la	a.bul5.la	gate	7	LOC	
	5	dba-ú-ka	ba.ú=ak='a	Bau=GEN=LOC	4	GEN	
	7	řú-a-ta	řú-Ø-'a=ta	erect-NFIN-NOM=ABL	1	acl	

The mapping of case labels to universal dependency labels is performed as a postprocessing step. Adnominal modifiers with case marking are mapped to `nmod`, oblique cases are  to `obl`, dative to `iobj`, ergative to `nsubj`. The mapping of absolutive is more challenging, as it needs to be disambiguated between `nsubj` (for intransitives) and `obj` (for transitives), see discussion below.

Following the morphological principle in syntactic annotation, these labels are being used only if indicated in the morphology annotation. Morphologically unmarked adnominal modification is annotated as `appos`. The same principle applies to the annotation of clausal co(sub)ordination: Morphologically marked subordination is annotated as `acl`, morphologically or syntactically marked coordination as `conj`, unmarked co(sub)ordination as `parataxis`.

Note: Morphological marking of case stacking seems to be limited if the same morpheme is to be repeated more than two times.
If a case can be reliably reconstructed, annotate it in dependency syntax as case, not as `appos`. The objective is that
in these cases, it is unclear which of the (syntactically required) case markers are omitted.
In case of ambiguity between a case and `appos` in these cases, annotate `appos`

	# Jagersma, Chap. 7 (49)						
	# ‘This is the ceremonial gift of the wife of the administrator of the Ebabbar temple.’						
	# (DP 2171:2-3; L;24)						
	1	maš da ri-a	maš da ri.a	ceremonial.gift	0	root	ABS => copular predicate
	3	dam	dam	wife	1	GEN	
	4	saĝĝa	saĝĝa	administrator	3	GEN	
	5	é-bar6-bar6-ka-kam	é.bar6.bar6=ak=ak=Ø='am	Ebabbar=GEN=GEN=ABS=be:3N.S	4	GEN

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
In the gold data, `dep` should be used if a particular source doesn't define the syntactic relations of a particular fragment. This includes, for example, the internal structure of year names according to Jaworski (2009).

Also, if an example is incompletely given, `dep` can be used to attach the symbols that mark the omission:

	# Jagersma, Chap. 7 (5)						
	# ‘the Dublamah – this temple was unbuilt, apart from that it had been (a...since time immemorial)’						
	# (FAOS9/2 Amarsuen123-8; Ur;21)						
	1	dub-lá-mah	dub.lá.mah	Dublamah	0	root	
	3	(...)	(...)	(...)	1	dep	
	5	ì-me-a-na-an-na	'i-me-Ø-'a=nanna	VP-be-3N.S-NOM=apart.from	1	acl	# not amod, as there are dependents in 3
	7	é-bé	é=be=Ø	house=this=ABS	8	ABS	
	8	nu-řú-àm	nu=řú-Ø='am	NEG=erect-NFIN=be:3N.S	1	acl	

In general, `dep` should not have further dependents. If a specific assumption leads you to assume that a dependency relation between an omitted/broken expression and a readable expression holds, annotate the relation, not `dep`.

As for head of `dep`, attach it as high as possible without creating a non-projective tree.

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

Semantically, the following would be `acl` but as the verb has no overtly realized arguments, we annotate that as `amod`.

	# Jagersma, Chap. 27 (65)						
	# ‘on to the field which he has seized’						
	# (TCS 1:229 7; L; 21)						
	1	a-šà	a.šà.g	field	0	LOC	marked on 2
	2	in-dab5-ba-na	'i-n-dab5-Ø-'a=ane='a	VP-3SG.A-seize-3N.S/DO-NOM=his=LOC	1	amod	no overt arguments, hence amod, not acl

For headless "adjectives" (relative clauses without independent arguments), annotate only case, not `amod`: If adjectives (including argument-less relative clauses) appear without nominal head, but with a grammatical role (morphological case) in a clause, treat them like nouns, i.e., use the morphological case for their annotation. Likewise, lexicalized deverbal nominals are annotated like nominal arguments. This is because such constructions are systematically ambiguous between an interpretation as lexicalized nominals and as nominalized clauses.

	# Jagersma, Chap. 7 (326)					
	# ‘from (the place of) Banzigen (“He/She let me rise”)’					
	# (Iraq 22 pl.19 MLC 42 2; D; 21)					
	1	ki	ki	place	0	ABL
	2	ba-zi-ge-na-ta	Ø-ba-n-zi.g-en=ak=ta	VP-MM-3SG.A-rise-1SG.S/DO=GEN=ABL	1	GEN	not: amod+GEN

	# Jagersma, Chap. 27 (34)						
	# ‘one in which it is sieved for me’						
	1	gema-an-sim	Ø-ma-n(i)-sim-Ø	VP-1SG.IO-in-sieve-3N.S/DO	0	ABS	not: amod+ABS

Etymologically, this is a headless relative clause, but it is lexicalized as a noun; according to CDLI conventions, that is originally an `amod`, because it comes without arguments. 

	# Jagersma, Chap. 27 (36)						
	# ‘one who has died’						
	1	ba-úš	Ø-ba-'úš-Ø	VP-MM-die-3SG/3N.S/DO	0	ABS	not: amod+ABS

Treat nominalized verbs with case like regular nouns (i.e., not `amod.ABS`, but `ABS`):

	# Jagersma, Chap. 24 (15a)						
	# ‘when the regular expenditures (lit. “what was raised of what is firm in the hand”) have been raised from it’						
	# (TPTS 80 4; U; 21)						
	1	zi-ga	zi.g-Ø-'a	rise-NFIN-NOM	4	ABS	treated like noun
	2	šu-a	šu='a	hand=LOC	3	LOC	
	3	ge-na	ge.n-Ø-'a=ak=Ø	be.firm-NFIN-NOM=GEN=ABS	1	acl.GEN	
	4	ù-ub-ta-zi	'u-b-ta-zi.g-Ø	REL.PAST-3N-from-rise-3N.S/DO	0	advcl	

Etymologically, this is a headless relative clause, but it is lexicalized as a noun.

	# Jagersma, Chap. 27 (53)						
	# ‘on whose right and left, lions were laying’						
	# (Cyl A 5:16; L; 22)						
	1	zi-da	zi.d-Ø-'a	be.right-NFIN-NOM	4	LOC	not: amod+LOC
	2	gabu2-na	gabu2=ane='a	left=his=LOC	1	appos	
	3	piriĝ	piriĝ=Ø	lion=ABS	4	ABS	
	4	ì-nú-nú-a	'i-b(i)-nú-nú-Ø-'a	VP-3N:on-lie-lie-3N.S/DO-NOM	0	acl	

Titles or functionaries can be referred to with (lexicalized) nominalizations, and then, an annotation like a nominal (nmod or appos) would be preferrable. Here, we follow the decision taken in morphology annotation.

If a lexicalized nominalization is segmented into multiple tokens in the transliteration, annotate its parts individually:

	# Jagersma, Chap. 6 (62)					
	# ‘freedom (lit.“returning to mother”)’					
	# (MVN 6:52 rev 8; L; 22) 					
	1	ama-ar-	ama=r(a)	mother=DAT	2	DAT
	2	gi4	gi4-Ø	turn-NFIN	0	acl	not: amod, because the chosen segmentation split off a syntactic argument
	
Note that this should not normally occur in CDLI data. If such instances are found, they should also be marked for subsequent checks of the transliteration/segmentation.

adjectives can be nominalized/head can be elided
	
	annotate like a noun

	# Jagersma, Chap. 10 (52)						
	# ‘children (“small ones”) of the scribes’						
	# (MVN 11:208 6; ?; 21)						
	1	di4-di4-la	di4.di4.l-Ø-'a	be.small:be.small-NFIN-NOM	0	root	nominalized adjective
	2	dub-sar-e-ne	dub.sar=enē=ak	scribe=PL=GEN	1	GEN	

	# Jagersma, Chap. 10 (54)					
	# ‘my sweet one’					
	# (PN) (TCS 1:58 1; L; 21)					
	1	du10-ga-ĝu10	du10.g-Ø-'a=ĝu	be.sweet-NFIN-NOM=my	0	root

	# Jagersma, Chap. 10 (55)					
	# ‘the sweet things of Irikagena’					
	# (Ukg. 41 1; L; 24)					
	1	du10-ga	du10.g-Ø-'a	be.sweet-NFIN-NOM	0	root
	2	iri-ka-ge-na-ka	iri.ka.ge.na.k=ak	Irikagena=GEN	1	GEN

TO BE DISCUSSED: abandon in favor of acl? (when working through Jagersma's glosses, confusing them seems to be a frequent source of errors)
		
	# Jagersma, Chap. 7 (74)					
	# ‘because of the couriers (lit.“the ones of running”)’					
	# (AUCT 2:122 3; D; 21)					
	1	mu	mu	name	0	TERM
	2	kas4-ke4-ne-šè	kas4-Ø=ak=enē=ak=še	run-NFIN=GEN=PL=GEN=TERM	1	amod+GEN

Occasionally, the arguments of a relative clause may occur as postposed genitive attributes of its syntactic head. Annotate according to their morphology, i.e., the relative clause as `amod`  (if no other arguments are given) and its arguments as adnominal `GEN`.

	# Jagersma, Chap. 7 (204b)						
	# ‘from Sagub to the border of the work done by Bau’s men: 80 nindan’						
	# (DP 636 2:3-3:1; L; 24)						
	1	saĝ-ub!-ta	saĝ.ub=ta	Sagub=ABL	9	ABL	
	2	/	_	_	1	punct	
	3	kíĝ	kíĝ	work	9	TERM	
	4	ak	ak-Ø	make-NFIN	3	amod	
	5	lú	lú	man	5	GEN	
	6	dba-ú-ka	ba.ú=ak=ak	Bau=GEN=GEN	5	GEN	
	7	zà-bé	zà.g=be=š(e)	border=its=TERM	3	appos	
	8	80	80	80	9	nummod	
	9	níĝ-řá	níĝ.řá	nindan	0	root	

preposed adjectives: "[A]n attributive adjective, as a rule, follows its head noun, [but] there are a few instances where an attributively used kù.g ‘pure, holy’ precedes it." (Jagersma 2010: p.273)

	# Jagersma, Chap. 10 (27)						
	# ‘The year: Enlil’s holy throne was fashioned.’						
	# Jagersma, Chap. 10 (e.g., AUCT 2:42 7; D; 21)						
	1	mu	mu	year	0	root	
	2	kù	kù.g	pure	3	amod	preposed adjective?
	3	gu-za	gu.za	throne	5	ABS	
	4	den-líl-lá	en.lil=ak=Ø	Enlil=GEN=ABS	3	GEN	
	5	ba-dím	Ø-ba-dím-Ø	VP-MM-create-3N.S/DO	1	ccomp	tbc

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

	# Jagersma, Chap. 8 (55)					
	# ‘of (the fact) that Huru established our freedom’					
	# (NG 169 10; L; 21)					
	1	hu-ru	hu.ru=e	Huru=ERG	3	ERG
	2	ama-ar-gi4-me	ama.ar.gi4=mē=Ø	freedom=our=ABS	3	ABS
	3	in-ĝar-ra	'i-n-ĝar-Ø-'a=ak	VP-3SG.A-place-3N.S/DO-NOM=GEN	0	acl+GEN

	# Jagersma, Chap. 10 (24)					
	# ‘five new ploughshares for deep-ploughing’					
	# (VS 14:67 2:1; L; 24).					
	1	5	5	5	2	nummod
	2	ĝišeme	eme	tongue	0	root
	3	tugurx	tugurx=Ø	plough=ABS	4	ABS
	4	si-ga	si.g-Ø-'a=ak	put.into-NFIN-NOM=GEN	2	acl+GEN
	5	gibil	gibil	new	2	amod

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

	# Jagersma, Chap. 7 (275)					
	# ‘since the very beginning of time (lit. “From the day when the bud came out, from when the seed sprouted”)’					
	# (St B 8:27-28; L; 22)					
	1	u4	u4.d	day	6	ABL
	2	ul-	ul=Ø	bud=ABS	3	ABS
	3	lí-a-ta	'è-Ø-'a=ta	go.out-NFIN-NOM=ABL	1	acl
	5	numun	numun=Ø	seed=ABS	6	ABS
	6	i-a-ta	'è-Ø-'a=ta	go.out-NFIN-NOM=ABL	0	acl+ABL

Note that these are not limited to adverbial (spatio-temporal) interpretations: 

	# Jagersma, Chap. 5 (25)					
	# ‘what Ningirsu has agreed with Irikagena’					
	# (locative) (Ukg.34 1; L; 24)					
	1	{d}nin-ĝír-sú-ke4	nin.ĝír.su.k=e	Ningirsu=ERG	3	ERG
	2	iri-ka-ge-na-da	iri.ka.ge.na.k=da	Irikagena=COM	3	COM
	3	e-da-du11-ga-a	'i-n-da-n-du11.g-Ø-'a='a	VP-3SG-with-3SG.A-say-3N.S/DO-NOM=LOC	0	acl+LOC
	
	# Jagersma, Chap. 6 (30)					
	# ‘the surveyors (lit. “man of pulling the rope”)’					
	# (Ukg. 4 4:2-6; L; 24)					
	1	lú	lú	man	0	root
	2	éš	éš=Ø	rope=ABS	3	ABS
	3	gíd	gíd-Ø=ak	pull-NFIN=GEN	1	acl+GEN

Note that a dependency label can aggregate more than two (case) labels

	# Jagersma, Chap. 7 (251)					
	# ‘because the lamentation priest was deprived of the field (lit. “went up from the field”)’					
	# (NG 215 47 U; 21)					
	1	gala	gala=Ø	lamentation.priest=ABS	3	ABS
	2	a-šà-ta	a.šà.g=ta	field=ABL	3	ABL
	3	e11-da-ke4-eš	e11.d-Ø-'a=ak=eš	go.up-NFIN-NOM=GEN=ADV	0	acl+GEN+ADV


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

	# Jagersma, Chap. 8 (17)					
	# ‘The things I know, he knows too.’					
	# (TrD 1 13; ?; 21)					
	1	níĝ	níĝ=Ø	thing=ABS	2	ABS
	2	ì-zu-a	'i-'-zu-Ø-'a=Ø	VP-1SG.A-know-3N.S/DO-NOM=ABS	4	acl+ABS
	3	a-ne	a.ne=e	he=ERG	4	ERG
	4	in-ga-an-zu	'i-nga-n-zu-Ø	VP-also-3SG.A-know-3N.S/DO	0	root

	# Jagersma, Chap. 8 (108)					
	# ‘I do not know what I shall do about it (lit. “I do not know its what shall I make”).’					
	# (VS 10:193 8; ?; 21)					
	1	a-na	a.na=Ø	what=ABS	2	ABS
	2	íb-ak-na-bé	'i-b-'ak-en-'a=be=Ø	VP-3N.DO-make-1SG.A/S:IPFV-NOM=its=ABS	3	acl+ABS
	3	nu-zu	nu='i-'-zu-Ø	NEG=VP-1SG.A-know-3N.S/DO	0	root
	
	# Jagersma, Chap. 8 (110)					
	# ‘Say to Lugalmu what Gube says: (...)!’					
	# (Nik 1:177 2:2-3:1; L; 24)					
	1	gú-bé	gú.be=e	Gube=ERG	4	ERG
	3	na-	a.na=Ø	what=ABS	4	ABS
	4	e-a	'a-b-'e-e-'a=Ø	VP-3N.OO-say:IPFV-3SG.A:IPFV-NOM=ABS	8	acl+ABS
	6	lugal-mu	lugal.mu=r(a)	Lugalmu=DAT	8	DAT
	8	du11-ga-na	du11.g-'a-nna-b	say-VP-3SG.IO-3N.DO	0	root

	# Jagersma, Chap. 24 (39)					
	# ‘Say to Ur-Lisina what the king says:’					
	# (TCS 1:1 1-4; U; 21)					
	1	lugal-e	lugal=e	king=ERG	4	ERG
	2	/	_	_	4	punct
	3	na-	(a.)na=Ø	what=ABS	4	ABS
	4	ab-bé-a	'a-b-'e-e-'a	VP-3N.OO-say:IPFV-3SG.A:IPFV-NOM	8	acl.ABS
	5	/	_	_	8	punct
	6	ur-dli9-si4-na-ra	ur.li9.si4.na.k=ra	Urlisina=DAT	8	DAT
	7	/	_	_	8	punct
	8	ù-na-a-du11	'u-nna-e-du11.g-Ø	REL.PAST-3SG.IO-2SG.A-say-3N.S/DO	0	advcl


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

Note that the implicit copula allows to treat *every word* to be head of a relative clause:

	# Jagersma, Chap. 8 (94)						
	# ‘the knowledge acquired by me, which is now this and that,’						
	# (Shulgi B 316; 21, OB copy)						
	1	ĝeštu2	ĝeštu2.g	wisdom	0	root	
	2	dab5-ba-ĝu10	dab5-Ø-'a=ĝu	take-NFIN-NOM=my	1	amod	
	3	ì-ne-šè	ì.ne.šè	now	4	LOC	?
	4	ne-e	nēn	this	1	acl	ABS => copular predicate => (implicit) relative clause
	5	ur5-ra-àm	ur5=Ø='am	that=ABS=be:3N.SG	4	appos	

Note: If a clause is ambiguous between an analysis as a (morphologically unmarked) relative clause or a declarative clause, annotate it as declarative clause.

Occasionally, the arguments of a relative clause may occur as postposed genitive attributes of its syntactic head. Annotate according to their morphology, i.e., the relative clause as `amod`  (if no other arguments are given) and its arguments as adnominal `GEN`.

	# Jagersma, Chap. 7 (204b)						
	# ‘from Sagub to the border of the work done by Bau’s men: 80 nindan’						
	# (DP 636 2:3-3:1; L; 24)						
	1	saĝ-ub!-ta	saĝ.ub=ta	Sagub=ABL	9	ABL	
	2	/	_	_	1	punct	
	3	kíĝ	kíĝ	work	9	TERM	
	4	ak	ak-Ø	make-NFIN	3	amod	
	5	lú	lú	man	5	GEN	
	6	dba-ú-ka	ba.ú=ak=ak	Bau=GEN=GEN	5	GEN	
	7	zà-bé	zà.g=be=š(e)	border=its=TERM	3	appos	
	8	80	80	80	9	nummod	
	9	níĝ-řá	níĝ.řá	nindan	0	root	

??? ccomp

	# Jagersma, Chap. 10 (27)						
	# ‘The year: Enlil’s holy throne was fashioned.’						
	# Jagersma, Chap. 10 (e.g., AUCT 2:42 7; D; 21)						
	1	mu	mu	year	0	root	
	2	kù	kù.g	pure	3	amod	preposed adjective?
	3	gu-za	gu.za	throne	5	ABS	
	4	den-líl-lá	en.lil=ak=Ø	Enlil=GEN=ABS	3	GEN	
	5	ba-dím	Ø-ba-dím-Ø	VP-MM-create-3N.S/DO	1	ccomp	tbc

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

implicit modification: genitive or equative
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

extends to other (implicit) cases: implicit modification

	# Jagersma, Chap. 10 (63)						
	# ‘19 full-grown oxen with both eyes healthy’						
	# (VS 14:66 2:1; L; 24).						
	1	20	20	20	4	nummod	
	2	lá	lá	minus	1	acl	
	3	1	1	1	2	nummod	
	4	gu4	gu4.ř	ox	0	root	
	5	gal-gal	gal-gal	big-big	4	amod	
	6	igi	igi	eye	4	appos	implicit modification
	7	silim	silim	intact	6	amod	

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

In rare cases, a phrase in a longer sequence of complex appositions may copy the case marker of its head although it does not mark the end of the phrase. According to Jagersma (2010:92), "if the head is followed by two or more appositions, the case marker is sometimes placed after every apposition and thus repeated several times. This happens chiefly when the number of appositions is particularly large. Take, for instance, the following example, which gives only the first two appositions out of a series of twelve, all of them with an ergative case marker:"

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

Occasionally, repeated case markers in an apposition could be a means of asserting non-identity, i.e., clarify that this is (implicit) conjunction rather than (implicit) identity. This is not made explicit on the syntactic annotation.

	# Jagersma, Chap. 7 (281)						
	# ‘by the power of the Nanshe and by the power of Ningirsu’						
	# (St D 4:2-3; L; 22)						
	1	á	á	arm	0	ABL	
	2	dnanše-ta	nanše=ak=ta	Nanshe=GEN=ABL	1	GEN	
	4	á	á	arm	1	appos	not ABL
	5	dnin-ĝír-su-ka-ta	nin.ĝír.su.k=ak=ta	Ningirsu=GEN=ABL	4	GEN	

In the following case, redundant case marking may just be a rhetoric device, as it underlines the parallelism between both appositions

	# Jagersma, Chap. 8 (88)					
	# ‘a young woman this beautiful, this splendid’					
	# (Enlil and Ninlil 38; OB)					
	1	lú-ki-sikil	lú.ki.sikil	young.woman	root	DAT
	2	ne-en	nēn	this	1	appos
	3	sa6-ga-ra	sa6.g-Ø-'a=ra	be.beautiful-NFIN-NOM=DAT	2	acl
	4	ne-en	nēn	this	1	appos
	5	mul-la-ra	mul-Ø-'a=ra	be.splendid-NFIN-NOM=DAT	4	acl

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

For units, the quantified commodity is to be annotated as syntactic head, unless the morphological annotation points to a genitive construction, as in the following example.

	# Jagersma, Chap. 7 (295)					
	# ‘each (person) with four rings of (lit. “with”) eight shekels of silver each’					
	# (AUCT 1:942 5; D; 21)					
	1	2	2	2	2	nummod
	2	har	har	ring	0	ABL
	3	kù-babbar	kù.babbar=ak	silver=GEN	2	GEN
	4	8	8	8	5	nummod
	5	giĝ4-ta-ta	giĝ4=ta=ta	shekel=ABL=ABL	2	ABL

Without the `GEN` marker, two interpretations are possible: Either the commodity are actual rings, with the modifier making the material explicit, or the commodity is silver, distributed in the form of rings. From the archeological context, we adopt the first interpretation, because silver as a commodity is normally described in units of weight, and this is made explicit in the morphological annotation by restoring a `=GEN` morpheme. Even if such a restored (or overt) morpheme is absent, the annotation as unit must only be applied if the element modified is not a proper name (but see epithets below) and if the unit is listed in the documentation of metrological units, cf. ([CDLI wiki](http://cdli.ox.ac.uk/wiki/doku.php?id=ur_iii_metrological_systems)).

Numeral modifiers adjacent to the unit are annotated as dependents of the unit, not the commodity. If the commodity stands *between* numeral and unit, numerals modify the commodity.

* if numerals appear adjacent to units, annotate the unit as head, not the commodity

	# Jagersma, Chap. 9 (43)					
	# ‘with five shekels of silver (for each sheep)’					
	# (JCS 26 p.11 3:1; L; 24)					
	1	kù	kù.g	silver	0	ABL
	2	5	ja	five	3	nummod
	3	giĝ4-ta	giĝ4=ta	shekel=ABL	1	appos

* if numerals and units are separated by the commodity, annotate both as modifiers of the commodity
	
	# Jagersma, Chap. 9 (44)					
	# ‘ten shekels of silver’					
	# (BIN 8:352 2:5; L; 25)					
	1	10	u	ten	2	nummod
	2	kù	kù.g	silver	0	root
	3	giĝ4	giĝ4	shekel	2	appos

`nmod` is also used for epithets and titles:

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

	# Jagersma, Chap. 7 (205b)						
	# ‘This (barley) was taken to the field Planted Emblem.’						
	# (DP 537 3:2-3; L; 24)						
	1	ašag	ašag	field	2	nmod	epithet
	2	uri3	uri3	emblem	5	TERM	
	3	řú-a	řú-Ø-'a=š(e)	erect-NFIN-NOM=TERM	2	amod	
	5	ba-ře6	Ø-ba-ře6-Ø	VP-MM-bring-3N.S/DO	0	root	

epithets can also be relational verbs, e.g., family terms

	# Jagersma, Chap. 25 (129)					
	#	‘He surely was my brother Ningirsu!’  				
	# (Cyl A 5:17; L; 22)					
	1	ses-ĝu10	ses=ĝu	brother=my	2	nmod
	2	{d}nin-ĝír-su	nin.ĝír.su.k=Ø	Ningirsu=ABS	3	ABS
	3	ga-nam-me-àm	ga-na-me-Ø='am	MOD-PFM-be-3SG.S=be:3SG.S	0	root

epithets can also be metaphorical rather than lexicalized

	# Jagersma, Chap. 26 (6)						
	# ‘You carry charm for the Great Mountain Enlil.’						
	#	(BE 31:04:00 01:06 (Shulgi H); N; 21, OB copy)					
	1	kur	kur	mountain	3	nmod	epithet!
	2	gal	gal	big	1	amod	
	3	{d}en-líl-ra	en.líl=ra	Enlil=DAT	5	DAT	
	4	ul	ul=Ø	charm=ABS	5	ABS	
	5	ša-mu-na-gùr-ù	ši-mu-nna-gùr-e	PFM-VENT-3SG.IO-carry-3SG.A:IPFV	0	root	

epithets share certain characteristics with determiners

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

The epithet rule does not apply to proper names in dependent clauses:

	# Jagersma, Chap. 6 (1)						
	# ‘one female slave, Šarrūa is her name, “its” price...’						
	# (FAOS 17:10 1-2; N; 21)						
	1	1	1	1	2	nummod	
	2	saĝ-mí	saĝ.mí	slave.woman	6	root
	3	sar-ru-a	sar.ru.a=Ø	Šarrūa=ABS	4	ABS	
	4	mu-né-em	mu=ane=Ø=('a)m	name=her=ABS=be:3SG.S	2	acl	

Likewise, the epithet rule does not apply to year names, as these are clausal:

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

	To be confirmed whether certain quantifiers should be annotated like determiners. Syntactically and morphologically, they behave like nominal appositions.
		
	# Jagersma, Chap. 8 (124)					
	# ‘I want to hold a rented field anywhere!’					
	# (MVN 11:168 17; U; 21)					
	1	ki	ki	place	4	LOC
	2	na-me-a	na.me='a	any=LOC	1	appos
	3	apin-lá	apin.lá=Ø	rented.field=ABS	4	ABS
	4	ga-ba-ab-dab5	ga-ba-b-dab5	MOD:1SG.A/S-MM-3N.DO-seize	0	root

Note: In the Jagersma reference data, these are currently annotated as `appos`. Check whether this is done systematically in data and throughout here.

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

If multiple conjuncts with an explicit conjunction are marked redundantly for the same case, annotate the first only, use `conj` for the others:

	# Jagersma, Chap. 7 (125)					
	# ‘that they will not say it to the king or to the administrator’					
	# (NRVN 1:180 12; N; 21)					
	1	lugal-ra	lugal=ra	king=DAT	0	DAT
	2	ù	ù	or	1	cc
	3	saĝĝa	saĝĝa=r(a)	administrator=DAT	1	conj
	4	nu-na-bé-ne-a	nu='i-nna-b-'e-enē-'a	NEG=VP-3SG.IO-3N.OO-say:IPFV-3PL.A:IPFV-NOM	1	acl
	
(In our understanding of the grammar, such replicated case markers are not necessary, if not ungrammatical, but they may occur due to scribal errors or to enforce the case for long series of conjunctions -- and, similarly, appositions.)

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

Note that absolutives in vocative use are annotated as `vocative` (not `ABS`) in both CDLI and UD

Note that a compound verb may seem to have core arguments multiple times, e.g., if an original `ABS` argument is lexicalized into a part of the verbal meaning. If such relations are transparent, they are also annoted as such:

	# Jagersma, Chap. 6 (41)						
	# ‘after Ursisi, the barber, had raised AN.LUH’s sons for three years’						
	# (BIN 8:293 3:2-5; N; 23)						
	1	mu	mu	year	10	ABL	cop on 2 ignored as emphatic article (is that right?)
	2	3-àm	3='am	3=be:3N.S	1	nummod	
	3	dumu	dumu	son	10	ABS	marked on 4
	4	AN.LUH	AN.LUH=ak=Ø	AN.LUH=GEN=ABS	3	GEN	
	6	ur-si4-si4	ur.si4.si4	Ursisi	10	ERG	
	7	šu-i	šu.i=e	barber=ERG	6	appos	
	9	á	á=Ø	strength=ABS	10	ABS	
	10	ì-è-éš-a-ta	'i-n-'è-eš-'a=ta	VP-3SG.A-go.out-3PL.S/DO-NOM=ABL	0	acl+ABL	

In UD, only the outer `ABS` argument (*dumu AN.LU*) should be annotated as `obj`, the inner (*á*) as `mwe`.

#### Datives

In morphology, labels are `DAT-H` and `DAT-NH`. Suggestion: Simplify as `DAT` (to better align with annotation projection)

> Taglist originally said to map `DAT-H` to `iobj`, only.
 
Terminative-locatives (if annotated as such) in dative function are treated as oblique arguments, not as datives.

#### Oblique arguments: LOC, TERM, ABL, DIR

In CDLI annotation, use morphological case as labels. In UD export, map to `obl`. For better alignment with annotation projection, use `LOC` in place of `L1`, `L2-NH` and `L3-NH`, etc.

TODO: Check treatment in pre-annotation.

Normally, these obliques can be mapped to semantic roles. Occasionally, however, two semantic roles may be encoded by the same morphological case, then, the relative order of oblique arguments seems to determine their semantic interpretation, cf. TERM [AMOUNT] and TERM [GOAL] in the following example:

	# Jagersma, Chap. 13 (23)					
	# ‘4 labourers for 10 days: they brought straw from KI.AN to Umma.’					
	# (TENS 205 1-3; U; 21)					
	1	4	4	4	2	nummod
	2	ĝuruš	ĝuruš	labourer	0	root
	3	u4	u4.d	day	10	TERM
	4	10-šè	10=še	10=TERM	3	nummod
	6	KI.ANki-ta	KI.AN=ta	KI.AN=ABL	10	ABL
	7	ummaki-<šè>	umma=še	Umma=TERM	10	TERM
	9	in-u	in.u=Ø	straw=ABS	10	ABS
	10	ì-im-ře6	'i-m(u)-ře6-Ø	VP-VENT-bring-3N.S/DO	2	parataxis

Aside from marking semantic roles, oblique cases could also be used to express a pragmatic function. In Old Sumerian, the `DIR`, modifying a relative, could also used as a topic marker. Annotate according to the morphology, not the pragmatics. (Should not occur in Ur III data.)

	# Jagersma, Chap. 7 (160)						
	# ‘As for your punting-poles, you are a dragon, sleeping a sweet sleep in its den.’						
	# (Shulgi R 13; N; 21, OB copy)						
	1	ge-m[u]š?-zu-ù	ge.muš=zu=e	punting.pole=your=DIR	2	DIR	
	2	ušumgal	ušumgal	dragon	0	root	ABS (marked on 6) => copular predicate
	3	ki-nú-bé-a	ki.nú=be='a	lying.place=its=LOC	6	LOC	
	4	ù	ù	sleep	6	ABS	
	5	du10	du10.g=Ø	sweet=ABS	4	amod	
	6	ku4-me-èn	ku4-Ø=Ø=me-en	sleep-NFIN=ABS=be-2SG.S	2	acl	


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

	# Jagersma, Chap. 28 (111)					
	# ‘Atu was proven to have given the boat (lit. “Atu was made firm as one who gave the boat”).’					
	#	(NG 62 11; U; 21). Note that a-tu is the subject of ba-ge-en6 and not of šúm-ma  				
	1	a-tu	a.tu=Ø	Atu=ABS	4	ABS
	2	má	má=Ø	boat=ABS	3	ABS
	3	šúm-ma-aš	šúm-Ø-'a=še	give-NFIN-NOM=TERM	1	acl+TERM
	4	ba-ge-en6	Ø-ba-ge.n-Ø	VP-MM-be.firm-3SG.S/DO	0	root

While these may be undebatable examples, there can also be ambiguity as to whether ablatives, terminatives, etc. are adnominal or clausal arguments (the following analyses according to Jagersma):

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

If no overt verb is given but an annotation of an adnominal modification is possible, annotate it as such.

	# Jagersma, Chap. 7 (142)						
	# ‘From the house next to the one of Mesandu’						
	# (DP 173 5:5; L; 24)						
	1	é	é	house	0	DIR	
	2	dmes-an-du-ke4	mes.an.du=ak=e	Mesandu=GEN=DIR	1	GEN	
	3	ús-sa-ta	ús-Ø-'a=ta	be.next.to-NFIN-NOM=ABL	1	ABL	not acl+ABL, as this is an amod

Occasionally, the arguments of a relative clause may occur as postposed genitive attributes of its syntactic head. Annotate according to their morphology, i.e., the relative clause as `amod`  (if no other arguments are given) and its arguments as adnominal `GEN`.

	# Jagersma, Chap. 7 (204b)						
	# ‘from Sagub to the border of the work done by Bau’s men: 80 nindan’						
	# (DP 636 2:3-3:1; L; 24)						
	1	saĝ-ub!-ta	saĝ.ub=ta	Sagub=ABL	9	ABL	
	2	/	_	_	1	punct	
	3	kíĝ	kíĝ	work	9	TERM	
	4	ak	ak-Ø	make-NFIN	3	amod	
	5	lú	lú	man	5	GEN	
	6	dba-ú-ka	ba.ú=ak=ak	Bau=GEN=GEN	5	GEN	
	7	zà-bé	zà.g=be=š(e)	border=its=TERM	3	appos	
	8	80	80	80	9	nummod	
	9	níĝ-řá	níĝ.řá	nindan	0	root	

#### Other adnominal dependenty

adnominal LOC

Jagersma (2010:178) "Adnominal use [of the locative -- CC] occurs in distributive expressions. ... Note, however, that what looks like adnominal use in a distributive expression may actually be adverbial use with ellipsis of the verb" 
							
	# Jagersma, Chap. 7 (195)						
	# ‘with two ban of barley in a month for one pig’						
	# (VS 14:9 9:3-4; L; 24)						
	1	šáh	šáh	pig	5	TERM	
	2	1-šè	1=še	1=TERM	1	nummod	
	3	/	_	_	1	punct	
	4	iti-da	iti.d='a	month=LOC	1	LOC	
	5	še	še	barley	0	root	morphologically ABL
	6	0.0.2-ta	0.0.2=ta	2.ban=ABL	5	nummod	

	# Jagersma, Chap. 7 (261)					
	# ‘with two ... in each of its bales’					
	# (Nik 2:111 2; U; 21)					
	1	gu-niĝin2-ba	gu.niĝin2=be='a	bale=its=LOC	3	LOC
	2	2	2	2	3	nummod
	3	LAGAB-ta-a	LAGAB=ta	?=ABL	0	ABL

	# Jagersma, Chap. 7 (196)						
	# ‘with nine bundles in a bale’						
	# (Zinbun 18 p. 101 6 BM 16163 1; L; 21)						
	1	gu-niĝin2-na	gu.niĝin2='a	bale=LOC	5	LOC	
	2	10	9	9	1	nummod	
	3	lá	_	_	2	acl	
	4	1	_	_	3	nummod	
	5	sa-ta	sa=ta	bundle=ABL	0	root	morphologically ABL

for the latter, cf.
	
	# Jagersma, Chap. 7 (197)						
	# ‘They (= bundles) were placed in a bale with twenty bundles each.’						
	# (AAICAB I/4 pl.269 Bod. S 425 4; D; 21)						
	1	gu-niĝin2-na	gu.niĝin2='a	bale=LOC	4	LOC	
	2	10	10	10	3	nummod	
	3	sa-ta	sa=ta	bundle=ABL	4	ABL	
	4	ba-an-ĝar	Ø-ba-n(i)-ĝar-Ø	VP-MM-in-place-3N.S/DO	0	root	

Note that the rule in eliptic transactions is to mark the commodity as head. Both the adnominal and the adverbial-elliptic interpretation of the locatives are consistent with this annotation.
		
cf. adnominal ABL

	# Jagersma, Chap. 7 (268)					
	# ‘They are men from Susa.’					
	# (RTC 350 8; L; 21)					
	1	lú	lú	man	0	root
	2	susinki-ta-me	susin=ta=Ø=me-eš	Susa=ABL=ABS=be-3PL.S	1	ABL

	# Jagersma, Chap. 7 (204a)						
	# ‘from the wall of the Medib-field to the middle imnun: 50 nindan’						
	# (DP 641 3:4-5; L; 24)						
	1	bàd	bàd	wall	8	ABL	
	2	ašag	ašag	field	3	nmod	
	3	me-dib-ta	me.dib=ak=ta	Medib=GEN=ABL	1	GEN	
	4	/	_	_	8	punct	
	5	im-nun	im.nun	imnun	8	TERM	
	6	mu5-ru5-šè	mu5.ru5b=ak=še	middle=GEN=TERM	5	GEN	
	7	80	50	50	8	nummod	
	8	níĝ-řá	níĝ.řá	nindan	0	root	

adnominal ABL

	"[T]he noun phrase in the ablative case can also be used adnominally and thus be a part of a larger noun phrase" (Jagersma 2010: 195)
	
	# Jagersma, Chap. 7 (269)					
	# ‘sealed documents (lit. “impressed seals”) and letters from Anshan’					
	# (BIN 9:302 2-3; I; 20)					
	1	kišib	kišib	seal	0	ABS
	2	ra-a	ra-Ø-'a	hit-NFIN-NOM	1	amod
	3	ù-na-a-du11	ù-na.a-du11.g	letter	1	appos
	5	an-ša-anki-ta	an.ša.an=ta=Ø	Anshan=ABL=ABS	3	ABL

	# Jagersma, Chap. 7 (279)					
	# ‘twenty pounds of wool (weighed) with the weight for the wool distribution’					
	# (VS 25:54 1:1; L; 24)					
	1	20	20	20	2	nummod
	2	ma-na	ma.na	pound	3	nmod
	3	siki	siki	wool	0	root
	4	na4	na4	stone	3	ABL
	5	siki-ba-ta	siki.ba=ak=ta	wool.distribution=GEN=ABL	4	GEN

	# Jagersma, Chap. 7 (280)					
	# ‘16 1/2 iku of land (measured) with the rope of purchase’					
	# (BM 3:10 1:1; L; 24)					
	1	0.2.4	0.2.4	16	3	nummod
	2	1/2	1/2	1/2	1	nummod
	3	gana2	gana2	land	0	root
	4	éš	éš	rope	3	ABL
	5	sám-ma-ta	sám.ma=ak=ta	purchase=GEN=ABL	4	GEN
	
	"The ablative case can also have a distributive meaning, usually in combination with a noun phrase in the terminative, locative, or ergative case" (Jagersma 2010: 195)
	
	# Jagersma, Chap. 7 (287)						
	# ‘Dudu the temple administrator and his wife and children consumed this in the house of Kisal.’						
	# (DP 224 6:5-9; L; 24)						
	1	du-du	du.du	Dudu	11	ERG	marked on 6
	3	saĝĝa	saĝĝa	administrator	1	appos	
	5	dam	dam	wife	3	ABL	adnominal ABL
	6	dumu-né-ta	dumu=ane=ta=e	child=his=ABL=ERG	5	appos	implicit conjunction
	8	é	é	house	11	LOC	
	9	ki-sal4-la-ka	ki.sal4=ak='a	Kisal=GEN=LOC	8	GEN	
	11	ì-gu7-ne	'i-gu7-enē	VP-eat-3PL.A:IPFV	0	root	

if the transaction rule does not apply, annotate like a sentence with an implicit copula, i.e., with the last argument as head

	# Jagersma, Chap. 7 (244)					
	# ‘with two ban of barley in a month for one pig’					
	# (Nik 1:63 10:1-2; L; 24)					
	1	šáh	šáh	pig	0	TERM
	2	1-šè	1=še	1=TERM	1	nummod
	4	iti-da	iti.d='a	month=LOC	1	LOC
	5	še	še	barley	1	ABL
	6	0.0.2-ta	0.0.2=ta	0.0.2=ABL	5	nummod

cf. adnominal `TERM`

	# Jagersma, Chap. 7 (216)					
	# ‘royal consignment (lit. “things that left the hand”) to Dilmun’					
	# (BIN 9:391 21-22; I; 20)					
	1	níĝ	níĝ	thing	0	root
	2	šu	šu=Ø	hand=ABS	3	ABS
	3	taka4-a	taka4-Ø-'a	leave-NFIN-NOM	1	acl
	4	lugal	lugal=ak	king=GEN	1	GEN
	5	dilmunki-šè	dilmun=še	Dilmun=TERM	1	TERM

	# Jagersma, Chap. 7 (222)					
	# ‘four labourers for 24 days’					
	# (UTAMI 3:1605 1; U; 21)					
	1	4	4	4	2	nummod
	2	ĝuruš	ĝuruš	young.man	0	root
	3	u4	u4.d	day	2	TERM
	4	24-šè	24=še	24=TERM	3	nummod
	
	# Jagersma, Chap. 7 (225)					
	# ‘from the month Shulgi’s Festival until (and including) the month Shuesha’					
	# (UET 3:988 6-7; Ur; 21)					
	1	iti	iti.d	month	0	ABL
	2	ezem	ezem	festival	1	appos
	3	dšul-ge-ta	šul.ge.r=ak=ta	Shulgi=GEN=ABL	2	GEN
	5	iti	iti.d	month	1	TERM
	6	šu-eš5-ša-šè	šu.eš5.ša=še	Shuesha=TERM	5	appos

	# Jagersma, Chap. 7 (234)					
	# ‘200 litres of emmer wheat (to be used) as seed’					
	# (NATN 647 1-2; N; 21)					
	1	0.3.2	0.3.2	200.litres	2	nummod
	2	zíz	zíz	emmer.wheat	0	root
	4	numun-šè	numun=še	seed=TERM	2	TERM

again, these may be elliptic:

	# Jagersma, Chap. 7 (245)					
	# ‘six men: with five reeds of work for one man’					
	# (DP 622 1:1-3; L; 24)					
	1	6	6	6	2	nummod
	2	lú	lú	man	0	root
	4	lú	lú	man	7	TERM
	5	1-šè	1=še	1=TERM	4	nummod
	7	kíĝ	kíĝ	work	2	ABL
	8	ge	ge	reed	7	appos
	9	5-ta	5=ta	5=ABL	8	nummod

	# Jagersma, Chap. 7 (246)					
	# ‘12 ½ men: To one man with three cubits of work each, it has been assigned.’					
	# (TSA 23 3:5-8; L; 24)					
	1	12	12	12	3	nummod
	2	½	½	½	1	nummod
	3	lú	lú	man	0	root
	5	lú	lú	man	12	TERM
	6	1-šè	1=še	1=TERM	5	nummod
	8	kíĝ	kíĝ	work	12	ABL
	9	kùš	kùš	cubit	8	appos
	10	3-ta	3=ta	3=ABL	9	nummod
	12	ì-ši-ti	'i-n-ši-te-Ø	VP-3SG-to-approach-3N.S/DO	3	parataxis


#### "Functional obliques"

Agents in a transaction without morphological marks for their grammatical structure.

	PN.GEN/ N.GEN (giri/ kiszib of a person or occupation)
	giri PN occupation N 
	kiszib PN = obl to verb

In UD export, annotated as `obl`. CDLI labels should be human-readable English short-hands, guided by common translations, e.g., `via` for *giri3*. TODO: Check annotation projection and current treatment in pre-annotation.

	# Jagersma, Chap. 7 (72)					
	# ‘via his son Abbasaga’					
	# (AUCT 1:388 5; D; 21)					
	1	ĝiri3	ĝiri3	foot	0	root
	2	ab-ba-sa6-ga	ab.ba.sa6.ga	Abbasaga	1	GEN
	3	dumu-na	dumu=ane=ak	child=his=GEN	2	appos


List all examples here.

QUESTION: Does that include *a-gù* "on (the account of)"?

	# Jagersma, Chap. 7 (9)						
	# ‘on the administrator of the god An’						
	# (CM 26:142 4; D; 21)						
	1	a-gù	a.gù	top	0	LOC	
	2	šabra	šabra	administrator	1	appos	GEN?
	3	an-na-ka	an=ak='a	An=GEN=LOC	2	GEN	

	# Jagersma, Chap. 15 (28)			
	# ‘He should not place it on his account, but he should place 14.4.0 gur on his account.’			
	# (AuOr 17/18 p. 219:5 6-10; L; 21)			
	1	a-gù-a-na	a.gù=ane='a	top=his=LOC
	3	na-bí-ĝá-ĝá	nan-bi-b-ĝar:RDP-e	NEG.MOD-3N:on-3N.DO-place:IPFV-3SG.A:IPFV
	5	14.04.2000	14.04.2000	14.04.2000
	6	gur	gur=Ø	gur=ABS
	8	a-gù-a-na	a.gù=ane='a	top=his=LOC
	10	ha-ab-ĝá-ĝá	ha=Ø-b(i)-ĝar:RDP-e	MOD=VP-3N:on-place:IPFV-3SG.A:IPFV

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

	# Jagersma, Chap. 7 (76)					
	# ‘when Geme-tarsirsira was chosen by extispicy (lit.“was found by a young he-goat”) in the one of (the god) Mesandu’					
	# (Nik1:1744:1-3; L;24)					
	1	[geme2]-tar-[sír]-sír-ra	PN=Ø	PN=ABS	6	ABS
	3	dmes-an-du-ka	mes.an.du=ak='a	Mesandu=GEN=LOC	6	GEN+LOC
	5	maš-e	maš=e	kid=ERG	6	ERG
	6	pà-da-a	pà.d-Ø-'a='a	find-NFIN-NOM=LOC	0	acl+LOC

	# Jagersma, Chap. 8 (33)					
	# ‘because of your captive wife’					
	# (Inanna B 141; OB copy)					
	1	dam	dam	wife	0	GEN+ADV
	2	dab5-ba-za-ke4-eš	dab5-Ø-'a=zu=ak=eš	take-NFIN-NOM=your=GEN=ADV	1	amod

#### Genitive case: GEN

Along with equative, the genitive is an adnominal case (not resumed by any dimensional prefix) indicating possession, origin or affiliation.
In the mapping to UD, represented as `nmod`.

The anticipatory genitive (`GEN+disloc`, see `disloc`) involves a dislocation. As this can be iterated (anticipatory genitive of an anticipatory genitive), we annotate the head in an opportunistic fashion: Where this is adjacent to the semantic head, annotate the semantic head, where it is detached, annotate the head of the clause as head. In UD, the first use should be `nmod`, the second should be `disloc`.

According to Jagersma (2010, p. 152), "[a] noun phrase in the genitive case can also be used as a constituent of a clause. It is then not syntactically dependent on a noun or another noun phrase. Such a noun phrase in the genitive case will be called a headless genitive. A headless genitive expresses the same meanings as English ‘the one(s) of ...’, ‘that of ...’, and the like":

	# Jagersma, Chap. 7 (77)					
	# ‘when in the new house the leather workers turned in that of the chariot’					
	# (Nik 1:93 3:3-6; L; 24)					
	1	ašgab-bé-ne	ašgab=enē=e	leather.worker=PL=ERG	9	ERG
	3	é	é	house	9	LOC
	4	gibil-a	gibil='a	new=LOC	3	amod
	6	{ĝiš}gigir2-ra	gigir2=ak	chariot=GEN	9	GEN+ABS
	8	šu-a	šu='a	hand=LOC	9	LOC
	9	bí-gi4-a	Ø-bi-b-gi4-'a='a	VP-3N:on-3N.A-turn-NOM=LOC	0	acl+LOC

Postposed genitives that represent the `ERG` arguments of a relative clause should be annotated as genitive dependents of the matrix noun, not the relative clause. If, by, consequence, no overt arguments of the `acl` remain, annotate it as `amod`.

	# Jagersma, Chap. 7 (156)					
	# ‘shepherd (ergative) chosen in his pure heart by Ningirsu (lit. “the by the heart found one of Ningirsu”)’					
	# (St B 2:8-9; L; 22)					
	1	sipa	sipa	shepherd	0	ERG
	2	šà-ge	šà.g=e	heart=DIR	3	DIR
	3	pà-da	pà.d-Ø-'a	find-NFIN-NOM	2	acl
	5	dnin-ĝír-su-ka-ke4	nin.ĝír.su.k=ak=e	Ningirsu=GEN=ERG	1	GEN


#### Equative case: EQU

Along with genitive, the equative (equitative) case, marked by *gin7*, is an adnominal case and not resumed by any dimensional prefix. It can be used to create nominal sentences. 

~~~ conllu
1	a-ba	_	who	_	_		root	_	_
2	szesz-gu10-gin7	_	like.my.brother	_	_	1	EQU	_	_

~~~
"Who is like my brother?" (Hayes, p.312, TCS 1,200)

	# Jagersma, Chap. 7 (327)						
	# ‘Who is like my brother?’						
	# (TCS 1:143 8; L; 21)						
	1	a-ba	a.ba=Ø	who=ABS	0	root	
	2	ses-ĝu10-gé	ses=ĝu=gen	brother=my=EQU	1	EQU	

"The equative case primarily expresses a relation of comparison between two noun phrases. Thus, like the genitive case (...), it does not indicate a semantic relation with the verb. This is undoubtedly the reason why finite verbal forms never contain an affix which is coreferential with a noun phrase in the equative or genitive case. All other cases designate some semantic relation with the verb and have their counterparts in some verbal affix." (Jagersma 2010: 203) Jagersma, chap. 7 mentions to exceptions to this rule.

However, note that an annotation as adnominal is not always possible in a projective parse. The following ("correct") analysis is non-projective (crossing edges). 

	# Jagersma, Chap. 7 (328)					
	# ‘Like the Anzu-bird, Ningirsu spreads out his wings over Irikagena.’					
	# (Ukg. 40 1; L; 24)					
	1	dnin-ĝír-su-ke4	nin.ĝír.su.k=e	Ningirsu=ERG	5	ERG
	2	iri-ka-ge-na-ra	iri.ka.ge.na.k=ra	Irikagena=DAT	5	DAT
	3	anzu{mušen}-gen	anzu2.d=gen	Anzu.bird=EQU	1	EQU
	4	á	á=Ø	arm=ABS	5	ABS
	5	mu-né-bař-ře	Ø-mu-nni-b-bař4-e	VP-VENT-3SG.OO-3N.DO-open-3SG.A:IPFV	0	root

It is not clear how to analyze this. In particular, the `ERG` case is not extended to the `EQU`. Similar to the annotation of dislocated genitives, mark the verb as head. This is feasible, however, only, if otherwise a non-projective parse (with crossing edges) would emerge.

Otherwise, `EQU` should always be annotated in relation to a noun. TODO: check in data and examples in documentation.

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

Note that the EQU (if analyzed as adnominal) deviates from all other morphological cases in that "the case marker of the compared phrase is not copied on the phrase in the equative case. For instance, in example (332) the noun é ‘house’, which is in the ergative case, is compared with the noun h~u~ r-sag ‘mountain’. Yet, the latter noun is only in the equative case, not also in the ergative case. This is normal in Sumerian, in contrast with some other languages." (Jagersma 2010: 204)

	# Jagersma, Chap. 7 (332)						
	# ‘The house lifted the head upwards in heaven and earth like a mountain.’						
	# (Cyl A 21:23; L; 22)						
	1	é-e	é=e	house=ERG	7	ERG	
	2	hur-saĝ-gen7	hur.saĝ=gen	mountain=EQU	1	EQU
	3	an	an	heaven	7	LOC	
	4	ki-a	ki='a	earth=LOC	3	appos	
	5	saĝ	saĝ=Ø	head=ABS	7	ABS	
	6	an-šè	an=še	heaven=TERM	7	TERM	
	7	mi-ni-íb-íl	Ø-mu-ni-b-'íl-Ø	VP-VENT-in-3N.A-lift-3N.S/DO	0	root	

TODO: please confirm priority of adnominal analysis for `EQU`.

	# Jagersma, Chap. 7 (333)						
	# ‘Let him seek shelter (lit. “bring his life”) in there as in his built-up city! (lit. “in there like his built city”).’						
	# (Shulgi A 35; OB manuscript)						
	1	iri	iri	city	4	EQU	isn't that actually EQU+LOC?
	2	řú-a-né-gen7	řú-Ø-'a=ane=gen	erect-NFIN-NOM=his=EQU	1	amod	
	3	zi-né	zi=ane=Ø	breath=his=ABS	4	ABS	
	4	ha-ba-ši-in-tùm	ha=Ø-ba-ši-n-tùm-Ø	MOD=VP-MM-to-3SG.A-bring:IPFV-3N.S/DO	0	root	

	
Headless EQU

	# Jagersma, Chap. 7 (331)						
	# ‘He had it (viz. a wall) surround his city like a green mountain.’						
	# (FAOS 9/2 Ibbīsuen 1-2 2:2-3; Ur; 21)						
	1	hur-saĝ	hur.saĝ	mountain	5	EQU	adnominal argument of (pro-dropped) subject
	2	sig7-ga-gen7	sig7-Ø-'a=gen	be.green-NFIN-NOM=EQU	1	acl	
	4	iriki-né	iri=ane=e	city=his=DIR	5	DIR	
	5	im-mi-dab6	'i-m(u)-bi-n-dab6-Ø	VP-VENT-3N.OO-3SG.A-surround-3N.S/DO	0	root	

TODO: Please confirm that `EQU` can be premodifying

	# Jagersma, Chap. 7 (334)					
	# ‘Who is as good as Bau?’					
	# (a personal name) (DP 112 5:6; L; 24)					
	1	dba-ú-gen7-	ba.ú=gen	Bau=EQU	1	EQU
	2	a-ba-	a.ba=Ø	who=ABS	3	ABS
	3	sa6	'a-sa6.g-Ø	VP-be.good-3SG.S/DO	0	root

TO CONFIRM: If adnominal, what does the EQU modify in the following example?

	# Jagersma, Chap. 7 (335)						
	# ‘as for the man who was as huge as heaven, as huge as the earth’						
	# (Cyl A 5:13; L; 22)						
	1	lú	lú	man	0	TERM	
	2	an-gen7	an=gen	heaven=EQU	3	EQU	adnominal?
	3	ri-ba	ri.b-Ø-'a	be.huge-NFIN-NOM	1	acl	
	4	ki-gen7	ki=gen	earth=EQU	5	EQU	adnominal?
	5	ri-ba-šè	ri.b-Ø-'a=še	be.huge-NFIN-NOM=TERM	1	acl	
	
Remark CC: Personally, I see little justification to insist on an *exclusively* adnominal interpretation of `EQU`. It is quite different from a classical adnominal case like `GEN` in terms of morphological (no case stacking) and syntactic (premodifying!?) features. However, Jagersma is quite explicit on that.


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

	# Jagersma, Chap. 7 (117)					
	# ‘Ningirsu, I am going to build your house for you.’					
	# (Cyl A 8:18; L; 22)					
	1	dnin-ĝír-su	nin.ĝír.su.k=Ø	Ningirsu=ABS	3	voc
	2	é-zu	é=zu=Ø	house=your=ABS	3	ABS
	3	ma-ra-řú-e	Ø-mu-ra-řú'-en	VP-VENT-2SG.IO-erect-1SG.A/S:IPFV	0	root

	# Jagersma, Chap. 8 (9)					
	# ‘My shepherd, I will explain your dreams for you.’					
	# (Cyl A 5:12; L; 22)					
	1	sipa-ĝu10	sipa.d=ĝu=Ø	shepherd=my=ABS	4	vocative
	2	ma-mu-zu	ma.mu.d=zu=Ø	dream=your=ABS	4	ABS
	3	ĝe26	ĝe26=e	I=ERG	4	ERG
	4	ga-mu-ra-búr-búr	ga-mu-ra-búr-búr	MOD:1SG.A/S-VENT-2SG.IO-reveal-reveal	0	root

	# Jagersma, Chap. 8 (70)					
	# ‘Slave! Is that man your master?’					
	# (GA 69; OB)					
	1	urdu2	urdu2.d	slave	3	voc
	2	lú-še	lú=še=Ø	man=that=ABS	3	ABS
	3	lugal-zu-ù	lugal=zu	master=your	0	root


TODO: standardize vocative/voc

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

Discussion: depending on context, vocatives can also be annotated as parataxis, if a clausal interpretation of the preposed nominal is likely. This includes all cases of (physical) deixis and cases where ellipsis can be demonstrated on grounds of parallel examples. 

Question: Require an explicit (or, restored in morphological annotation) 2nd person reference for using vocative?

TODO: make consistent throughout this document.

TODO: what's default here?



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

annotate semantic head if adjacent
	
	# Jagersma, Chap. 10 (76)					
	# ‘Someone would carry off the best of those sheep.’					
	# (Ukg. 6 1:3'-4'; L; 24)					
	1	udu-ba	udu=be=ak	sheep=this=GEN	2	GEN+disloc
	2	udu	udu	sheep	6	ABS
	3	sa6-ga-bé	sa6.g-Ø-'a=be=Ø	be.good-NFIN-NOM=its=ABS	2	amod
	5	lú	lú=e	person=ERG	6	ERG
	6	ba-ta-túm-mu	Ø-ba-ta-túm-e	VP-MM-from-carry-3SG.A:IPFV	0	root

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

Preposed and postposed numerals can occur in combination with each other:

	# Jagersma, Chap. 7 (293)					
	# ‘(silver) for six rings of five shekels each’					
	# (UET 3:710 2; Ur; 21)					
	1	har	har	ring	0	TERM
	2	5	5	5	3	nummod
	3	giĝ4-ta	giĝ4=ta	shekel=ABL	1	ABL
	4	6-šè	6=še	6=TERM	1	nummod

If adjacent to a unit, mark the unit as head, not the commodity. This is because the same phrase may combine multiple units:

	# Jagersma, Chap. 9 (111)					
	# ‘three pots and three and a half litre of oil’					
	# (Nik 1:257 2:1; L; 24)					
	1	3	eš	three	2	nummod
	2	dug	dug	pot	6	nmod
	3	3	eš	three	5	nummod
	4	½	½	½	3	nummod
	5	sila3	sila3	litre	6	nmod
	6	ì	ì	oil	0	root
	
	# Jagersma, Chap. 9 (95)					
	# ‘four and one-third of a litre of oil’					
	# (Nik 1:261 2:7; L; 24)					
	1	4	limmu	four	2	nummod
	2	sila3	sila3	litre	4	nmod
	3	igi-3-ĝál	igi.eš.ĝál	one.third	2	nummod
	4	ì	ì	oil	0	root

This may mean that multiple numeral modifiers of a commodity do not all depend on the same syntactic head:
	
	# Jagersma, Chap. 9 (103)						
	# ‘eleven and one-third shekels of silver’						
	# (OSP 2:68 1; N; 23)						
	1	11	11	11	2	nummod	
	2	kù	kù	silver	0	root	
	3	giĝ4	giĝ4	shekel	2	appos	unit
	4	igi-3	igi.eš	one.third	4	nummod	


Adverbial numerals (numeral oblique arguments) are annotated `nummod`, regardless of their morphological case:

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

Unmodified pronominal numerals are annotated `nummod`, regardless of morphological case. Note that these can be subsequently disambiguated on grounds of morphology: 

	# Jagersma, Chap. 9 (68)						
	# ‘This was taken away among the second ones that went.’						
	# (DP 313 2:2-3; L; 24)						
	1	2-kam-ma	2-kamma	2-ORD	4	nummod	morphologically marked LOC ignored
	2	ĝen-na-a	ĝen-Ø-'a='a	go-NFIN-NOM=LOC	1	acl	
	4	ba-ře6	Ø-ba-ře6-Ø	VP-MM-bring-3N.S/DO	0	root	

	# Jagersma, Chap. 9 (89)					
	# ‘One-fifth of this is on top of it.’					
	# (RA 76 p.28 1:2; U; 21)					
	1	igi-5-ĝál-bé	igi.ja.ĝál=be=Ø	one.fifth=its=ABS	3	nummod
	2	a-gù-ba	a.gù=be='a	top=its=LOC	3	LOC
	3	ì-íb-ĝál	'i-b(i)-ĝál-Ø	VP-3N:on-be.there-3N.S/DO	0	root

	# Jagersma, Chap. 9 (98)					
	# ‘(gold) for four pieces of jewelry (weighing) one-fourth (of a shekel) each (lit. “with one- fourth”)’					
	# (UET 3:438 4; Ur; 21)					
	1	na-bí-hu-um	na.bí.hu.um	an.ornament	0	TERM
	2	igi-4-ĝál-ta	igi.limmu.ĝál=ta	one.fourth=ABL	1	nummod
	3	4-šè	limmu=še	four=TERM	1	nummod

Exception: Annotate modified numerals (except if modified by mathematical operators or other numerlas) according to their grammatical context, not as `nummod`. This is because these can always be read as elliptic constructions.

	# Jagersma, Chap. 9 (70)						
	# ‘two fourth-quality (lit. “the fourth which is next”) barley-fed rams’						
	# (PDT 2:907 rev 2; D; 21)						
	1	2	min	two	0	nummod	
	2	udu	udu	ram	0	root	
	3	niga	niga	barley-fed	2	appos	
	4	4-kam	limmu-kam	four-ORD	2	appos	modified => not annotated like nominal
	5	ús	ús-Ø	be.next.to-NFIN	4	amod	

Exception: `conj` overrides `nummod`. Again, this reflects elliptic constructions.

	# Jagersma, Chap. 9 (59)					
	# ‘The slave woman and the three of them (i.e., her children) were assigned (by the court) to PN.’					
	# (NG 72 23’-25’; L; 21)					
	1	geme2	geme2	slave.woman	7	ABS
	2	ù	ù	and	1	cc
	3	3-a-bé	eš-'a=be=Ø	three-NOM=its=ABS	1	conj
	5	PN-ra	PN=ra	PN=DAT	7	DAT
	7	ba-na-ge-en6	Ø-ba-nna-ge.n-Ø	VP-MM-3SG.IO-be.firm-3N.S/DO	0	root

Note that the annotation of nummod without cases captures the idea that numeral modification took place, but it fails to capture the exact semantics:
The annotation does not distinguish adverbial numerals (e.g., "doing sth. twice") and adnominal numerals with elided head (e.g., "two of them"). Can be distinguished by morphology.

	# Jagersma, Chap. 9 (57)					
	# ‘He bought the house from the two of them.’					
	# (FAOS 17 88* 13-14; U; 21)					
	1	2-na-ne-ne-šè	min-'a=anēnē=še	two-NOM=their=TERM	4	nummod
	3	é	é=Ø	house=ABS	4	ABS
	4	in-ne-ši-sa10	'i-nnē-ši-n-sa10-Ø	VP-3PL-to-3SG.A-barter-3N.S/DO	0	root

	# Jagersma, Chap. 9 (58)					
	# ‘The three of them received this (lit. “let this approach the hand”).’					
	# (Nik 1:317 2:12-13; L; 24)					
	1	3-a-ne-ne	eš-'a=anēnē=e	three-NOM=their=ERG	4	nummod
	3	šu	šu=e	hand=DIR	4	DIR
	4	ba-ti-éš	Ø-ba-n-ti-eš	VP-3N.IO-3SG.A-approach-3PL	0	root

	# Jagersma, Chap. 9 (71)					
	# ‘secondly’					
	# (Cyl A 9:5; L; 22)					
	1	2-kam-ma-šè	min-kamma=še	two-ORD=TERM	0	nummod

	# Jagersma, Chap. 9 (17)						
	# ‘This is of the eight statues of the Inner Room.’						
	# (DP 53 9:14; L; 24)						
	1	alan	alan	statue	0	root	copular predicate
	2	é-šà-ga	é.šà.g=ak	Inner.room=GEN	1	GEN	
	3	8-ba-kam	ussu=be=ak='am	eight=this=GEN=be:3N.S	1	nummod	

	# Jagersma, Chap. 9 (20)					
	# ‘both eyes’					
	# (VS 14:66 3:2; L; 24)					
	1	igi	igi	eye	0	root
	2	2-na-bé	min-'a=be	two-NOM=this	1	nummod

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

Note that numerals are inherently verbal. Even if this marked explicitly in the morphology, annotate as nummod, not `amod` or `acl`.
	
	# Jagersma, Chap. 9 (21)					
	# ‘the three Bau temples’					
	# (TLB 3:167 1:6; L; 21)					
	1	é	é	house	0	root
	2	dba-ú	ba.ú=ak	Bau=GEN	1	GEN
	3	3-a-bé	eš-'a=be	three-NOM=this	1	nummod

Clausal numerals should be annotated `nummod` if they are used as modifiers, but not if they constitute independent main clauses:
	
	# Jagersma, Chap. 9 (23)					
	# ‘It was square number two (lit. “the square which is two”) that he put on the temple.’					
	# (Cyl A 21:1; L; 22)					
	1	é-a	é='a	house=LOC	4	LOC
	2	sá	sá	square	4	ABS
	3	min-nam	min='am	two=be:3N.S	2	nummod
	4	nam-mi-sì	na-m(u)-bi-n-sì.g-Ø	PFM-VENT-3N:on-3SG.A-put-3N.S/DO	0	root

However, numerals that constitute independent clause that do not modify or stand in apposition to anything should be annotated as clauses:
	
	# Jagersma, Chap. 9 (2)						
	# ‘This is of the six of them.’						
	# (VS 14:172 8:9; L; 24)						
	1	6-a-ne-ne-kam	āš=anēnē=ak='am	six=their=GEN=be:3N.S	0	root	

	# Jagersma, Chap. 7 (22)					
	# ‘This is of the three of them.’					
	# (DP 223 10:5'; L; 24)					
	1	3-a-ne-ne-kam	3=anēnē=ak='am	three=their=GEN=be:3N.S	0	root	(parataxis, etc.)

Numerals that are predicates of copular clauses are annotated as root, not nummod (TBC)
	
	# Jagersma, Chap. 9 (6)					
	# ‘His loaves of bread are 420 (in number).’					
	# (Ukg. 4 6:6; L; 24)					
	1	ninda-né	ninda=ane=Ø	bread=his=ABS	2	ABS
	2	420-nam	/ĝešd-umin/=Ø='am	sixty-seven=ABS=be:3N.S	0	root

Furthermore, `nummod` is used for parts of a numeral, annotated as dependents of the first element in a numeral

	# Jagersma, Chap. 7 (280)					
	# ‘16 1/2 iku of land (measured) with the rope of purchase’					
	# (BM 3:10 1:1; L; 24)					
	1	0.2.4	0.2.4	16	3	nummod
	2	1/2	1/2	1/2	1	nummod
	3	gana2	gana2	land	0	root
	4	éš	éš	rope	3	ABL
	5	sám-ma-ta	sám.ma=ak=ta	purchase=GEN=ABL	4	GEN

	# Jagersma, Chap. 9 (110)						
	# ‘Its labour (expense) is that of twenty and a half days.’						
	# (SACT 2:136 10; U; 21)						
	1	á-bé	á=be=Ø	labour=its=ABS	2	ABS	
	2	u4	u4.d	day	0	root	GEN => copular predicate
	3	20	niš	twenty	2	nummod	
	4	½-kam	½=ak='am	½=GEN=be:3N.S	4	nummod	

TBC: attach numerals to last numeral? this may be semantically incorrect (as in the following example), but this would facilitate automated annotation as numeral scope will be hard to ascertain automatically.

	# Jagersma, Chap. 9 (124)						
	# ‘The labour of the troops for this is that of seventy-two days and four-fifths (lit. “two- thirds and eight-sixtieths”).’						
	# (Civil FI p.191 A.5835 1:7; U; 21)						
	1	á	á	labour	3	ABS	
	2	eren2-na-bé	eren2=ak=be=Ø	troops=GEN=its=ABS	1	GEN	
	3	u4	u4.d	day	0	root	copular predicate
	4	72	72	72	3	nummod	
	5	⅔	⅔	⅔	4	nummod	
	6	8	8	8	4	nummod	
	7	giĝ4-kam	giĝ4=ak='am	shekel=GEN=be:3N.S	6	nummod	

> Note: Earlier, we used `compound` and `flat` for the internal structure of complex numerals. But this is inconsistent with the annotation of *la2* "minus" as `acl` (should be `flat` as well, then). Hence, another relation.

Note: The `nummod` rule is motivated by the need to facilitate automated annotation and to improve inter-annotator agreement.

Complex numerals can include mathematical operators. Annotate `lá`  "minus" as `acl` with `nummod` dependent. The head of `lá` should be `nummod`.

	# Jagersma, Chap. 9 (102)					
	# ‘one and two-thirds of a litre of sesame oil’					
	# (BIN 8:156 12; I?; 21)					
	1	2	min	two	2	nummod
	2	sila3	sila3	litre	5	nmod
	3	lá	lá	minus	2	acl
	4	igi-3	igi.eš	one.third	3	nummod
	5	ì-ĝiš	ì.ĝiš	sesame.oil	0	root

TODO: confirm the analysis of `si-la`:
	
	# Jagersma, Chap. 9 (122)					
	# ‘ten shekels (= ten sixtieths) split off’					
	# (MSL 14 p.195 and 254; MSL 3 p.134)					
	1	kin-	giĝ4	shekel	0	root
	2	gu-	u	ten	1	nummod
	3	si-la	si.il-Ø-'a	split.off-NFIN-NOM	1	amod

TODO: confirm that ordinals are currently treated as `nummod`. In certain constellations, treating them like `amod` may be preferrable. However, such contexts are hard to detect automatically, hence left for subsequent refinement.

	# Jagersma, Chap. 9 (79)						
	# ‘This is the second heap.’						
	# (MVN 3:5 4:1; L; 24)						
	1	guru7	guru7	heap	0	root	
	2	2-kam-ma-am6	min-kamma=Ø='am	two-ORD=ABS=be:3N.S	1	nummod	
							
	# Jagersma, Chap. 9 (80)						
	# ‘his second son’						
	# (RTC 76 2:4; L; 24)						
	1	dumu	dumu	son	0	root	
	2	2-kam-ma-né	min-kamma=ane	two-ORD=his	1	nummod	?amod
							
	# Jagersma, Chap. 9 (81)						
	# ‘his second general’						
	# (Cyl B 8:7; L; 22)						
	1	šagina	šagina	general	0	root	
	2	2-kam-né	min-kamma=ane	two-ORD=his	1	nummod	?amod

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

Adverbial clauses in Sumerian are annotated in accordance with their morphology, not their functional interpretation. 

`advcl` is thus used for a subset of adverbial clauses only: 
- subordinate clauses with an explicit `mark` that indicates an adverbial function, e.g., *tukumbi* "if", or
- a temporal clause established with the perfective relative past marker *'u* (MTAAC gloss `ANT`).

"For [conditional clauses,] Sumerian uses clauses introduced by u4-da ‘if’ or tukum-bé ‘if’." (Jagersma 2010: 524)
In addition, non-conditional adverbial clauses can also be marked morphologically

	ETCSRI: `V1=ANT` *u* "prefix of anterioriy"
	Jagersma: `REL.PAST` *ù* {'u} "relative-past prefix"

MTAAC `ANT`, e.g.
		
	u3-na-a-du11	u-nn-a-e-dug[speak]	N	ANT.3-SG-H.DAT.2-SG-A.V.3-SG-P
	
"A verbal form with the prefix {'u} is subordinate to the following verb and expresses an anterior action. A clause with such a form can usually be translated into English with a temporal clause introduced by ‘when’ or ‘after’" (Jagersma 2010: 518)
	
"The prefix {'u} has a subordinating function. If a clause has a verbal form with the prefix {'u} as its predicate, it is a subordinate clause and part of a larger sentence." (Jagersma 2010: 522)
	
	# Jagersma, Chap. 11 (45)						
	# ‘When Gududu’s sealed document is brought (dynamic passive), Akalla’s sealed document is to be destroyed.’						
	# (UTAMI 3:Um. 2247 3-6; U; 21)						
	1	kišib	kišib	seal	4	ABS	
	2	gu-du-du	gu.du.du=ak=Ø	Gududu=GEN=ABS	1	GEN	
	4	ù-um-ře6	'u-m(u)-ře6-Ø	REL.PAST-VENT-bring-3N.S/DO	0	root	
	6	kišib	kišib	seal	9	ABS	
	7	a-kal-la	a.kal.la=ak=Ø	Akalla=GEN=ABS	6	GEN	
	9	ze-re-dam	ze.r-ed-Ø='am	destroy-IPFV-NFIN=be:3N.S	4	parataxis	shallow annotation

Functionally, these forms can also have a (polite) imperative function, esp., u3-na-a-du11 "speak!", lit. "when you have said to him". (Jagersma (2010:526): "Akkadian letters also show an imperative form in the address. Accordingly, the form ù-na-adu11 ‘(lit.) when you have said to him’ must express here an instruction, probably in a polite way.")

	# CDLI, P131033
	1	lu2-{d}szul-gi-ra	Lu-Szulgi	PN	PN	2	DAT
	2	u3-na-a-du11	u-nn-a-e-dug[speak]	N	ANT.3-SG-H.DAT.2-SG-A.V.3-SG-P	6	advcl
	3	1(disz)	1(disz)[one]	NU	NU	4	nummod
	4	udu	udu[sheep]	N	N	6	ABS
	5	ur-{d}iszkur	Uriszkur	PN	PN	6	TERM
	6	i3-dab5	dab[seize]	V	FIN.3-SG-H-A.V.3-SG-P	0	root
	7	ur-{d}hendur-sag-ra	Ur-Hendursag	PN	PN	10	DAT
	8	sze-na	sze[barley]	N	N	10	LOC
	9	szu	szu[hand]	N	N.ABS	10	ABS
	10	ha-mu-na-a-ba-re	_[release]	V	MOD1.VEN.3-SG-H.DAT.3-SG-H-A.V.3-SG-P	6	parataxis
	# To Lu-Šulgi speak! "1 ram did Ur-Iškur receive". To Ur-Ḫendursag: "In his barley may he release!"

Note that `ANT` (Jagersma's `REL.PAST`) can also occur in relative clauses (`acl`). Annotate these as `acl`, not `advcl`: "Verbal forms with the prefix {'u} are also found in nominalized clauses (...). Since such clauses are already subordinate, the prefix {'u} primarily adds the notion ‘anterior action’ to the event expressed by such clauses." (Jagersma 2010: 525):
	
	# Jagersma, Chap. 24 (38)						
	# ‘Your having directed your eyes to the people means rain and abundance (lit. “Your eyes which you have brought out towards the people are rain and abundance”).’						
	# (Cyl A 3:4; L; 22)						
	1	igi	igi	eye	4	ABS	marked on 3
	2	ùĝ-šè	ùĝ=še	people=TERM	3	TERM	
	3	ù-ši-bar-ra-zu	'u-m(u)-ši-e-bar-Ø-'a=zu=Ø	REL.PAST-VENT-to-2SG.A-be.outside-3N.S/DO-NOM=your=ABS	1	acl	not advcl
	4	šeĝx(=IM.A)	šeĝx	rain	0	root	ABS -> copular predicate
	5	hé-ĝál-la-àm	hé.ĝál=Ø='am	abundance=ABS=be:3N.S	4	appos	
	
This also extends to cases in which an `acl` clause serves an adverbial function (expressed by `acl.LOC`, here):
	
	# Jagersma, Chap. 17 (68)					
	# ‘when after Ningirsu, my master, will have called for him among the people’					
	# (St B 8 14-16; L; 22)					
	1	dnin-ĝír-su	nin.ĝír.su.k	Ningirsu	6	ERG
	2	lugal-ĝu10	lugal=ĝu=e	king=my=ERG	1	appos
	3	/	_	_	6	punct
	4	ùĝ-ĝá	ùĝ='a	people=LOC	6	LOC
	5	gù	gù=Ø	voice=ABS	6	ABS
	6	ù-na-dé-a	'u-nna-n-dé-Ø-'a='a	REL.PAST-3SG.IO-3SG.A-pour-3N.S/DO-NOM=LOC	0	advcl

This also extends to "adverbial" relative clauses with a nominal head:
	
	# Jagersma, Chap. 18 (114a)					
	# ‘when someone holds on to the field’					
	# (MAD 4:151 10; 23)					
	1	u4	u4.d	day	0	LOC
	2	ašag-ga	ašag='a	field=LOC	4	LOC
	3	lú	lú=Ø	man=ABS	4	ABS
	4	ù-ma-a-řú-a	'u-m(u)-ba-e-řú-Ø-'a	REL.PAST-VENT-MM-on-hold-3SG.S/DO-NOM	1	acl
	
Note that double marking of adverbial clauses can occur, i.e., when combining *tukumbi* and *ù-*:
	
		# Jagersma, Chap. 24 (34)						
		# ‘If Ur-Amma the shepherd takes an oath about this, this sealed document is to be broken.’						
		# (CST 533 7-10; U; 21)						
		1	tukum-bé	tukum.bé	if	7	mark	
		2	/	_	_	7	punct	
		3	ur-àm-ma	ur.àm.ma	Uramma	7	ERG	
		4	sipa	sipa.d=e	shepherd=ERG	3	appos	
		5	/	_	_	7	punct	
		6	nam-erim2-bé	nam.'erim=be=Ø	oath=its=ABS	7	ABS	
		7	ù-un-ku5	'u-n-ku5.ř-Ø	REL.PAST-3SG.A-cut-3N.S/DO	10	advcl	double marking: tubumbi + ù-
		8	/	_	_	10	punct	
		9	kišib-bé	kišib=be=Ø	seal=this=ABS	10	ABS	
		10	ze-re-dam	ze.r-ed-Ø='am	break-IPFV-NFIN=be:3N.S	0	root	

Conditional and temporal adverbial clauses can occur in the same sentence.
	
		# Jagersma, Chap. 24 (36)					
		# ‘When the tablet about this is looked at, if this is not written on it, Ur-Meme will replace it.’					
		# (NG 209 18-21; N; 21)					
		1	im-ba	im=be='a	clay=its=LOC	3	LOC
		2	igi	igi=Ø	eye=ABS	3	ABS
		3	ù-bar	'u-b(i)-bar-Ø	REL.PAST-3N:on-be.outside-3N.S/DO	10	advcl
		4	/	_	_	10	punct
		5	tukum-bé	tukum.be	if	6	mark
		6	nu-ub-sar	nu='i-b(i)-sar-Ø	NEG=VP-3N:on-write-3N.S/DO	10	advcl
		7	/	_	_	10	punct
		8	ur-me-me-ke4	ur.me.me.k=e	Urmeme=ERG	10	ERG
		9	/	_	_	10	punct
		10	íb-su-su	'i-b-su.g:RDP-e	VP-3N.DO-repay:IPFV-3SG.A:IPFV	0	root
		
		# Jagersma, Chap. 24 (37)						
		# ‘When their prebends have been surveyed, if they are too small, the three men whose pre-bends are too small will take it, (but) if they are sufficient, Lū-šalim will take it.’						
		# (NG 215 3-8; U; 21)						
		1	šuku-bé	šuku.ř=be=Ø	prebend=its=ABS	2	ABS	
		2	ù-ul-gíd	'ul-gíd-Ø	REL.PAST-survey-3N.S/DO	12	advcl	
		3	/	_	_	12	punct	
		4	tukum-bé	tukum.be	if	5	mark	
		5	ì-lá	'i-lá-Ø	VP-be.short-3N.S/DO	12	advcl	
		6	/	_	_	12	punct	
		7	lú	lú	man	12	ERG	mared on 10
		8	3	3	3	7	nummod	
		9	šuku-bé	šuku.ř=be=Ø	prebend=its=ABS	10	ABS	
		10	ì-lá-a	'i-lá-Ø-'a=e	VP-be.short-3N.S/DO-NOM=ERG	7	acl	
		11	/	_	_	12	punct	
		12	ba-ab-tùm	Ø-ba-b-tùm-Ø	VP-MM-3N.A-carry:IPFV-3N.S/DO	0	root	
		13	/	_	_	12	punct	
		14	tukum-bé	tukum.be	if	15	mark	
		15	íb-si	'i-b-si-Ø	VP-3N.OO-fill-3N.S/DO	18	advcl	
		16	/	_	_	18	punct	
		17	lú-ša-lim-e	lú.ša.lim=e	Lū.šalim=ERG	18	ERG	
		18	ba-an-tùm	Ø-ba-n-tùm-Ø	VP-MM-3SG.A-carry:IPFV-3N.S/DO	12	parataxis	

No nesting of adverbial clauses. If multiple adverbial clauses occur in a sentence and interpretation is ambiguous as to whether the head of an advcl is another advcl or a main clause, annotate the main clause. (Note: In annotation practice, this means that `advcl` is very unlikely to modify another `advcl`.)
[Objective: In the following example, it was basically impossible to find an analysis that was consistent with the translation and with the requirement that an 'u-`advcl` should modify a following clause. Either this is not a general rule, or the nesting of adverbial clauses is inferred rather than morphologically coded. We go with the latter assumption and prefer a shallow annotation. NB: Translation hints at 22 -parataxis-> 14 -advcl-> 30, morpology hints at 14 -advcl-> 22 -advcl-> 30; syntactic parallelism between 25 and 14 also hints at 14 -advcl-> 30.]
	
		# Jagersma, Chap. 24 (35)						
		# ‘When a beautiful donkey is born to a subordinate and his foreman says to him “I want to buy it from you”; whether he lets him buy it from him and has said “Pay me the price I want,” or whether he does not let him buy it from him, the foreman must not become angry with him!’						
		# (Ukg. 4 11:20-31; L; 24)						
		1	RU-lugal-ra	RU.lugal.k=ra	subordinate=DAT	6	DAT	
		2	/	_	_	6	punct	
		3	anše	anše	donkey	6	ABS	marked on 4
		4	sa6-ga	sa6.g-Ø-'a=Ø	be.good-NFIN-NOM=ABS	3	amod	
		5	/	_	_	6	punct	
		6	ù-na-dú	'u-nna-dú.d-Ø	REL.PAST-3SG.IO-be.born-3N.S/DO	30	advcl	temporal, before 11
		7	/	_	_	30	punct	
		8	ugula-né	ugula=ane=e	foreman=his=ERG	11	ERG	
		9	ga-šè-sa10	ga-e-ši-sa10	MOD:1SG.A/S-2SG-to-barter	11	ccomp	direct speech
		10	/	_	_	11	punct	
		11	ù-na-du11	'u-nna-n-du11.g-Ø	REL.PAST-3SG.IO-3SG.A-say-3N.S/DO	30	advcl	temporal, before conditionals
		12	/	_	_	30	punct	
		13	u4-da	u4.da	if	14	mark	
		14	mu-šè-sa10-sa10	Ø-mu-n-ši-n-sa10:RDP-e	VP-VENT-3SG-to-3SG.OO-barter:IPFV-3SG.A:IPFV	30	advcl	
		15	/	_	_	30	punct	
		16	kù	kù.g	silver	20	ABS	
		17	šà-ĝá	šà.g=ĝu='a	heart=my=LOC	18	LOC	
		18	a-sa6-ga	'a-n(i)-sa6.g-Ø-'a=Ø	VP-in-be.good-3N.S/DO-NOM=ABS	16	acl	
		19	/	_	_	20	punct	
		20	lá-ma	lá-Ø-ma-b	weigh-VP-1SG.IO-3N.DO	22	ccomp	
		21	/	_	_	22	punct	
		22	ù-na-du11	'u-nna-n-du11.g-Ø	REL.PAST-3SG.IO-3SG.A-say-3N.S/DO	30	advcl	temporal, should modify following clause; but translation indicates that this dependent on 14
		23	/	_	_	30	punct	
		24	u4-da	u4.da	if	25	mark	
		25	nu-šè-sa10-sa10	nu='i-n-ši-n-sa10:RDP-e	NEG=VP-3SG-to-3SG.OO-barter:IPFV-3SG.A:IPFV	30	advcl	
		26	/	_	_	30	punct	
		27	ugula	ugula=e	foreman=ERG	30	ERG	
		28	lipiš-bé	lipiš=be=Ø	anger=its=ABS	30	ABS	
		29	/	_	_	30	punct	
		30	na-na-tag-ge	na-nna-tag-e	NEG.MOD-3SG.IO-touch-3SG.A:IPFV	0	root	

Note that adverbial clauses without explicit arguments are annotated `advcl`, not `advmod`. 

	# Jagersma, Chap. 11 (46)					
	# ‘Whenever one (of Ur-Enlila’s sealed documents) is brought (dynamic passive), it is to be destroyed.’					
	# (NRVN 1:235 3-4; N; 21)					
	1	ù-um-re-re	'u-m(u)-ře6-ře6-Ø	REL.PAST-VENT-bring-bring-3N.S/DO	3	advcl
	2	/	_	_	3	punct
	3	ze-re-dam	ze.r-ed-Ø='am	destroy-IPFV-NFIN=be:3N.S	0	root

Note: The objective for the apparent imbalance with `acl`:`amod` is that adverbial clauses necessarily represent cases of ellipsis whereas relative clauses are morphologically marked as nominalizations (i.e., for an adjectival function).
	
	TODO: check all instances of `ANT` in corpus

Other forms of subordinate clauses with adverbial interpretation can be formed by combining markers of syntactic subordination with an oblique case. They are to be annotated as `acl+case`. 

	# Jagersma, Chap. 27 (180)						
	# ‘Nin-Idmah took an oath by the king’s name – as to that she would not go back on Irini-she, the herald.’						
	#	(SRU 84 13-16; I; 23) (Similarly: SRU 85 1-6; I; 23)					
	1	nin-íd-<mah>-e	nin.íd.mah=e	Nin.Idmah=ERG	5	ERG	
	2	/	_	_	5	punct	
	3	mu	mu	name	5	ABS	
	4	lugal	lugal=ak=Ø	king=GEN=ABS	3	GEN	
	5	in-pa	'i-n-pà.d-Ø	VP-3SG.A-find-3N.S/DO	0	root	
	6	/	_	_	10	punct	
	7	iri-né-šè	iri.né.šè	Irineshe	10	DAT	
	8	niĝir-ra	niĝir=ra	herald=DAT	8	appos	
	9	/	_	_	10	punct	
	10	la-ba-gi4-gi4-da-šè	nu=Ø-ba-n-gi4:RDP-ed-Ø-'a=še	NEG=VP-MM-3SG.OO-turn:IPFV-IPFV-3SG.S:IPFV-NOM=TERM	5	acl+TERM	adverbial clause

The label `advcl` is only to be used where no morphological case marking is used or restored during morphological annotation.

#### perfective relative past

Jagersma (2010: 518, 521): "A verbal form with the prefix {'u} is subordinate to the following verb and expresses an anterior action. A clause with such a form can usually be translated into English with a temporal clause introduced by ‘when’ or ‘after’ ... 
The relative-past prefix {'u} is incompatible with the imperfective and only occurs in perfective verbal forms. A form with {'u} is subordinate to the following verb and expresses an action with the approximate meaning ‘under the circumstance that (…) has happened’. It designates an action which is both anterior and circumstantial to the action expressed by the following verb. A clause with such a verbal form can usually be translated into English with a temporal clause introduced by ‘when’ or ‘after’, or with a participial construction."

	# Jagersma, Chap. 24 (18)					
	# ‘The sealed document about this was lost. When it is found, it is to be destroyed.’					
	#	(OrSP 47/49:411 7-9; U; 21). The phrasal verb ú-gu—dé means ‘lose’				
	1	kišib-bé	kišib=be=Ø	seal=its=ABS	3	ABS
	2	ú-gu	ú.gu=e	?=DIR	3	DIR
	3	ba-an-dé	ba-n(i)-dé-Ø	MM-in-pour-3N.S/DO	0	root
	4	/	_	_	3	punct
	5	ù-ul-pà	'u-pà.d-Ø	REL.PAST-find-3N.S/DO	7	ccomp
	6	/	_	_	7	punct
	7	ze-re-dam	ze.r-ed-Ø='am	destroy-IPFV-NFIN=be:3N.S	3	parataxis

Note that `advcl` should also be used if the the clause does not contain any modifiers. There is no `advmod` tag. (Note that this is different from the treatment of `acl` and `amod`. This is motivated by the comparably higher number of "adjectives" that functionally overlap with adjectives in English, whereas the functional counterpart of English adverbs are mostly Sumerian nominals with oblique case.)

	# Jagersma, Chap. 24 (26)					
	# ‘When she (viz. a slave bought) gets lost or when she dies, Ur-Suen will not place a claim on Ur-Shulpae.’					
	#	(FAOS 17:94** 8-11; U; 21). Note that the phrasal verb ú-gu—dé means ‘lose’ _				
	1	ú-gu	ú.gu=Ø	?=ABS	2	ABS
	2	a-ba-dé	'u-ba-dé-Ø	REL.PAST-MM-pour-3N.S/DO	10	advcl
	3	a-ba-úš	'u-ba-'úš-Ø	REL.PAST-MM-die-3N.S/DO	10	advcl
	4	/	_	_	10	punct
	5	ur-dsuen-ke4	ur.suen.k=e	Ursuen=ERG	10	ERG
	6	/	_	_	10	punct
	7	ur-dšul-pa-è	ur.šul.pa.è.k=ra	Urshulpae=DAT	10	DAT
	8	/	_	_	10	punct
	9	inim	inim=Ø	word=ABS	10	ABS
	10	nu-un-ĝá-ĝá	nu='i-n-ĝar:RDP-e	NEG=VP-3SG.OO-place:IPFV-3SG.A:IPFV	0	root

	# Jagersma, Chap. 11 (46)					
	# ‘Whenever one (of Ur-Enlila’s sealed documents) is brought (dynamic passive), it is to be destroyed.’					
	# (NRVN 1:235 3-4; N; 21)					
	1	ù-um-re-re	'u-m(u)-ře6-ře6-Ø	REL.PAST-VENT-bring-bring-3N.S/DO	3	advcl
	2	/	_	_	3	punct
	3	ze-re-dam	ze.r-ed-Ø='am	destroy-IPFV-NFIN=be:3N.S	0	root

The objective for the apparent imbalance with `acl`:`amod` is that adverbial clauses necessarily represent cases of ellipsis whereas relative clauses are morphologically marked as nominalizations (i.e., for an adjectival function).	

TODO: update references to advcl elsewhere in this document
TODO: scan data and examples for instances of this morpheme. how is this represented in CDLI?

#### *tubumbi*

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

	# Jagersma, Chap. 6 (43)					
	# ‘if after today Ur-Sha’usha and my children run away’					
	# (ZA 55 p.68:ITT 5:9594 3'-4'; L; 21)					
	1	tukum-bé	tukum.bé	if	7	mark
	2	u4-da-ta	u4.da=ta	today=ABL	7	ABL
	4	ur-dša-u18-ša	ur.ša.u18.ša	Ur.Sha’usha 	7	ABS
	5	ù	ù	and 	4	cc
	6	dumu-ĝu10-ne	dumu=ĝu=enē=Ø	child=my=PL=ABS 	4	conj
	7	ba-zàh-dè-eš	h:=Ø-ba-zàh-ed-eš	MOD=VP-MM-run.away-IPFV-3PL.S:IPFV	0	advcl


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

As for relative clauses with oblique case that translate to adverbial clauses in English, these are not annotated as `advcl` but according to their morphology, e.g., `acl+ABL` and `acl+DIR` in the following examples:

	# Jagersma, Chap. 6 (41)					
	# ‘after Ursisi, the barber, had raised AN.LUH’s sons for three years’					
	# (BIN 8:293 3:2-5; N; 23)					
	1	mu	mu	year	10	ABL
	2	3-àm	3='am	3=be:3N.S	1	nummod
	3	dumu	dumu	son	10	ABS
	4	AN.LUH	AN.LUH=ak=Ø	AN.LUH=GEN=ABS	3	GEN
	6	ur-si4-si4	ur.si4.si4	Ursisi	10	ERG
	7	šu-i	šu.i=e	barber=ERG	6	appos
	9	á	á=Ø	strength=ABS	10	ABS
	10	ì-è-éš-a-ta	'i-n-'è-eš-'a=ta	VP-3SG.A-go.out-3PL.S/DO-NOM=ABL	0	acl+ABL

	# Jagersma, Chap. 6 (42)					
	# ‘in order to arrest fugitives’					
	# (RTC 355 10; L; 21)					
	1	lú-zàh	lú.zàh=Ø	fugitive=ABS	2	ABS
	2	dab5-dab5-dè	dab5-dab5-ed-Ø=e	take-take-IPFV-NFIN=DIR	0	acl+DIR


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

	# Jagersma, Chap. 7 (86)					
	# ‘of Ashniu’s sealed documents which are at Kitushlu’s place, their duplicates’					
	# (TPTS 1:123 14-16; ?; 21)					
	1	kišib	kišib	seal	0	root
	2	aš-ni-u18	aš.ni.u18=ak	Ashniu=GEN	1	GEN
	4	ki	ki	place	7	LOC
	5	ki-tuš-lú-ka	ki.tuš.lú=ak='a	Kitushlu=GEN=LOC	4	GEN
	7	mu-ĝál-la	Ø-mu-n(i)-ĝál-Ø-'a=ak	VP-VENT-in-be.there-3N.S/DO-NOM=GEN	1	acl
	8	gaba-ri-bé	gaba.ri=be	copy=its	1	parataxis

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

TO BE CONFIRMED: `parataxis` vs. `acl` vs. `abs` (~ other cases or `vocative`):
If a noun phrase is to be connected with a statement and overt morphology for syntactic subordination (=> `acl`) or case (=> `abs`, etc) are missing, different analyses are possible. Suggestion:

- annotate case if and only if explicit in the morphological glossing
- prefer `parataxis` interpretation: the detached noun phrase is inherently propositional, e.g., an elliptic representation of a transaction
- prefer `acl` interpretation is the detached noun phrase is not inherently propositional, e.g., because its nominal head is subsequently modified
- in case of doubt, chose the more frequently applied construction for a specific constellation and leave a comment
- if no preference can be established, leave a comment and annotate `parataxis` (to be confirmed)

	# Jagersma, Chap. 7 (102)						
	# ‘One bear: the dogs seized it in the presence of the king.’						
	# (UDT 123 8-9; D; 21)						
	1	1	1	1	2	nummod	
	2	aza	aza	bear	0	root	
	3	igi	igi	eye	7	TERM	
	4	lugal-šè	lugal=ak=še	king=GEN=TERM	3	GEN	
	6	ur-gi7-re	ur.gi7.r=e	dog=ERG	7	ERG	
	7	íb-dab5	'i-b-dab5-Ø	VP-3N.A-take-3N.S/DO	2	acl	no morphological marks of subordination. parataxis ? (=> one bear is propositional)

	# Jagersma, Chap. 7 (247)						
	# ‘15 men: With three cubits of work for one man, they took it in charge.’						
	# (VS 25:86 1:1- 4; L; 24)						
	1	15	15	15	2	nummod	
	2	lú	lú	man	0	root	
	4	lú	lú	man	11	TERM	
	5	1-šè	1=še	1=TERM	4	nummod	
	7	kíĝ	kíĝ	work	11	ABL	
	8	kùš	kùš	cubit	7	appos	
	9	3-ta	3=ta	3=ABL	8	nummod	
	11	e-dab5	'i-b-dab5-Ø	VP-3N.A-take-3N.S/DO	2	parataxis	? acl

alternative analysis here with 2 being ABS argument of 6, and 6 being acl of 1. However, this means to ignore the copula at 2
	
	# Jagersma, Chap. 9 (9)						
	# ‘because (lit. “for the name of that”) three sheep of the palace were caught among his sheep’						
	# (AAICAB I/2 pl. 104 Ashm. 1937-61 3-4; D; 21)						
	1	mu	mu	name	0	TERM	
	2	udu	udu	sheep	1	acl+GEN	marked on 6
	3	é-gal	é.gal=ak	palace=GEN	2	GEN	
	4	3-àm	eš=Ø='am	three=ABS=be:3N.S	2	nummod	
	5	udu-na	udu=ane='a	sheep=his=LOC	6	LOC	
	6	ba-an-dab5-ba-šè	Ø-ba-n(i)-dab5-Ø-'a=ak=še	VP-MM-in-take-3N.S/DO-NOM=GEN=TERM	2	parataxis	

If an argument is morphologically marked by an (emphatic?) copula and an interpretation as independent clause is semantically and syntactically possible (a minimal requirement is that it does not interrupt the sequence of arguments), annotate in accordance with its overt morphology:

	# Jagersma, Chap. 15 (84)					
	# ‘Why does Urlama not allow grazing?’					
	#	(TCS 1:121 6-9; L; 21)				
	1	a-na-aš-àm	a.na=š(e)='am	what=TERM=be:3N.S	0	root
	2	/	_	_	1	punct
	3	ur-dlama3-ke4	ur.lama3.k=e	Urlama=ERG	8	ERG
	4	/	_	_	8	punct
	5	ú	ú=Ø	grass=ABS	6	ABS
	6	gu7-dè	gu7-ed-Ø=e	eat-IPFV-NFIN=DIR	8	acl+DIR
	7	/	_	_	8	punct
	8	nu-ub-še-ge	nu='i-b-še.g-e	NEG=VP-3N.OO-allow-3SG.A:IPFV	1	parataxis

DISCUSSION: special treatment of seals

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

The predicate of a copular clause is its head. The morphological case of a copular predicate is *not* annotated. In many cases, this will be an `ABS` argument, so, giving it a clausal annotation allows to reliably distinguish subject (first `ABS` argument) and predicate (second `ABS` argument):

	# Jagersma, Chap. 7 (115)						
	# ‘that Luzah was a slave of (the god) Shara’						
	# (NG 212 46; U; 21)						
	1	lú-zàh	lú.zàh=Ø	Luzah=ABS	2	ABS	
	2	urdu2	urdu2.d	slave	0	root	ABS => copular predicate
	3	dšara2	šara2=ak=Ø	Shara=GEN=ABS	2	GEN	
	4	ì-me-a	'i-me-Ø-'a	VP-be-3SG.S-NOM	2	cop	

This also includes cases in which the head has a more complex structure, e.g., do not annotate the genitive relation in the following example:

	# Jagersma, Chap. 5 (21)						
	# ‘They are the ones of Geme-Bau.’						
	# (Nik 1:7 2:4; L; 24)						
	1	geme2-{d}ba-ú-ka-me	geme2.ba.ú.k=ak=Ø=me-eš	Geme-Bau=GEN=ABS=be-3PL.S	0	root	copular predicate is a headless absolutive NP with a genitive argument
	
Likewise, do not annotate the relative clause that is the copular predicate in the following example:

	# Jagersma, Chap. 7 (161)						
	# ‘As for your (bent) spine, you are (like) one who writes tablets all the time.’						
	# (Lugal- banda II 122; OB)						
	1	murgu2-zu	murgu2=zu=e	back=your=DIR	3	DIR	
	2	dub	dub=Ø	tablet=ABS	3	ABS	
	3	sar-sar-re-me-en	sar-sar-ed-Ø=Ø=me-en	write-write-IPFV-NFIN=ABS=be-2SG.S	0	root	acl => ABS => copular predicate

	
Note that the copular predicate can also carry cases other than `ABS`. In these cases they can be read as adnominal cases of a headless NP (e.g., "`ABL+ABS`").

	# Jagersma, Chap. 29 (90)						
	# ‘if it was by the hand of SI.A-a’						
	#	(NG 215 49; U; 21)					
	1	tukum-bé	tukum.bé	if	2	mark	
	2	šu	[šu	[hand	0	advcl	ABL => copular predicate; tukumbi => advcl
	3	SI.A-a-ta-àm	SI.A.a=ak=ta]='am	SI.A.a=GEN=ABL]=be:3N.S	2	GEN	


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

TODO: change internal structure of month names according to the following Jagersma examples:

	# Jagersma, Chap. 7 (167)					
	# ‘in the month when the granaries were heaped up’					
	# (BIN 8:362 7:3; L; 24)					
	1	iti	iti.d	month	0	LOC
	2	guru7	guru7	granary	3	ABS
	3	dub-ba-a	dub-Ø-'a='a	heap.up-NFIN-NOM=LOC	1	acl

	
	# Jagersma, Chap. 7 (168)					
	# ‘in the month when Bau’s wool is supplied’					
	# (Nik 1:63 13:2; L; 24)					
	1	iti	iti.d	month	0	LOC
	2	siki	siki	wool	4	ABS
	3	dba-ú	ba.ú=ak=Ø	Bau=GEN=ABS	2	GEN
	4	e-ta-ĝar-ra-a	'i-b-ta-ĝar-Ø-'a='a	VP-3N-from-place-3N.S/DO-NOM=LOC	1	acl

? what about the following ?
	(we could model it as appos by assuming that it contains an implicit copula, i.e., "in the month that is Duku")
	
	# Jagersma, Chap. 7 (186)					
	# ‘in the month Duku’					
	# (NRVN 1:38 5; N; 21)					
	1	iti	iti.d	month	0	LOC
	2	du6-kù-ga	du6.kù.g='a	Duku=LOC	1	appos

	# Jagersma, Chap. 7 (67)					
	# ‘in the month of Shunumun’					
	# (NRVN 1:114 5; N; 21)					
	1	iti	iti.d	month	0	LOC
	2	šu-numun-a-ka	šu.numun=ak='a	Shunumun=GEN=LOC	1	GEN
						
	# Jagersma, Chap. 7 (68)					
	# ‘in the month of Nesag’					
	# (SANTAG 6:313 obv 5; U; 21)					
	1	iti	iti.d	month	0	LOC
	2	nesaĝ2-ka	nesaĝ2=ak='a	Nesag=GEN=LOC	1	GEN


Note: When describing periods, other cases need to be assumed

	# Jagersma, Chap. 7 (69)					
	# ‘from the month of Shunumun’					
	# (YOS 4:162 5; U; 21)					
	1	iti	iti.d	month	0	ABL
	2	šu-numun-na-ta	šu.numun=ak=ta	Shunumun=GEN=ABL	1	GEN

	# Jagersma, Chap. 7 (225)					
	# ‘from the month Shulgi’s Festival until (and including) the month Shuesha’					
	# (UET 3:988 6-7; Ur; 21)					
	1	iti	iti.d	month	0	ABL
	2	ezem	ezem	festival	1	appos
	3	dšul-ge-ta	šul.ge.r=ak=ta	Shulgi=GEN=ABL	2	GEN
	5	iti	iti.d	month	1	TERM
	6	šu-eš5-ša-šè	šu.eš5.ša=še	Shuesha=TERM	5	appos

TODO: consolidate guidelines and data:
- taglist recommends `appos` for `MN` (month name), with head being the word *iti* (month)
	- this is also implemented in the MTAAC pre-annotation
	- the examples above use `LOC` for dependencies within dates and `date` for the head element of a date
- taglist recommends `appos` for the clause after *mu*
	- apply `acl` systematically, check in the data
- check treatment in pre-annotation and annotation projection

### Head of verb-less transactions

In transactions that lack an explicit verb, annotate the commodity as functional head, without marking its case. This may not not reflect the linguistic reality, but the commodity is the only obligatory part of a transaction, so this will produce more coherent annotations.

"Distributive expressions (...) in their full form contain a verbal form" (Jagersma 2010, p.158)

	# Jagersma, Chap. 7 (105)					
	# ‘One labourer makes it with (a work load of) two nindan in one day.’					
	# (TMHC NF 1/2:294 6-7; N; 21)					
	1	ĝuruš	ĝuruš	labourer	8	ERG
	2	1-e	1=e	1=ERG	1	nummod
	3	u4	u4.d	day	8	LOC
	4	1-a	1='a	1=LOC	3	nummod
	5	2	2	2	6	nummod
	6	nindan-ta	nindan=ta	nindan=ABL	8	ABL
	8	ì-a-ke4	'i-'ak-e	VP-make-3SG.A:IPFV	0	root
	
"Usually, however, such expressions lack the verbal form:" (Jagersma 2010, p.158)	
						
	# Jagersma, Chap. 7 (106)						
	# ‘with half a nindan by one labourer’						
	# (CT 7 pl.43:BM 17759 rev 12; L; 21)						
	1	ĝuruš	ĝuruš	labourer	4	ERG	
	2	1-e	1=e	1=ERG	1	nummod	
	3	½	½	½	4	nummod	
	4	nindan-ta	nindan=ta	nindan=ABL	0	root	treat commodity as functional head
							
In those eamples, assume that the commodity is the functional head. This may not correspond to the linguistic reality of these concepts.

	# Jagersma, Chap. 7 (107)						
	# ‘with 210 litres of NÍG.KI-fish per month by a spear labourer’						
	# (MVN 10:149 =TLB 3:145 =TLB 3:146 obv 1:4; L; 21)						
	1	ĝuruš	ĝuruš	labourer	6	ERG	
	2	ĝiš-gíd-da-ke4	ĝiš.gíd.da=ak=e	spear=GEN=ERG	1	GEN	
	3	iti	iti.d	month	6	LOC	
	4	1-a	1='a	1=LOC	3	nummod	
	5	ku6	ku6	fish	6	nmod	assuming this is a proper name
	6	NÍG.KI	NÍG.KI	NÍG.KI	0	ABL	ellipsis => commodity as head
	7	0.3.3-ta	0.3.3=ta	0.3.3=ABL	6	nummod	

	# Jagersma, Chap. 8 (161)						
	# ‘one lamb (as an offering for) Enmetena’s statue’						
	# (ITT 1:1081 rev 1; L; 22)						
	1	1	1	1	2	nummod	
	2	sila4	sila4	lamb	0	root	verbless => commodity is head
	3	alan	alan	statue	2	DAT	implicit recipient
	4	en-	en	lord	3	GEN	
	5	me-te-na	ní.te=ane=ak	self=his=GEN=GEN	4	GEN	

Note that commodities in a broader sense can also include people. Annotate like commodity in the absence of other commodities.

	# Jagersma, Chap. 9 (27)						
	# ‘(three labourers) for four months and fifteen days; its (total number of) labourers: 405 for one day’						
	# (TMHC NF 1/2:293 6-7; N; 21)						
	1	iti	iti.d	month	6	TERM	marked on 4
	2	4	4	4	1	nummod	
	3	u4	u4.d	day	1	appos	implicit conjunction
	4	15-šè	15=še	15=TERM	3	nummod	
	6	ĝuruš-bé	ĝuruš=be	labourer=its	0	root	
	7	405	405	405	6	nummod	
	8	u4	u4.d	day	6	TERM	laborers are the "commodity" here
	9	1-šè	1=še	1=TERM	8	nummod	

In transactions with morphologically marked (or annotated) copular predicate, this is the head (not the commodity)

	# Jagersma, Chap. 9 (36)						
	# ‘Fifteen rams: this is income of the second day (lit. “day two”); seven rams: this is of the third (lit. “day three”).’						
	# (CTMMA I 8 1-2; D; 21)						
	1	15	15	15	2	nummod	
	2	udu	udu	ram	3	ABS	morphologically unmarked
	3	mu-DU	mu.DU.r	income	0	root	copular predicate; this is head because of explicit copula
	4	u4	u4.d	day	3	GEN	
	5	2-kam	min=ak='am	two=GEN=be:3N.S	4	nummod	
	7	7	7	7	8	nummod	
	8	udu	udu	ram	9	ABS	
	9	u4	u4.d	day	3	parataxis	
	10	3-kam	eš=ak='am	three=GEN=be:3N.S	9	GEN	

	# Jagersma, Chap. 9 (52)						
	# ‘three pounds of copper: it is of two shekels of silver.’						
	# (RA 73 p.1-22 2:1-2; I; 24)						
	1	3	eš	three	2	nummod	
	2	uruda	uruda	copper	6	ABS	
	3	ma-na	ma.na	pound	2	appos	
	5	2	min	two	6	nummod	
	6	kù	kù.g	silver	0	root	morphologically marked copula
	7	giĝ4-kam	giĝ4=ak='am	shekel=GEN=be:3N.S	6	appos	

	# Jagersma, Chap. 9 (53)					
	# ‘Its furrows are 25 (in number).’					
	# (DP 395 1:7; L; 24)					
	1	absin3-bé	absin3=be=Ø	furrow=its=ABS	2	ABS
	2	25-am6	25=Ø='am	25=ABS=be:3N.S	0	root
	
TBC: is that systematically applied and recognizable from MTAAC morphology?
	
"graded commodities":
In order to arrive at principled annotation in case of multiple (potential) commodities, assume the following preference:

	typical product > unit or amount representing a typical product > commodities in a broader sense (labour, people) > "currency" (i.e., silver)
	
	# Jagersma, Chap. 9 (39)						
	# ‘with two pounds of wool per (lit. “in one”) shekel of silver’						
	# (Nik 1:300 3:4-4:1; L; 24)						
	1	kù	kù.g	silver	5	LOC	
	2	giĝ4	giĝ4	shekel	1	appos	unit
	3	1-a	diš='a	one=LOC	2	nummod	
	5	siki	siki	wool	0	ABL	the commodity is the wool, the silver is the (equivalent of) currency
	6	ma-na	ma.na	pound	5	appos	
	7	2-ta	min=ta	two=ABL	6	nummod	

	# Jagersma, Chap. 9 (42)						
	# ‘with five hides per (lit. “in”) two shekels of silver’						
	# (Nik 1:230 5:2-3; L; 24)						
	1	kù	kù.g	silver	5	LOC	
	2	giĝ4	giĝ4	shekel	1	appos	unit
	3	2-a	min='a	two=LOC	2	nummod	
	5	kuš	kuš	hide	0	root	
	6	5-ta	ja=ta	five=ABL	5	nummod	

	# Jagersma, Chap. 9 (54)						
	# ‘Three hundred pairs of shoes: its bull’s hides are thirty (in number).’						
	# (TuT 83 1-2; L; 21)						
	1	300	300	300	2	nummod	
	2	kuše-sír	e.sír	shoe	0	root	commodity => head
	3	é-ba-an	é-ba-an	pair	2	appos	unit
	5	kuš	kuš	hide	7	ABS	
	6	gu4-bé	gu4.r=ak=be=Ø	bull=GEN=its=ABS	5	GEN	
	7	30-àm	30=Ø='am	30=ABS=be:3N.S	2	parataxis	in accordance with translation

	# Jagersma, Chap. 9 (55)						
	# ‘540 bundles of reed; with 36 (bundles) in each of its bales: its bales are 15 (in number).’						
	# (BAOM 2 p. 39:116 1-3; U; 21)						
	1	540	540	540	2	nummod	
	2	sa	sa	bundle	3	nmod	unit
	3	ge	ge	reed	0	root	
	5	gu-niĝin2-ba	gu.niĝin2=be='a	bale=its=LOC	9	LOC	
	6	36-ta	36=ta	36=ABL	9	nummod	
	8	gu-niĝin2-bé	gu.niĝin2=be=Ø	bale=its=ABS	9	ABS	
	9	15-àm	15=Ø='am	15=ABS=be:3N.S	3	parataxis	according to translation

	
These preferences are overridden by explicit or annotated morphology:
	
	# Jagersma, Chap. 9 (45)						
	# ‘one-third of a pound and three shekels of silver (as payment) for damaged fleeces’						
	# (Nik 1:295 1:1; L; 24)						
	1	⅓ša	šuššana	one.third	2	nummod	
	2	giĝ4	giĝ4	shekel	0	root	currency, not commodity, but morphological analysis emphasizes that the commodity is adnominal, hence head
	3	3	eš	three	4	nummod	
	4	kù	kù.g	silver	2	appos	implicit conjunction
	5	bar	bar	fleece	2	GEN	this is the more likely commodity, but we follow the annotated morphology
	6	dúb-ba	dúb-Ø-'a=ak	damage-NFIN-NOM=GEN	5	amod	


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

There are two principal possibilities to analyze the internal structure of functional dependents with nominal "function words": as `nmod` in accordance with the epithet rule, or as head.

Possible `nmod` analysis of *giri3 XY "gave"*

	[giri3 -nmod-> XY] -obl-> "gave"

However, the epithet analysis is inconsistent with cases in which explicit morphology is provided. For *giri3*, the agent (*XY*) can be marked as genitive:

	[giri3 <-GEN- XY.GEN] -obl-> "gave"

Analysis of functional dependents should follow examples where explicit morphology is provided, e.g., for *ki* "from"

	# Jagersma, Chap. 6 (18)					
	# ‘from the slave women’					
	# (MVN 22:273 obv 2; L; 21)					
	1	ki	ki	place	0	ABL
	2	geme2-ne-ta	geme2=enē=ak=ta	slave.woman=PL=GEN=ABL	1	GEN

	# Jagersma, Chap. 7 (271)					
	# ‘This was raised from Ur-Ishtaran.’					
	# (OSP 1:71 9-10; N; 24)					
	1	ki	ki	place	4	ABL
	2	ur-dištaran-ta	ur.ištaran=ak=ta	Urishtaran=GEN=ABL	1	GEN
	4	ab-ta-zi	'a-b-ta-zi.g-Ø	VP-3N-from-rise-3N.S/DO	0	root

cf. *szag*+ABL "out of"

	# Jagersma, Chap. 19 (70)					
	# ‘when he had taken his hand out of the midst of 216000 men’					
	# (St B 3:10-11; L; 22)					
	1	šà	šà.g	heart	6	ABL
	2	lú	lú	man	1	GEN
	3	216000-ta	216000=ak=ta	216000=GEN=ABL	2	nummod
	5	šu-né	šu=ane=Ø	hand=his=ABS	6	ABS
	6	ba-ta-an-dab5-ba-a	Ø-ba-ta-n-dab5-Ø-'a='a	VP-MM-from-3SG.A-take-3N.S/DO-NOM=LOC	0	acl+LOC

*szag*+LOC "in, among"

	# Jagersma, Chap. 7 (18)					
	# ‘in the middle of that year’					
	# (Ukg.4 12:29; L; 24)					
	1	šà	šà.g	heart	0	LOC
	2	mu-ba-ka	mu=be=ak='a	year=its=GEN=LOC	1	GEN

	# Jagersma, Chap. 9 (5)					
	# ‘among forty sealed documents’					
	# (AUCT 3:153 2; D; 21)					
	1	šà	šà.g	heart	0	LOC
	2	kišib	kišib	seal	1	GEN
	3	40-na	nimin=ak	forty=GEN	2	nummod


tbc: case of szag in the following

	# Jagersma, Chap. 24 (117)						
	# ‘They are men taken captive and in the guardhouse.’						
	# (DAS 206 17; L; 21)						
	1	lú	lú	man	3	ABS	different from Jagersma's gloss: The men taken captive are in the guardhouse
	2	al-dab5-ba	'a-dab5-Ø-'a	VP-take-3N.S/DO-NOM	1	amod	
	3	šà	šà.g	heart	0	root	case (?ABS, ?ABL) => copular predicate
	4	en-nu-me	en.nu.ĝ=ak=Ø=me-eš	guard=GEN=ABS=be-3PL.S	3	GEN	



TO BE CONFIRMED: This means that the epithet analysis is to be avoided in such cases.
TODO: list all possible functional dependents, along with explicit examples, if possible.

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

If no verb is provided, mark suppliers as ERG, receivers as DAT and commodities as ABS. This corresponds to the verbal frame of "give":


"give": 
	ERG supplier
	DAT recipient
	TERM manner (as price)
	ABS commodity
	ABL source
	DIR target (?)

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

	# Jagersma, Chap. 7 (236)					
	# ‘As the price for him (= a slave) she gave her ... (= various items).’					
	# (RTC 17 2:4-3:1; L; 24)					
	1	níĝ-sám-ma-né-šè	níĝ.sám.ma=ane=še	price=his=TERM	5	TERM
	3	(...)	(...)=Ø	(...)=ABS	5	ABS
	5	e-na-šúm	'i-nna-n-šúm-Ø	VP-3SG.IO-3SG.A-give-3N.S/DO	0	root


	# Jagersma, Chap. 6 (60)					
	# ‘PN2, wife of PN3, the king of Lagash, gave this from the palace to PN1, the chief merchant.’					
	# (VS 14:43 3:3-4:4; L; 24)					
	1	PN1	PN1	PN1	16	DAT
	3	gal-dam-gara3	gal.dam.gara3=r(a)	merchant.in.chief=DAT	1	appos
	5	PN2	PN2	PN2	16	ERG
	7	dam	dam	wife	5	appos
	8	PN3	PN3	PN3	7	GEN
	10	lugal	lugal	king	8	appos
	12	lagas{ki}-ka-ke4	lagas=ak=ak=e	Lagash=GEN=GEN=ERG	10	GEN
	14	é-gal-ta	é.gal=ta	palace=ABL	16	ABL
	16	e-na-šúm	'i-nna-n-šúm-Ø	VP-3SG.IO-3SG.A-give-3N.S/DO	0	root
	
	# Jagersma, Chap. 7 (136)					
	# ‘The Ummaite set fire to the border dike. He set fire to the Antasurra.’					
	# (Ukg. 16 1:1-5; L; 24)					
	1	lú	lú	man	8	ERG
	2	ummaki-ke4	umma=ak=e	Umma=GEN=ERG	1	GEN
	4	e	e.g	dike	8	DIR
	5	ki-surx(ERIM)-ra-ke4	ki.sur.ra=ak=e	border=GEN=DIR	4	GEN
	7	izi	izi=Ø	fire=ABS	8	ABS
	8	ba-šúm	Ø-ba-n-šúm-Ø	VP-3N.IO-3SG.A-give-3N.S/DO	0	root
	10	an-ta-sur-ra	an.ta.sur.ra=e	Antasurra=DIR	13	DIR
	12	izi	izi=Ø	fire=ABS	13	ABS
	13	ba-šúm	Ø-ba-n-šúm-Ø	VP-3N.IO-3SG.A-give-3N.S/DO	8	parataxis

	# Jagersma, Chap. 8 (15)						
	# ‘By the king’s life, I, myself, gave Abbakalla to Urmes.’						
	# (TCS 1:81 3-7; L; 21)						
	1	ab-ba-kal-la	ab.ba.kal.la=Ø	Abbakalla=ABS	10	ABS	
	3	ur-mes-ra	ur.mes=ra	Urmes=DAT	10	DAT	
	5	zi	zi	life	10	???	? case
	6	lugal	lugal=ak	king=GEN	1	GEN	
	8	ĝe26-e-me	ĝe26=Ø=me-en	I=ABS=be-1SG.S	10	ERG	sic!
	10	ha-na-šúm	ha='i-nna-'-šúm-Ø	MOD=VP-3SG.IO-1SG.A-give-3N.S/DO	0	root	

TODO: compare with other explicit verbs of supply and reception:

verbs of transfer

"receive": 
	ERG receiver
	ABS commodity
	TERM manner
	ki+ABL supplier

	# Jagersma, Chap. 6 (3)					
	# ‘Beli-arik and Urnigingar received this.’					
	# (PIOL 19:278 8-10; D; 21)					
	1	be-lí-a-rí-ik	be.lí.a.rí.ik	Beliarik	6	ERG
	3	ù	ù	and	1	cc
	4	ur-nigin3-ĝar-ke4	ur.nigin3.ĝar.k=e	Urnigingar=ERG	1	conj
	5	šu	šu=e	hand=DIR	6	DIR
	6	ba-an-ti-éš	Ø-ba-n-ti-eš	VP-3N.IO-3SG.A-approach-3PL	0	root

	# Jagersma, Chap. 6 (4)					
	# ‘Beli-arik and Urnigingar received this.’					
	# (BIN 3:611 8-10; D; 21)					
	1	be-lí-a-rí-ik	be.lí.a.rí.ik	Beliarik	7	ERG
	3	ù	ù	and	1	cc
	4	ur-nigin3-ĝar	ur.nigin3.ĝar.k=e	Urnigingar=ERG	1	conj
	6	šu	šu=e	hand=DIR	7	DIR
	7	ba-ab-ti	Ø-ba-b-ti-Ø	VP-3N.IO-3N.A-approach-3N.S/DO	0	root

	# Jagersma, Chap. 7 (233)					
	# ‘Urdukuga received from Ur-Suen two shekels of silver as a loan.’					
	# (NATN 422 1-5; N; 21)				
	1	2	2	2	2	nummod
	2	giĝ4	giĝ4	shekel	3	nmod
	3	kù-babbar	kù.babbar=Ø	silver=ABS	13	ABS
	5	ur5-šè	ur5=še	loan=TERM	13	TERM
	7	ki	ki	place	13	ABL
	8	ur-dsuen-ta	ur.suen=ak=ta	Ursuen=GEN=ABL	7	GEN
	10	ur-du6-kù-ga	ur.du6.kù.ga=e	Urdukuga=ERG	13	ERG
	12	šu	šu=e	hand=DIR	13	DIR
	13	ba-ti	Ø-ba-n-ti-Ø	VP-3N.IO-3SG.A-approach-3N.S/DO	13	root

pay (= place on [account])
	ABS theme [e.g. interest]
	LOC target [account]
	(ERG supplier)

	# Jagersma, Chap. 20 (91)					
	# ‘He will pay interest on this.’					
	# (NG 144 15; U; 21)					
	1	ugu4-ba	a.gù=be='a	top=its=LOC	3	LOC
	2	máš	máš=Ø	interest=ABS	3	ABS
	3	ì-íb-ĝá-ĝ[á]	'i-b(i)-ĝar:RDP-e	VP-3N:on-place:IPFV-3SG.A:IPFV	0	root

cf. place on:
	ABS theme
	LOC target
	(ERG: supplier)
		
	# Jagersma, Chap. 25 (114)					
	# ‘I will put Ea's ox in its place!’					
	# (TCS 1:58 7-8; L; 21)					
	1	gu4	gu4.ř	ox	5	ABS
	2	e-a-a	e.a'=ak=Ø	Ea=GEN=ABS	1	GEN
	4	ki-ba	ki=be='a	place=its=LOC	5	LOC
	5	ga-ra-a-ĝá-ar	ga-ra-e-ĝar	MOD:1SG.A/S-2SG.IO-on-place	0	root

give:
	ABS theme (thing given)
	ERG supplier
	DAT receiver
	
	# Jagersma, Chap. 27 (135)						
	# ‘Six gurs of apples, worth five shekels of silver: Dalu and Ur-Ab'u gave this to Ur-Shara, the merchant, before one could estimate it.’						
	# (BM 105356 7-11; U; 21)						
	1	6	6	6	2	nummod	
	2	ĝišhašhur	hašhur	apple	18	ABS	???
	3	gur	gur	gur	2	appos	
	5	kù-bé	kù.g=be	silver=its	2	appos	
	6	5	5	5	7	nummod	
	7	giĝ4	giĝ4	shekel	5	appos	
	9	káb	káb=Ø	?=ABS	10	ABS	
	10	nu-ub-da-ab-du11-ga-aš	nu='i-b-da-b-du11.g-Ø-'a=še	NEG=VP-3N-with-3N.A-do-3N.S/DO-NOM=TERM		acl+TERM	
	12	da-lu5	da.lu5	Dalu	18	ERG	
	13	ù	'ù	and	12	cc	
	14	ur-dab-ú-ke4	ur.ab.ú.k=e	Urab'u=ERG	12	conj	
	16	ur-dšara2	ur.šara2	Urshara	18	DAT	
	17	dam-[ga]ra3	dam.gara3=r(a)	merchant=DAT	16	appos	
	18	in-na-šúm	'i-nna-b-šúm-Ø	VP-3SG.IO-3N.A-give-3N.S/DO	0	root	

	# Jagersma, Chap. 13 (25)					
	# ‘King Enki gave an oracle for it.’					
	# (Cyl B 4:3; L; 22)					
	1	lugal	lugal	king	2	nmod
	2	den-ki-ke4	en.ki.k=e	Enki=ERG	4	ERG
	3	eš-bar-kíĝ	eš.bar.kíĝ=Ø	oracle=ABS	4	ABS
	4	ba-an-šúm	Ø-ba-n-šúm-Ø	VP-3N.IO-3SG.A-give-3N.S/DO	0	root


take:
	ABS theme (thing taken)
	ERG receiver
	ABL source

	# Jagersma, Chap. 6 (23)					
	# ‘barley rations of the persons holding a subsistence field’					
	# Jagersma, Chap. 6 (e.g., DP 154 1:2; L; 24)					
	1	še-ba	še.ba	ration.barley	0	root
	2	lú	lú	man	1	GEN
	3	šuku	šuku.ř=Ø	subsistence=ABS	4	ABS
	4	dab5-ba-ne	dab5-Ø-'a=enē=ak	take-NFIN-NOM=PL=GEN	2	acl

	# Jagersma, Chap. 6 (33)					
	# ‘The fatteners took them.’					
	# (BCT 1:119 13; D; 21)					
	1	gurušta-e	gurušta=e	fattener=ERG	2	ERG
	2	íb-dab5	'i-b-dab5-Ø	VP-3N.A-take-3N.S/DO	0	root

	# Jagersma, Chap. 7 (103)					
	# ‘Donkeys were seized by the shepherd.’					
	# (Ukg. 4 3:7-8; L; 24)					
	1	anše	anše=Ø	donkey=ABS	4	ABS
	2	ú-du-le	ú.du.l=e	shepherd=ERG	4	ERG
	4	e-dab5	'i-n-dab5-Ø	VP-3SG.A-take-3N.S/DO	0	root

	# Jagersma, Chap. 7 (174)					
	# ‘In those days, the chief bargee took charge of the boats.’					
	# (Ukg. 4 3:4-6; L; 24)					
	1	u4-bé-a	u4.d=be='a	day=its=LOC	7	LOC
	3	lú	lú	man	7	ERG
	4	má-lah5-ke4	má.lah5.d=ak=e	boatman=GEN=ERG	3	GEN
	6	má	má=Ø	boat=ABS	7	ABS
	7	e-dab5	'i-n-dab5-Ø	VP-3SG.A-take-3N.S/DO	0	root

	# Jagersma, Chap. 13 (29a)					
	# ‘when he had taken his hand from among 216000 men’					
	# (St B 3:10-11; L; 22)					
	1	šà	šà.g	heart	6	ABL
	2	lú	lú	man	1	GEN
	3	216000-ta	216000=ta	216000=ABL	2	nummod
	5	šu-né	šu=ane=Ø	hand=his=ABS	6	ABS
	6	ba-ta-an-dab5-ba-a	Ø-ba-ta-n-dab5-Ø-'a='a	VP-MM-from-3SG.A-take-3N.S/DO-NOM=LOC	0	root

put on
	ABS theme (thing given)
	LOC target (receiver)
	?ERG agent (supplier)
	
	# Jagersma, Chap. 7 (175)					
	# ‘This silver was put on their hands.’					
	# (TMTIM 61 7-8; ?; 23)					
	1	kù-bé	kù.g=be=Ø	silver=this=ABS	4	ABS
	2	šu-ne-ne-a	šu=anēnē='a	hand=their=LOC	4	LOC
	4	ab-si	'a-b(i)-si.g-Ø	VP-3N:on-put-3N.S/DO	0	root

put into
	ABL quantity
	ABS thing put into
	(ERG supplier)

	# Jagersma, Chap. 20 (4a)					
	# ‘Fifteen baskets of (one ba-rí-ga=) sixty litres each: dates were put into them.’					
	#	(MVN 16 Um. 1677 obv 1-2; U; 21).				
	1	15	15	15	2	nummod
	2	gegur-dub	gur.dub	basket	6	ABL
	3	0.1.0-ta	0.1.0=ta	1=ABL	2	nommod
	4	/	_	_	6	punct
	5	zú-lum	zú.lum=Ø	dates=ABS	6	ABS
	6	ba-an-si	Ø-ba-n(i)-si.g-Ø	VP-MM-in-put-3N.S/DO	0	root

buy (barter towards)	
	ABS theme (thing bought)
	TERM(1) price
	TERM(1) supplier (seller)
	ERG receiver (buyer)

	# Jagersma, Chap. 7 (248)					
	# ‘One male slave Abbagena bought from (lit. “bartered towards”) Lu-Nanna (in ex- change) for five shekels of silver.’					
	# (FAOS 17:94*** 1-5; U; 21)					
	1	1	1	1	2	nummod
	2	saĝ-nita2	saĝ.nita2=Ø	male.slave=ABS	12	ABS
	4	kù	kù.g	silver	12	TERM
	5	5	5	5	6	nummod
	6	giĝ4-šè	giĝ4=še	shekel=TERM	4	appos
	8	lú-dnanna-šè	lú.nanna=še	Lunanna=TERM	12	TERM
	10	ab-ba-ge-na-a	ab.ba.ge.na=e	Abbagena=ERG	12	ERG
	12	in-ši-sa10	'i-n-ši-n-sa10-Ø	VP-3SG-to-3SG.A-barter-3SG.S/DO	12	root

send (turn)
	ERG sender
	ABS theme (people sent)
	DAT goal (receiver)

	# Jagersma, Chap. 13 (71b)					
	# ‘Let him send PN1, PN2, and twenty gardeners here with it!’					
	# (TCS 1:56 5-8; U; 21)					
	1	PN1	PN1	PN1	10	ABS
	3	PN2	PN2	PN2	1	conj
	5	ù	ù	and	1	cc
	6	20	20	20	7	nummod
	7	ĝuruš	ĝuruš	man	1	conj
	8	nu-ĝiškiri6	nu.kiri6=Ø	gardener=ABS	7	appos
	10	hé-em-da-ab-gi4-gi4	ha=Ø-mu-nnē-gi4:RDP-e	MOD=VP-VENT-3PL.DO-turn:IPFV-3SG.A:IPFV	0	root
	
	# Jagersma, Chap. 15 (8)					
	# ‘He should send me a driver!’					
	# (MVN 11:168 18; U; 21)					
	1	lú-ús	lú.ús=Ø	follower=ABS	3	ABS
	2	ĝá-ar	ĝe26=r(a)	I=DAT	3	DAT
	3	ha-mu-ši-in-gi4-gi4	ha=Ø-mu-'-ši-n-gi4:RDP-e	MOD=VP-VENT-1SG-to-3SG.DO-turn:IPFV-3SG.A:IPFV	0	root
	
bring
	ABS theme (thing brought)
	ERG agent (supplier)
	TERM(1) amount
	ABL/LOC source
	TERM(2) goal
	
	# Jagersma, Chap. 9 (90)					
	# ‘(barley) that was taken out of Girsu as one-sixtieth’					
	# (BM 15308 1:4; L; 21)					
	1	igi-60-ĝál-šè	igi.ĝešd.ĝál=še	one.sixtieth=TERM	3	TERM
	2	ĝír-suki-ta	ĝír.su=ta	Girsu=ABL	3	ABL
	3	ře6-a	ře6-Ø-'a	bring-NFIN-NOM	0	acl

	# Jagersma, Chap. 13 (23)					
	# ‘4 labourers for 10 days: they brought straw from KI.AN to Umma.’					
	# (TENS 205 1-3; U; 21)					
	1	4	4	4	2	nummod
	2	ĝuruš	ĝuruš	labourer	0	root
	3	u4	u4.d	day	10	TERM
	4	10-šè	10=še	10=TERM	3	nummod
	6	KI.ANki-ta	KI.AN=ta	KI.AN=ABL	10	ABL
	7	ummaki-<šè>	umma=še	Umma=TERM	10	TERM
	9	in-u	in.u=Ø	straw=ABS	10	ABS
	10	ì-im-ře6	'i-m(u)-ře6-Ø	VP-VENT-bring-3N.S/DO	2	parataxis
	
	# Jagersma, Chap. 13 (31a)					
	# ‘because he had not brought this fish to the palace’					
	# (NG 189 7; U; 21)					
	1	mu	mu	name	0	TERM
	2	ku6-bé	ku6=be=Ø	fish=this=ABS	4	ABS
	3	é-gal-šè	é.gal=še	palace=TERM	4	TERM
	4	nu-mu-un-ře6-a-šè	nu=Ø-mu-n-ře6-Ø-'a=ak=še	NEG=VP-VENT-3SG.A-bring-3N.S/DO-NOM=GEN=TERM	1	acl+GEN

	# Jagersma, Chap. 13 (31b)					
	# ‘This is wood that Ursag brought from the forest of Abbar.’					
	# (DP 442 1:3-2:1; L; 24)					
	1	ĝiš	ĝiš	wood	0	root
	2	tir	tir	forest	7	ABL
	3	abbarki-ta	abbar=ak=ta	Abbar=GEN=ABL	2	GEN
	5	ur-saĝ-ĝe26	ur.saĝ=e	Ursag=ERG	7	ERG
	7	mu-ře6-a-am6	Ø-mu-n-ře6-Ø-'a=Ø='am	VP-VENT-3SG.A-bring-3N.S/DO-NOM=ABS=be:3N.S	1	acl

	# Jagersma, Chap. 15 (90)					
	# ‘Who has taken away the Anzu-bird from its nest? (=The bird is now gone)’					
	# (Lugalbanda II 89 manuscript AA; OB)					
	1	anzumušen	anzu.d=Ø	Anzu=ABS	4	ABS
	2	gùd-ba	gùd=be='a	nest=its=LOC	4	LOC
	3	a-ba	a.ba=e	who=ERG	4	ERG
	4	<ba>-ra-an-tùm	Ø-ba-ta-n-tùm-Ø	VP-MM-from-3SG.A-bring:IPFV-3N.S/DO	0	root

take away
	ABS theme (thing taken)
	COM source
	ERG agent (taker)

	# Jagersma, Chap. 19 (19)					
	# ‘Nobody takes away its fish.’					
	# (Ukg. 6 3:9'; L; 24)					
	1	ku6-bé	ku6=be=Ø	fish=its=ABS	3	ABS
	2	lú	lú=e	man=ERG	3	ERG
	3	nu-ba-dab6-kar-re	nu=Ø-ba-da-b-kar-e	NEG=VP-MM-with-3N.DO-take.away-3SG.A:IPFV	0	root

	# Jagersma, Chap. 19 (45)					
	# ‘Three ban of barley seed was taken away from the slave of PN, the farmer.’					
	# (OrSP 47/49:502 9-10; U; 21)					
	1	0.0.3	0.0.3	3.ban	2	nummod
	2	še-numun	še.numun=Ø	seed.barley=ABS	7	ABS
	3	urdu2	urdu2.d	slave	7	COM
	4	PN	PN	PN	3	GEN
	6	engar-da	engar=ak=da	farmer=GEN=COM	4	appos
	7	ba-an-da-kar	Ø-ba-n-da-kar-Ø	VP-MM-3SG-with-take.away-3N.S/DO	7	root

supply (from place)
	ERG supplier
	ABL source
	(ABS supplied thing)

	# Jagersma, Chap. 7 (95)					
	# ‘Shulme the steward supplied this from the palace.’					
	# (DP 512 4:1-4; L; 24)					
	1	šul-me	šul.me	Shulme	7	ERG
	3	agrig-ge	agrig=e	steward=ERG	1	appos
	5	é-gal-ta	é.gal=ta	palace=ABL	7	ABL
	7	e-ta-ĝar	'i-b-ta-n-ĝar-Ø	VP-3N-from-3SG.A-place-3N.S/DO	0	root

### Multiple agents in a transaction

When we have not only one obl in different roles, we use not use `conj` to link them together, but treat them as independent arguments. E.g., in

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

Do not annotate "emphatic" copula as copula if it serves as a nominal argument.

	# Jagersma, Chap. 24 (22)						
	# ‘When someone divorced his wife, the ruler took five shekels of silver for himself.’						
	# (Ukg. 6 2:15'-18'; L; 24)						
	1	lú	lú=e	man=ERG	3	ERG	
	2	dam	dam=Ø	wife=ABS	3	ABS	
	3	ù-taka4	'u-n-taka4-Ø	REL.PAST-3SG.A-leave-3N.S/DO	11	advcl	
	4	/	_	_	11	punct	
	5	kù	kù.g	silver	6	nmod	unit
	6	giĝ4	giĝ4	shekel	11	ABS	we consider copula as emphatic and ignore for annotation
	7	5-am6	5=Ø='am	5=ABS=be:3N.S	6	nummod	
	8	/	_	_	11	punct	
	9	ensi2-ke4	ensi2.k=e	ruler=ERG	11	ERG	
	10	/	_	_	11	punct	
	11	ba-ře6	Ø-ba-n-ře6-Ø	VP-MM-3SG.A-bring-3N.S/DO	0	root	

Instead, such examples are interpreted as "emphatic copula"/"standard marker" ("STM"), basically like a focus particle.

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

If an argument marked by emphatic copula can also be analyzed as an independent clause (i.e., it is the first argument of the matrix clause), analyse it as such (in accordance with the morphology)

	# Jagersma, Chap. 8 (26)					
	# ‘I, the shepherd, (lit. “(I) who am the shepherd”) have built the temple.’					
	# (Cyl B 2:5; L; 22)					
	1	sipa-me	sipa.d=Ø=me-en	shepherd=ABS=be-1SG.S	0	root
	2	é	é=Ø	house=ABS	3	ABS
	3	mu-řú	Ø-mu-'-řú-Ø	VP-VENT-1SG.A-erect-3N.S/DO	1	parataxis

	# Jagersma, Chap. 8 (87)					
	# (Two brothers sell their sister as a slave. If she stops working) ‘it is they who shall be slaves.’					
	# (FAOS 17:45 10; N; 21)					
	1	ne-me	nēn=Ø=me-eš	this=ABS=be-3PL.S	0	root
	2	urdu2	urdu2.d=Ø	slave=ABS	3	ABS
	3	ha-me	ha='i-me-eš	MOD=VP-be-3PL.S	1	parataxis


otherwise, annotate the syntatically expected case (against the morphology)
	
	# Jagersma, Chap. 8 (15)						
	# ‘By the king’s life, I, myself, gave Abbakalla to Urmes.’						
	# (TCS 1:81 3-7; L; 21)						
	1	ab-ba-kal-la	ab.ba.kal.la=Ø	Abbakalla=ABS	10	ABS	
	3	ur-mes-ra	ur.mes=ra	Urmes=DAT	10	DAT	
	5	zi	zi	life	10	???	? case
	6	lugal	lugal=ak	king=GEN	1	GEN	
	8	ĝe26-e-me	ĝe26=Ø=me-en	I=ABS=be-1SG.S	10	ERG	sic!
	10	ha-na-šúm	ha='i-nna-'-šúm-Ø	MOD=VP-3SG.IO-1SG.A-give-3N.S/DO	0	root	

### Negation with *nu*

Negation is normally expressed with a proclitic, but occasionally, it appears as individual word. Jagersma (2010, p.717) hints at the possibility that these may be analysed as `cop`, but then the relation between the copular clause and the following relative clause that modifies its predicate (as well as the relation between both copular clauses) is unclear.

	# Jagersma, Chap. 6 (11)					
	# ‘NOT PN1, the farmer; NOT PN2, the farmer: the barley of their subsistence-fields not to be given’					
	# (ASJ 9 p.334:9 1-3; L; 21)					
	1	nu	nu	NEG	2	cop	?
	2	PN1	PN1	PN1	0	root
	3	engar	engar	farmer	2	appos
	5	n[u]	nu	NEG	6	cop	?
	6	PN2	PN2	PN2	2	parataxis	?
	7	engar	engar	farmer	6	appos
	9	še	še	barley	11	ABS
	10	šuku-ba	šuku.r=be=ak=Ø	subsistence=its=GEN=ABS	9	GEN
	11	nu-šúm-mu	nu=šúm-ed-Ø	NEG=give-IPFV-NFIN	2	acl

For the annotation of the relative clause, cf. an example with a numeral:

	# Jagersma, Chap. 6 (10)					
	# ‘1 PN, the farmer: the barley of his subsistence-field not to be given’					
	# (ASJ 9 p.334:9 7; L;21)					
	1	1	1	1	2	nummod
	2	PN	PN	PN	0	root
	3	engar	engar	farmer	2	appos
	4	še	še	barley	6	ABS
	5	šuku-ra-na	šuku.r=ane=ak=Ø	subsistence=his=GEN=ABS	4	GEN
	6	nu-šúm-mu	nu=šúm-ed-Ø	NEG=give-IPFV-NFIN	2	acl

As the copula can be annotated as particle, a particle-based annotation for negation could be considered here. TODO: develop principled handling of such cases.

### Hard examples

Collect examples here that are not satisfactorily analyzed, yet.

#### "empty" numerals?

To check: what does 1 mean in the following gloss? Can that modify a proper name (in the sense of "one slave, Urnigdu", but with scrambled word order)? Or is that a replacement for, say, *ud4* "day (when)"?

	# Jagersma, Chap. 22 (15)					
	# ‘when you redeem Urnigdu, the slave, from Elu’					
	# (NG 28 9’; L; 21)					
	1	1	1	1	2	nummod
	2	úr-níĝ-du10	úr.níĝ.du10.g	Urnigdu	5	ABS
	3	urdu2	urdu2.d=Ø	slave=ABS	2	appos
	4	é-lú-ta	é.lú=ta	Elu=ABL	5	ABL
	5	ù-mu-duh	'u-mu-e-duh-Ø	REL.PAST-VENT-2SG.A-loosen-3N.S/DO	0	advcl

#### interrogatives with copula

parataxis or emphatic copula

	# Jagersma, Chap. 10 (85)						
	# ‘Why is it that you make things bigger than yourself? (lit. “big to your excess”)’						
	# (Two scribes: CT 42:47 2:7 // ISET 2 pl. 97 Ni. 4194 rev. 4; N; OB)						
	1	a-na-aš-àm	a.na=še='am	what=TERM=be:3N.S	0	root	TERM => copular predicate
	2	diri-zu-šè	diri.g=zu=še	excess=your=TERM	4	TERM	
	3	níĝ	níĝ=Ø	thing=ABS	4	ABS	
	4	ab-gur4-re-en	'a-b-gur4-en	VP-3N.DO-be.thick-2SG.A/S:IPFV	1	parataxis	


#### adverbial EQU?

	# Jagersma, Chap. 10 (50)						
	# ‘About that you are wide as the earth – let it be known!’						
	# (Inanna B 124; OB manuscript)						
	1	ki-gen7	ki=gen	earth=EQU	3	EQU	attachment?
	2	daĝal-la-za	daĝal-Ø-'a=zu='a	be.wide-NFIN-NOM=your=LOC	3	LOC	amod+LOC
	3	hé-zu-àm	ha='i-zu-Ø='am	MOD=VP-know-3N.S/DO=be:3N.S	0	root	

#### unmarked GEN+disloc 

in administrative texts -- if not `GEN+disloc`, how then?
	
	# Jagersma, Chap. 9 (96)					
	# ‘one and a quarter plot of house’					
	# (RTC 18 5:1-2; L; 24)					
	1	1	diš	one	3	nummod
	2	é	é	house	3	GEN+disloc
	3	šar	sar	plot	0	root
	5	igi-4-ĝál	igi.limmu.ĝál	one.fourth	3	nummod

#### annotating calculation tables:

	if equality with a sum is expressed, annotate as sum as predicate of (implicit) copula 

	# Jagersma, Chap. 9 (104)						
	# ‘Of sixty its half: thirty’						
	# (AfO 50 p.356 BM 106425 1; U; 21)						
	1	60-da	ĝešd=ak	sixty=GEN	3	GEN+disloc	
	2	igi-2-bé	igi.min=be	one.half=its	1	nummod	
	3	30	ušu	thirty	0	root	implicit copula

#### discontinuous spellings
	
	# Jagersma, Chap. 9 (115)					
	# ‘one-third of a pound and three shekels of silver’					
	# (BIN 8:37 1:1; N; 24)					
	1	šú	(šuššana)	(one.third)	?	?
	2	3	eš	three	3	nummod
	3	kù	kù.g	silver	0	root
	4	ša-na	šuššana	one.third	5	nummod
	5	giĝ4	giĝ4	shekel	3	nmod

	in this example, connecting szu with sza-na will produce a non-projective parse. Also, the label has to be confirmed.

#### adnominal non-genitives

	# Jagersma, Chap. 9 (48)					
	# ‘the interest a hundred litres in a gur’					
	# (AUCT 3:329 2; N; 21)					
	1	máš	máš	interest	0	root
	2	1	(diš)	(one)	1	nummod
	3	gur-ra	gur='a	gur=LOC	1	LOC
	4	0.1.4-ta	0.1.4=ta	100.litres=ABL	1	ABL

	# Jagersma, Chap. 9 (49)					
	# ‘its furrows: with twelve in a nindan (= ca. six metres)’					
	# (CT 1 pl. 12-13 BM 18041 4:11; L; 21)					
	1	ab-sín-bé	ab.sín=be	furrow=its	0	root
	2	1	1	1	1	nummod
	3	nindan-na	nindan='a	nindan=LOC	1	ABL
	4	12-ta	12=ta	12=ABL	3	nummod

#### discuss: ordinal numbers as `amod`?
	
	# Jagersma, Chap. 9 (62)						
	# ‘four ban(-units of barley for) Eku; four ban (for) Eku the second’						
	# (STH 1:23 3:13-15; L; 24)						
	1	0.0.4	_	_	0	root	numeral representing the (elided) commodity
	2	é-kù	_	_	1	DAT	
	4	0.0.4	_	_	1	parataxis	
	5	é-kù	_	_	4	DAT	
	7	2-kam-ma	_	_	5	amod	? nummod
							
	# Jagersma, Chap. 9 (63)						
	# ‘1 Urnigingar; 1 Urnigingar the second’						
	# (TCL 5:6036 2:12-13; U; 21)						
	1	1	_	_	0	root	
	2	ur-nigin3-ĝar	_	_	1	DAT	
	4	1	_	_	1	parataxis	
	5	ur-nigin3-ĝar	_	_	4	DAT	
	6	2-kam	_	_	5	amod	? nummod

but clearly not in

	# Jagersma, Chap. 9 (64)					
	# ‘for the third time’					
	# (PDT 1:502 8; D; 21)					
	1	a-řá	a.řá	time	0	TERM
	2	3-kam-ma-aš	eš-kamma=š(e)	three-ORD=TERM	1	nummod

	# Jagersma, Chap. 9 (65)					
	# ‘The second was a warrior.’					
	# (Cyl A 6:3; L; 22).					
	1	2-kam-ma	min-kamma=Ø	two-ORD=ABS	2	ABS
	2	ur-saĝ-àm	ur.saĝ=Ø='am	warrior=ABS=be:3SG.S	0	root

	# Jagersma, Chap. 9 (69)					
	# ‘third quality (lit. “the third which is next”)’					
	# (DP 382 1:3; L; 24)					
	1	3-kam-ma	eš-kamma	three-ORD	0	root
	2	ús	ús-Ø	be.next.to-NFIN	1	acl

#### clarify interaction between copula and case

	# Jagersma, Chap. 9 (8)					
	# ‘In this, there are five intercalary months. (Lit. “In its heart there are extra months which are five (in number).”)’					
	# (RA 9 p.158 obv 5; U; 21)					
	1	šà-ba	šà.g=be='a	heart=its=LOC	5	LOC
	2	iti	iti.d	month	5	ABS
	3	diri	diri.g	extra	2	amod
	4	5-àm	ja=Ø='am	five=ABS=be:3N.S	2	nummod
	5	ì-ĝál	'i-n(i)-ĝál-Ø	VP-in-be.there-3N.S/DO	0	root

	# Jagersma, Chap. 9 (10)					
	# ‘because his three sons were on duty for it’					
	# (MVN 6:293 3:9'; L; 21)					
	1	mu	mu	name	0	TERM
	2	dumu-né	dumu=ane	son=his	4	ABS
	3	3-àm	eš=Ø='am	three=ABS=be:3N.S	2	nummod
	4	ba-gub-ba-šè	Ø-ba-gub-Ø-'a=ak=še	VP-3N.IO-stand-3N.S/DO-NOM=GEN=TERM	1	acl+GEN


#### annotation of implicit copula

	# Jagersma, Chap. 8 (93)						
	# ‘This day is something beautiful.’						
	# (PN) (e.g., NG 193 25'; L; 21)						
	1	u4-	u4.d	day	0	root	
	2	ne-	nēn	this	1	appos	
	3	níĝ-	níĝ	thing	1	appos	implicit copula?
	4	sa6-ga	sa6.g-Ø-'a	be.beautiful-NFIN-NOM	3	amod	

Appositional analysis seems to be Jagersma's preferred analysis here. For an annotation as implicit copula, we would expect an annotation for ABS on 1.

#### multiple copula

Annotating the functional head rather than the morphological head of copula clauses can produce complicated structures.
	
`a-ba me-a` : morphological head is (the copula) *me-a*, functional head is *a-ba-*
`a-ba me-a nu`: morphological head is (the negative copula) *nu*, functional head is *a-ba-*
`a-ba me-a nu a-ba me-a-né`: morphological head is *nu*, functional head is *a-ba-*

	# Jagersma, Chap. 8 (116)					
	# ‘whoever she is not, whoever she is.’					
	# (Cyl A 4:23; L; 22)					
	1	a-ba-	a.ba=Ø	who=ABS	0	DIR
	2	me-a	'i-me-Ø-'a=Ø	VP-be-3SG.S-NOM=ABS	1	cop
	3	nu	nu	NEG	1	cop
	4	a-ba-	a.ba=Ø	who=ABS	1	acl
	5	me-a-né	'i-me-Ø-'a=ane=e	VP-be-3SG.S-NOM=her=DIR	4	cop

the logic is clearer from the phrase structure:
	
	(        # empty head (headless clause) => head stays on 1
	 (       # clause; syntactic head: NEG/cop => annotate 1
	  (      # nominalized, head stays
	   (     # clause; syntactic head: cop   => annotate 1
		  who=ABS
		  VP-be-3SG.S ) # cop, end of "who is"
		 –NOM         ) # relative clause, end of "that who is"
		 =ABS           # abs argument of "is not"
		  NEG         ) # neg. cop, end of "that who is is not"
	 (       # relative clause => depends on head of preceding clause
	  (      # clause; syntactic head: cop   => annotate 4
		  who=ABS
		  VP-be-3SG.S ) # cop, end of "who is"
		 -NOM         ) # end of relative clause "that who is"
		 =her           # assume that this takes scope over both sentences [i.e., the first]
		 =DIR         ) # DIR is the case of the empty head

so, DIR of 1 marked on 5; cases of copular predicates dropped: 1 marked ABS of 2 [but that is non-head]; 2 marked ABS of 3 [but that is non-head]; 

#### postposed ABS

That should not exist. Theoretically, these could always be analysed as predicates of an implicit copula. However, the following example employs an explicit (emphatic?) copula along with such an "implicit" (?) copula:

	# Jagersma, Chap. 8 (85)					
	# ‘(Referring to various plants, Enki says:) “What is this?”’					
	# (ENh 199; OB)					
	1	a-na-àm	a.na=Ø='am	what=ABS=be:3N.S	0	root
	2	ne-e	nēn=Ø	this=ABS	1	ABS

#### *zi lugal* "by the king's life"

Jagersma (2010) never provides an interpretation of the phrase. If first element of a clause, it can be considered an elliptical clause, but this does not seem to be possible for the following case:

	# Jagersma, Chap. 8 (15)						
	# ‘By the king’s life, I, myself, gave Abbakalla to Urmes.’						
	# (TCS 1:81 3-7; L; 21)						
	1	ab-ba-kal-la	ab.ba.kal.la=Ø	Abbakalla=ABS	10	ABS	
	3	ur-mes-ra	ur.mes=ra	Urmes=DAT	10	DAT	
	5	zi	zi	life	10	???	? case
	6	lugal	lugal=ak	king=GEN	1	GEN	
	8	ĝe26-e-me	ĝe26=Ø=me-en	I=ABS=be-1SG.S	10	ERG	sic!
	10	ha-na-šúm	ha='i-nna-'-šúm-Ø	MOD=VP-3SG.IO-1SG.A-give-3N.S/DO	0	root	
	
#### nested acls
	
	# Jagersma, Chap. 8 (23)						
	# ‘because they are persons of the ... plain’						
	# (JAOS 103 p. 64 6N-T638 1:8; N; 21)						
	1	a-ne-ne	a.ne.ne=Ø	they=ABS	2	ABS	
	2	lú	lú	person	0	GEN+ADV	ABS marked on 5 => copular predicate; GEN+ADV marked on 6
	3	eden	eden	plain	4	nmod	
	4	bar	_	_	2	GEN	consider this a proper namy
	5	tab-ba	...=ak=Ø	...=GEN=ABS	4	appos	
	6	al-me-a-ke4-eš	'a-me-eš-'a=ak=eš	VP-be-3PL.S-NOM=GEN=ADV	2	cop	


#### head in elliptic adverbial constructions

	# Jagersma, Chap. 7 (289)					
	# ‘with five reeds of work for one man’					
	# (DP 622 1:2-3; L; 24)					
	1	lú	lú	man	4	TERM
	2	1-šè	1=še	1=TERM	1	nummod
	4	kíĝ	kíĝ	work	0	ABL
	5	ge	ge	reed	4	appos
	6	5-ta	5=ta	5=ABL	5	nummod
						
	# Jagersma, Chap. 7 (290)					
	# ‘with sixteen bundles in each of its bales’					
	# (TENS 48 2; U; 21)					
	1	gu-niĝin2-ba	gu.niĝin2=be='a	bale=its=LOC	3	LOC
	2	sa	sa	bundle	0	ABL
	3	16-ta	16=ta	16=ABL	2	nummod
	
	# Jagersma, Chap. 7 (291)					
	# ‘with ten shekels (of digging work) by one man’					
	# (ITT 5:6865 2; L; 21)					
	1	lú	lú	man	0	ERG
	2	1-e	1=e	1=ERG	1	nummod
	3	10	10	10	4	nummod
	4	giĝ4-ta	giĝ4=ta	shekel=ABL	1	ABL

	
#### head and attachment of copula clause

	# Jagersma, Chap. 7 (309)								
	# ‘It was (the case) that a slave woman was equal to her mistress.’								
	# (St B 7:31; L; 22)								
	1	geme2	[geme2=Ø	[slave.woman=ABS				3	ABS
	2	nin-a-né	nin=ane=d(a)	lady=her=COM				3	COM
	3	mu-da-sá-àm	Ø-mu-n-da-sá-Ø-'a=Ø]='am	VP-VENT-3SG-with-be.equal-3SG.S/DO-NOM=ABS]=be:3N.S				0	root

	
#### acl vs. parataxis

	# Jagersma, Chap. 7 (318)						
	# ‘four ban (of barley) PN, the cupbearer; he lives in the palace; 4 ban (of barley) PN, the barber; he lives at Lugaltemen’s place’						
	# (DP 119 5:4-11; L; 24)						
	1	0.0.4	0.0.4	4.ban	2	nummod	commodity is implicit, so annotate nummod; with explicit commodity, this would be head
	2	PN	PN	PN	0	root	implicit case is DAT
	4	sagi	sagi	cupbearer	2	appos	
	6	é-gal-la	é.gal='a	palace=LOC	8	LOC	
	8	ì-ti	'i-n(i)-ti.l-Ø	VP-in-live-3SG.S/DO	4	acl	on ground of morphology and translation, parataxis would be better suited; treated here like "the cupbearer who lives in the palace"
	10	0.0.4	0.0.4	4.ban	11	nummod	
	11	PN	PN	PN	2	parataxis	
	13	šu-i	šu.i	barber	11	appos	
	15	lugal-temen-da	lugal.temen=da	Lugaltemen=COM	17	COM	
	17	e-da-ti	'i-n-da-ti.l-Ø	VP-3SG-with-live-3SG.S/DO	13	acl	



#### what=TERM=COP

	# Jagersma, Chap. 7 (252)						
	# ‘Why is it he slanders me regarding the children?’						
	# (MVN 11:168 3-5; U; 21)						
	1	a-na-aš-àm	a.na=še='am	what=TERM=be:3N.S	7	TERM	or root + parataxis?
	3	dumu-dumu-e-ne-ke4-eš	dumu-dumu=enē=ak=eš	child-child=PL=GEN=ADV	7	GEN+ADV	
	4	/			7	punct	
	5	inim	inim	word	7	ABS	
	6	sig-ĝu10	sig=ĝu=Ø	weak=my=ABS	5	amod	
	7	íb-bé	'i-b-'e-e	VP-3N.OO-say:IPFV-3SG.A:IPFV	0	root	


#### Adnominal vs. elliptic adverbial readings

In the following example, either commodity could be syntactic head. If analysed as adnominal ABS resp. TERM, we would prefer 1 to be head in accordance with the general structure of noun phrases. If analysed as elliptic adverbials, we would prefer 5 to be the head as this is the argument closer to the (elliptic) verbal head.

	# Jagersma, Chap. 7 (288)					
	# ‘with ten ban of barley in a month for one pig’					
	# (STH 1:30 9:7-8; L; 24)					
	1	šáh	šáh	pig	5	TERM
	2	1-šè	1=še	1=TERM	1	nummod
	4	iti-da	iti.d='a	month=LOC	5	LOC
	5	še	še	barley	0	ABL
	6	0.1.4-ta	0.1.4=ta	0.1.4=ABL	5	nummod


#### doubtful analyses

Jagersma (2010, p.138, in the context of a possible further case): "Twice in our corpus, a formal element -na-an-na is found which may be a further case marker but which may also be a complex form that includes a known case marker, like, for instance, the locative case marker {÷a}. According to Falkenstein (1956: II, 40) and Edzard (2003b: 158), this -na-an-na means ‘without, apart from’. As I am unable to provide an analysis, I give the two attestations with tentative translations"

suggestion: annotate these as `LOC`

	# Jagersma, Chap. 7 (4)								
	# ‘that, apart from Urbalagkuga, no man slept with her’								
	# (NG 24 10'; L; 21)								
	1	ur-balaĝ-kù-ga-na-an-na	ur.balaĝ.kù.ga.k=nanna	Urbalagkuga=apart.from	4	LOC	Jagersma 2010: 138: analysis uncertain		
	2	/	_	_		punct			
	3	lú	lú=Ø	man=ABS	4	ABS			
	4	nu-ù-da-nú-a	nu='i-n-da-nú-Ø-'a	NEG=VP-3SG-with-lie-3SG.S/DO-NOM	0	acl			

	# Jagersma, Chap. 7 (5)								
	# ‘the Dublamah – this temple was unbuilt, apart from that it had been (a...since time immemorial)’								
	# (FAOS9/2 Amarsuen123-8; Ur;21)								
	1	dub-lá-mah	dub.lá.mah	Dublamah	0	root			
	2	/	_	_		punct			
	3	(...)	(...)	(...)	1	dep			
	4	/	_	_		punct			
	5	ì-me-a-na-an-na	'i-me-Ø-'a=nanna	VP-be-3N.S-NOM=apart.from	1	acl+LOC	# not amod, as there are dependents in 3	Jagersma 2010: 138: analysis uncertain	
	6	/	_	_		punct			
	7	é-bé	é=be=Ø	house=this=ABS	8	ABS			
	8	nu-řú-àm	nu=řú-Ø='am	NEG=erect-NFIN=be:3N.S	1	acl			



#### acl

confirm case of acl+GEN (acl+GEN+ABS?)

	# Jagersma, Chap. 7 (87)						
	# ‘He took an oath by the king’s name to repay it (viz. a barley loan) until the month of Nesag (lit. “of repaying until the Month Nesag, he called a king’s name about it”).’						
	# (SAT 3:1229 6-8; U; 21)						
	1	iti	iti.d	month	4	TERM	
	2	nesaĝ-šè	nesaĝ=ak=še	Nesaĝ=GEN=TERM	1	GEN	
	4	su-su-da	su.g:RDP-ed-Ø=ak	repay:IPFV-IPFV-NFIN=GEN	8	acl+GEN	???
	6	mu	mu	name	8	ABS	
	7	lugal-bé	lugal=ak=be=Ø	king=GEN=its=ABS	6	GEN	
	8	in-pà	'i-n-pà.d-Ø	VP-3SG.A-call-3N.S/DO	0	root	

if the first word is propositional, how can it be head of a relative clause (as entailed by translation):

	# Jagersma, Chap. 8 (22)						
	# ‘It is he who (lit. “(he) who is he”, cf. §29.6.2) holds him for me on orders of the guard.’						
	# (TCS 1:54 6; L; 21)						
	1	e-ne-àm	e.ne=Ø='am	he=ABS=be:3SG.S	0	root	
	2	inim	inim	word	4	ABL	
	3	en-nu-ĝá-[ta]	en.nu.ĝ=ak=ta	guard=GEN=ABL	2	GEN	
	4	ma-an-dab5	Ø-ma-n-dab5-Ø	VP-1SG.IO-3SG.A-take-3SG.S/DO	1	parataxis	? acl

Jagersma's 2010 glosses don't add up to a valid parse:

	# Jagersma, Chap. 6 (50)						
	# ‘its features great features, surpassing all features’						
	# (Cyl A 9:12; L; 22)						
	1	me-bé	me=be=Ø	being=its=ABS	2	ABS	
	2	me	me	being	0	root	interpreted as copular clause with implicit copula
	3	gal-gal	gal-gal	big-big	2	amod	
	4	me-me-a	me-me='a	being-being=LOC	5	LOC	
	5	diri-ga	diri.g-Ø-'a	exceed-NFIN-NOM	2	acl	

#### copula

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
