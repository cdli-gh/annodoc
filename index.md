---
layout: entry
title: Dependency Syntax for Sumerian
---

## Table of contents
- [Status of this document](#status-of-this-document)
- [Background and General Information](#background-and-general-information)
- [Parts of Speech](#parts-of-speech)
- [Syntactic dependencies](#syntactic-dependencies)
  * [Incomplete annotation (dep)](#incomplete-annotation--dep-)
  * [Adjectival modifiers (amod)](#adjectival-modifiers--amod-)
  * [Subordinate clauses (acl)](#subordinate-clauses--acl-)
  * [Adpositions ("case")](#adpositions---case--)
  * [Apposition (appos)](#apposition--appos-)
  * [Nominal modifiers: nmod](#nominal-modifiers--nmod)
  * [Quantifiers: det](#quantifiers--det)
  * [Syntactic coordination: conj, cc](#syntactic-coordination--conj--cc)
  * [Punctuation: punct](#punctuation--punct)
  * [Grammatical roles (morphological case): ABS, ERG, DAT, ABL, ADV, COM, EQU, TERM, LOC, GEN](#grammatical-roles--morphological-case---abs--erg--dat--abl--adv--com--equ--term--loc--gen)
- [Dependency annotation for Administrative texts](#dependency-annotation-for-administrative-texts)
  * [Transactions and their participants](#transactions-and-their-participants)
  * [Dates](#dates)
- [Changes](#changes)
- [Open issues](#open-issues)
  * [Complex numerals](#complex-numerals)
  * [Syntactic relation between mu and year name](#syntactic-relation-between-mu-and-year-name)
  * [Dependency syntax: Other uses of the copula](#dependency-syntax--other-uses-of-the-copula)
- [Mapping to UD](#mapping-to-ud)
- [How to edit this document](#how-to-edit-this-document)
  * [Formatting example annotations](#formatting-example-annotations)
- [Acknowledgements](#acknowledgements)

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

## Parts of Speech

See [Tagsets](https://cdli-gh.github.io/guides/guide_tagsets.html).
Mapping to UD yet to come.

## Syntactic dependencies

The annotation scheme is designed with the goal of mappability to UD v.2, however, the specifics of Sumerian require a language-specific schema. The mapping of native labels to UD dependencies is approached here as a post-processing task. 

As Sumerian employs morphology to mark syntactic relations, we adopt a morphology-driven (rather than a semantics-driven) approach to annotation. This does facilitate automated annotation, but entails the following modifications:

- co(sub)ordination: If subordination or coordination is not made explicit in the morphology annotation, we annotate appos (between a noun and its nominal dependents) or parataxis (between verbs [clauses])
- We use morphological annotations for case as labels for syntactic dependencies of nouns, with two exceptions: all locatives are marked LOC, all datives are marked DAT.
- Sumerian does not have the grammatical category ADJ. The label amod is used for relative clauses without clausal arguments. This also applies to all participles (morphologically, Sumerian relative clauses are participles or nominalizations).
- We annotate all subordinate clauses as relative clauses (acl). If an adverbial function is evident from the morphology, this involves a case marker, and then a compound label acl+CASE is used. This means that we do not use the dependencies ccomp, xcomp, and csubj.
- Sumerian does not have the grammatical category ADV. Adverbials are modelled like adjectives, resp. relative clauses, with additional case marking. The dependencies advcl and advmod do not exist.

### Incomplete annotation (dep)

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

### Subordinate clauses (acl)

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

Note that CDLI annotates adverbial clauses as relative clauses. The label advcl is not used. We follow a morphology-driven approach to syntax annotation and mark syntactic subordination along with the case of the constituent. If a subordinate clause is headless (and also lacking a "relative pronoun" such as lu2), we mark it as acl+CASE. The adverbial function is not expressed in the subordination, but in the morphological case. While we do not use the UD labels advcl (or advmod) in CDLI annotation, these are derived for the UD export as follows:
	
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
1	13	iti	iti[month]	NOUN	N	Number=Sing	0	date	_	_
2	14	ses-da-gu7	Sesdagu[1]	PROPN	MN	Number=Sing	1	appos	_	_
3	15	mu	mu[year]	NOUN	N	Number=Sing	1	LOC	_	_
4	16	{d}gu-za	guza[chair]	NOUN	N	Number=Sing	6	ABS	_	_
5	17	{d}en-lil2-la2	Enlil[1]	PROPN	DN	Animacy=Hum|Case=Gen,Abs|Number=Sing	4	GEN	_	_
6	18	ba-dim2	dim[create]	VERB	V	Number=Sing|Person=3|Voice=Mid	3	acl	_	_
~~~
(P102313)


### Adpositions ("case")

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

### Apposition (appos)

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

implicit genitive
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

implicit copula
~~~ conllu
1	{d}amar-{d}suen	_	_	_	_	0	ABS	_	_
2	ki	_	_	_	_	3	ABS	_	_
3	aŋ₂	_	_	_	_	1	acl+appos	_	_
4	urim₅{ki}-ma	_	_	_	_	3	GEN	_	_

~~~
"Amar-Suen, beloved of Ur" (name of a statue, Q000985)

This can also be interpreted as having an implicit copula (expected to be marked at 20, cf. Hayes 2000, p. 197)

Appositions and case-marked nominal dependents are post-modifying, i.e., the syntactic head of a noun phrase should be its first element. For exceptions to this rule established on semantic grounds (epithets/titles and units), premodifying nominals are marked as nmod.

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

If conjunction is not explicitly expressed, use appos.

### Punctuation: punct

No punctuation in Sumerian. However, breaks (new line, different column, different side) are sometimes used to separate different thoughts. If these are encoded explicitly as part of the text, the recommended dependency is punct. Likewise, if a Sumerian transcript includes modern punctuation signs.

### Grammatical roles (morphological case): ABS, ERG, DAT, ABL, ADV, COM, EQU, TERM, LOC, GEN

As a general rule, the syntactic relation of nominal dependents with their head is described by the morphological case associated with it. If no case is provided, adnominal nouns are marked nmod (if premodifying) or appos (if postmodifying).
As labels for dependencies, we use the case labels employed in morphological annotation, with the exception of locatives (all represented as LOC) and datives (all represented as DAT). Note that locatives include both spatial and temporal relationships.

Where case marking is postulated in the morphology annotation, we follow that analysis, regardless of whether the morpheme is realized in the surface string. In particular, this includes the annotation of administrative texts, where case marking is systematically lacking.

## Dependency annotation for Administrative texts 

The description so far focused on prose text. Administrative texts require a slightly different treatment.

### Transactions and their participants

Dependency relations specific to administrative texts include
- ziga, giri3, kiszib
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
10	zi-ga	_	disembursement-from	2	ziga	_	_
11	be-li2-du10	_	B.	_	_	9	GEN	_	_
12	iti	_	month	_	_	13	nmod	_	_
13	a2-ki-ti	_	Akiti	_	_	2	date	_	_
14	mu	_	year	_	_	13	LOC	_	_
15	an-sza-an{ki}	_	Anshan	_	_	16	ABS	_	_
16	ba-hul	_	destroyed	_	_	14	acl	_	_

~~~	
(P109483)

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

The list relation holds between entitites of the same kind, here, the objects of transaction. Note that list should not be used to connect transactions. We assume that transactions are inherently sentential, so, use `parataxis`. The total is connected by a total relation

The internal structure of complex numerals is represented by `nummod` (design decision; chosen here in favour of `compound` or `flat` which would be equally possible).

Note that the morphology and the relation of a-ra2 (35) are currently unclear and may be revised. Maybe, this is some kind of verbal form?

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

TBC for other roles: the respective person designated is assumed to represent the syntactic head, with the technical term treated like epithet or unit identifier

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
1	ud	_	day	0	date	_	_
2	30	_	29	1	nummod	_	_
3	la1	_	_	2	compound	_	_
4	1-kam	_	_	2	compound	_	_
5	iti	_	month	6	nmod	_	_
6	Sze-kar-ra-gal2	_	Shekaragal	1	LOC	_	_
7	mu	_	year	6	LOC	_	_
8	Si-mu-ru-um{ki}	_	Simurum	14	ABS	_	_
9	Lu-lu-bu-um{ki}	_	Lulubum	8	appos	_	_
10	a-ra2	_	ninth.time	14	dep	_	_
11	10	_	_	10	nummod	_	_
12	la1	_	_	11	compound	_	_
13	1-kam	_	_	11	compound	_	_
14	ba-hul	_	destroyed	_	_	7	acl	_	_

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

- numbered product: conventional structure is `number -nummod-> unit -nmod-> product`. Problematic case is the sequence `number product unit`. Change modelling in gold data to `number -nummod-> product <-appos- unit` (instead of `number -nummod-> [product -nmod-> unit]`). Check whether there are any such cases in the guidelines. The reason is to have the product systematically as head.
- acl: originally, the morphological feature was used for annotation (e.g., SUB, TL, etc.). Replace globally with `acl`. This is done here but must be applied to gold data.
- connect transactions by parataxis (not by list, as this is used for numbered products and could be conflated)
- change internal structure of complex numerals to appos (add there "implicit addition") rather than compound; for la2, see morphology guidelines 
- TODO: synchronize with (https://cdli-gh.github.io/guides/month_names.html), (https://cdli-gh.github.io/guides/verbal_chain_slot_system.html), (https://cdli-gh.github.io/guides/lists.html)
- TODO: add material from https://drive.google.com/drive/folders/1bYRho0QkHCiTE-ajPlvJTTmM8bViI4da
- iti+month name: current pre-annotation: iti is head, month in apposition (fix in docu and data)
- complex numbers: head is nummod, internal relation produced by pre-annotation is also nummod; change guidelines and examples (currently compound); add comment that an alternative analysis would be with `appos` (with appos for implicit addition), but that (as a design decision), this is not done here.
- TODO: 11. As for giri3 PN (by the means of PN), and kishib PN (by the seal of PN), we tag giri3/kishib as obl, mark dependent as GEN (in data and doc)

## Open issues

### Dependency syntax: Other uses of the copula

~~~ conllu
1	šag₄	_	heart	_	_	6	ERG	_	_
2	en-lil₂-la₂-ke₄	_	DN=GEN=ERG	_	_	1	GEN	_	_
3	id2idigna-am₃	_	WN=STM	_	_	1	STM	acl?	_	_
4	a	_	water	_	_	6	ABS	_	_
5	dug₃-ga	_	sweet-PT=ABS	_	_	4	amod	_	_	
6	nam-de₆	_	MOD-VEN-3.SG.NH.A-bring-3.SG.P	_	_	0	root	_	_

~~~						
“The heart of the god Enlil brought sweet water like the river Tigris.”	(Q000377)					

The third word contains the "standard marker"; this actually contains the copula, but lexicalized into a cleft-like construction. This is evident from the ergative case that the subject receives from the verb in line 6. However, it does not depend on szag, because otherwise, the ergative marker would have been placed after the STM. Nevertheless, it is analyzed as an acl here.

An alternative (and shallower) analysis would be to interpret the copula literally, and to postulate a parataxis relation ("The heart of Enlil is (like) the Tigris; he brought sweet water.") However, the ergative of sza3 remains unexplained, then. 

The most consistent way to annotate such cases would be to interpret the copula like a morphological case (or, if non-clitic, as a ,focus particle). Requires deeper study. This is, however, not relevant to administrative texts.

Both these models violate the underlying morphology.

## Mapping to UD

yet to come

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

Contributors:
EPP, JW, LR, ...

This page is based on a fork of the [Annodoc](http://www2.lingfil.uu.se/SLTC2014/abstracts/sltc2014_submission_32.pdf) template, originally under (https://github.com/spyysalo/annodoc). See there for documentation.
