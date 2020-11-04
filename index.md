---
layout: entry
title: Dependency Syntax for Sumerian
---

## Table of contents
- [Status of this document](#status-of-this-document)
- [Background and General Information](#background-and-general-information)
- [Parts of Speech](#parts-of-speech)
- [Syntactic dependencies](#syntactic-dependencies)
	- [Incomplete annotation (dep)](#incomplete-annotation-dep)
	- [Adjectival modifiers (amod)](#adjectival-modifiers-amod)
	- [Subordinate clauses (acl)](#subordinate-clauses-acl)
	- [Subordinating conjunction: mark](#subordinating-conjunction-mark)
	- [Adpositions ("case")](#adpositions-case)
	- [Apposition (appos)](#apposition-appos)
	- [Nominal modifiers: nmod](#nominal-modifiers-nmod)
	- [Quantifiers: det](#quantifiers-det)
	- [Syntactic coordination: conj, cc](#syntactic-coordination-conj-cc)
	- [Punctuation: punct](#punctuation-punct)
	- [Grammatical roles (morphological case): ABS, ERG, DAT, ABL, ADV, COM, EQU, TERM, LOC, GEN](#grammatical-roles-morphological-case-abs-erg-dat-abl-adv-com-equ-term-loc-gen)
		- [Case of headless phrases](#case-of-headless-phrases)
		- [Possession](#possession)
	- [Vocative: voc](#vocative-voc)
	- [Dislocation: +disloc](#dislocation-disloc)
	- [Clausal complement: ccomp](#clausal-complement-ccomp)
	- [Copula clauses: cop](#copula-clauses-cop)
- [Dependency annotation for Administrative texts](#dependency-annotation-for-administrative-texts)
	- [Transactions and their participants](#transactions-and-their-participants)
	- [Discontinuous lists](#discontinuous-lists)
	- [Dates](#dates)
	- [Complex numerals](#complex-numerals)
	- [Detached totals](#detached-totals)
- [Changes](#changes)
- [Open issues](#open-issues)
	- [Adverbial clauses: advcl](#adverbial-clauses-advcl)
	- [Dependency syntax: Other uses of the copula](#dependency-syntax-other-uses-of-the-copula)
- [Mapping to UD](#mapping-to-ud)
- [How to edit this document](#how-to-edit-this-document)
	- [Formatting example annotations](#formatting-example-annotations)
- [Acknowledgements](#acknowledgements)
	- [Contributors](#contributors)
	- [References](#references)

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

If adjectives appear without nominal head, but with a grammatical role (morphological case) in a clause, use the morphological case for their annotation. Likewise, lexicalized deverbal nominals are annotated like nominal arguments. Titles or functionaries can be referred to with (lexicalized) nominalizations, and then, an annotation like a nominal (nmod or appos) would be preferrable. Here, we follow the decision taken in morphology annotation.

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

Note that headless relative clauses can be clausal arguments, and should be marked with the corresponding case:

~~~ conllu
1	2(barig)	_	_	_	_	2	nummod	_	_
2	kasz	_	_	_	_	17	parataxis	_	_
3	elam	_	_	_	_	4	ABL	_	_
4	ki-masz{ki}-me	_	_	_	_	2	acl+DAT	_	_

~~~
"120 liter beer for those (slaves) from Elam" (P315784)

elam ki-masz{ki}-me carries a copula and is thus analyzed as a predicate here.

Todo: check the treatment of clauses in absolutive case

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

Note that CDLI annotates adverbial clauses without `mark` as relative clauses. We follow a morphology-driven approach to syntax annotation and mark syntactic subordination along with the case of the constituent. If a subordinate clause is headless (and also lacking a "relative pronoun" such as lu2), we mark it as acl+CASE. The adverbial function is not expressed in the subordination, but in the morphological case. While the use of `advcl` and `advmod` is limited in CDLI annotation, these are derived for the UD export as follows:
	
	acl+LOC, TERM, EQU, etc. => advcl
	acl+GEN => acl (modifying a noun)
	acl => acl (in apposition with a noun)

As for acl+ABS, acl+ERG and acl+DAT, these are systematically ambiguous between nominal (UD nsubj, obj, iobj) and clausal interpretation (UD csubj, ccomp, xcomp) and asserting one would be artificial and not grounded in Sumerian grammar. If subordination is morphologically marked, the UD label is thus always chosen in accordance with their case (i.e., nominal interpretation). The UD labels csubj, ccomp and xcomp are not being used.

Note that syntactic annotation is morphology-driven. If subordination is not marked in the morphological annotation, we resort to parataxis. Note that subordination morphemes may have gone unwritten (e.g., because of assimilation processes or deficiencies of the writing), but if (unambiguously) so, we expect them to be restored in the morphological annotation.

Note that `acl` is also used for the syntactic relation between *mu* `year` and year name (typically a clause), also if subordination is not morphologically marked.

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

### Subordinating conjunction: mark

Subordinate markers (CNJ), like *tukumbi* 'if'

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

TODO: clarify whether `CNJ` in morphology can reliably distinguish coordinating and subordinating conjunctions
TODO: list coordinating and subordinating conjunctions

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

Sumerian syntax annotation is morphology-driven. If an adnominal noun does not morphologically or syntactically mark its relation with its head, it is marked as appos. Appositions are widely used and cover interpretations such as implicit identity, implicit coordination, implicit genitive, or implicit copula.

implicit identity

~~~ conllu
1	an	_	_	_	_	0	DAT	_	_
2	lugal	_	_	_	_	1	appos	_	_
3	diŋir-re-ne	_	_	_	_	2	GEN	_	_
4	lugal-a-ni	_	_	_	_	1	appos	_	_

~~~
"An, king of the gods, his king" (Q000937)

implicit conjunction

~~~ conllu
1	lugal	_	_	_	_	0	appos	_	_
2	ki-en-gi	_	_	_	_	1	GEN	_	_
3	ki-uri-ke₄	_	_	_	_	2	appos	_	_

~~~
"king of Sumer (and) Akkad" (Q000953)

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

The overt morphology (according to annotation) of ur-dba-u₂-ka provides the locative marker, but the genitive remains implicit. As for the annotation of implicit genitives as appos, we rely on morphology annotation. If the genitive is restored in morphology annotation, the dependency will be labelled GEN.

The pattern applies to both adnominal cases, i.e., GEN and EQU. Note that equatives forms nominal sentences, an implicit equative can thus always also be interpreted as implicit copula. We thus do not annotate implicit equatives as such. Instead, apply the annotation of implicit copula.

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

Note that implicit addition in complex numerals is *not* annotated by `appos`, but by `nummod`:

~~~ conllu
1	3(gesz2)	3(gesz)[sixty]	NUM	NU	_	4	nummod	_	_
2	1(u)	1(u)[ten]	NUM	NU	_	1	nummod	_	_
3	7(disz)	7(disz)[one]	NUM	NU	_	1	nummod	_	_
4	udu	udu[sheep]	NOUN	N	Number=Sing	0	root	_	_

~~~
"197 (180+10+7) sheep" (P102315)

Appositions and most case-marked nominal dependents are post-modifying, i.e., the syntactic head of a noun phrase should be its first element. For exceptions to this rule established on semantic grounds (epithets/titles and units), premodifying nominals are marked as nmod.

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

TODO: Check `conj` vs. `list` in taglist

	There are some cases where some conclusive phrases are put to describe different goods mentioned above, for example, sheep, goats, donkeys, the delivery/ offering/ expenditure/ wage. It is more convenient to use `conj` or `list` in these cases.

### Nominal modifiers: nmod

In CDLI annotation, nmod is exclusively used for prenominal nominal modifiers. Postnominal nominal modifiers are marked according to their case or as appos.

Sumerian NPs usually place the head of the NP at their left periphery. For semantic reasons, we deviate from this analysis for epithets (incl. titles, etc.) and units:

~~~ conllu
1	sukkal	_	minister	_	_	2	nmod	_	_
2	an-sig₇-ga-ri-a	_	PN.ABS	_	_	0	ABS	_	_

~~~
"Minister Ansiga-ria" (Q000370)

In the mapping to UD interpretation, case-marked adnominal dependents of nominal heads are mapped to nmod. Most prominently, this includes genitives.

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

Morphologically marked conjunction is *-bi-da*, frequently written as *-bi*, and typically occurring between nouns. Originally, *-bi* marks possession and *-da* marks comitative (Hayes p.356). Annotated as `conj` here, not `COM`. 

~~~ conllu
1	{id2}idigna	idigna	Tigris	_	_	6	ERG	_	_
2	{id2}buranuna-bi-da	buranuna	Euphrates.CONJ.ERG	_	_	1	conj	_	_
3	gud	gud	bull	_	_	6	EQU	_	_
4	gal-gin7	gal	big.EQU	_	_	3	amod	_	_
5	jiri3-bi	jiri3	foot.their	_	_	6	ABS	_	_
6	nam-mi-in-gub	gub	stand	_	_	0	root	_	_

~~~

"The Tigris and the Euphrates stood like great bulls" (EE 28, example from PPCS manual)

If applied to a clausal argument, it can express a circumstantial meaning. For these cases, we annotate `acl+COM`, not `conj`.

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

### Punctuation: punct

No punctuation in Sumerian. However, breaks (new line, different column, different side) are sometimes used to separate different thoughts. If these are encoded explicitly as part of the text, the recommended dependency is punct. Likewise, if a Sumerian transcript includes modern punctuation signs.

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

#### Adominal dependents: GEN, EQU

In CDLI, annotated according to morphological case. In UD export as `nmod`. If no morphological case is annotated, use `nmod` for pre-modifying nominals, `appos` for post-modifying nominals.

	N; GEN；N.3-SG-POSS (Its weight, size……..)
	N-N.3-SG-POSS

> Taglist doesn't make the difference between `appos` and `nmod` explicit. TODO: confirm treatment in pre-annotation and in annotation projection.

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

~~~ conllu
1	...	_	N	_	_	0	root	_	_
2	...	_	NU.GEN.COP-3-SG	_	_	1	nummod	_	_

~~~
(postmodifying numeral)

Furthermore, `nummod` is used for parts of a numeral, annotated as dependents of the first element in a numeral

> Note: Earlier, we used `compound` and `flat` for the internal structure of complex numerals. But this is inconsistent with the annotation of *la2* "minus" as `acl` (should be `flat` as well, then). Hence, another relation.

### Compound: compound

Used for the nominal part of a compound verb (if a list of compound verbs is provided). Without such a list, this is annotated according to its grammatical structure (if transparent).

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
- taglist recommends `appos` for `MN` (month name), with head being the day [this entails that *iti* is an epithet and annotated as `nmod` dependent]
	- the examples above use `LOC` for dependencies within dates and `date` for the head element of a date
- taglist recommends `appos` for the clause after MU
	- examples have `ccomp`
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
- year name: annotate as ccomp, not as acl, because this is (kind of) direct speech

## Open issues

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
- PPCS (2004), PPCS (Penn Parsed Corpus of Sumerian): A Brief Introduction to the Syntactic Annotation System of the PPCS, version of 6/14/04, available from https://www.yumpu.com/en/document/view/12162126/ppcs-penn-parsed-corpus-of-sumerian-a-brief-introduction-to-the- and https://web.archive.org/web/20070708210654if_/http://psd.museum.upenn.edu/ppcs/ppcs-manual.pdf, author is unnamed (Fumi Karahashi)
