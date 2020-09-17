---
layout: entry
title: Dependency Syntax for Sumerian
---


## Table of contents

## Basics of Sumerian grammar

yet to come

## Parts of Speech

yet to come

## Syntactic dependencies

The annotation scheme is designed with the goal of mappability to UD v.2, however, the specifics of Sumerian require a language-specific schema. The mapping of native labels to UD dependencies is approached here as a post-processing task. 

As Sumerian employs morphology to mark syntactic relations, we adopt a morphology-driven (rather than a semantics-driven) approach to annotation. This does facilitate automated annotation, but entails the following modifications:

- co(sub)ordination: If subordination or coordination is not made explicit in the morphology annotation, we annotate appos (between a noun and its nominal dependents) or parataxis (between verbs [clauses])
- We use morphological annotations for case as labels for syntactic dependencies of nouns, with two exceptions: all locatives are marked LOC, all datives are marked DAT.
- Sumerian does not have the grammatical category ADJ. The label amod is used for relative clauses without clausal arguments. This also applies to all participles (morphologically, Sumerian relative clauses are participles or nominalizations).
- We annotate all subordinate clauses as relative clauses (acl). If an adverbial function is evident from the morphology, this involves a case marker, and then a compound label acl+CASE is used. This means that we do not use the dependencies ccomp, xcomp, and csubj.
- Sumerian does not have the grammatical category ADV. Adverbials are modelled like adjectives, resp. relative clauses, with additional case marking. The dependencies advcl and advmod do not exist.

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
2	...	_	_	_	_	_	_	_	_
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

Note syntactic annotation is morphology-driven. If subordination is not marked in the morphological annotation, we resort to parataxis. Note that subordination morphemes may have gone unwritten (e.g., because of assimilation processes or deficiencies of the writing), but if (unambiguously) so, we expect them to be restored in the morphological annotation.

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

	1	šag₄	heart	6	ERG
	2	en-lil₂-la₂-ke₄	DN=GEN=ERG	1	GEN
	3	id2idigna-am₃	WN=STM	1	acl
	4	a	water	6	ABS
	5	dug₃-ga	sweet-PT=ABS	4	amod
	6	nam-de₆	MOD-VEN-3.SG.NH.A-bring-3.SG.P	0	root

“The heart of the god Enlil brought sweet water like the river Tigris.” (Q000377)

As these constructions are analyzed in accordance with their morphology rather than their semantic interpretation in English, the UD label "case" is not used for Sumerian.

### Apposition (appos)

Sumerian syntax annotation is morphology-driven. If an adnominal noun does not morphologically or syntactically mark its relation with its head, it is marked as appos. Appositions are widely used and cover interpretations such as implicit identity, implicit coordination, implicit genitive, or implicit copula.

implicit identity

	1	an	10	DAT
	2	lugal	1	appos
	3	diŋir-re-ne	2	GEN
	4	lugal-a-ni	1	appos

"An, king of the gods, his king" (Q000937)

implicit conjunction

	8	lugal	3	appos
	9	ki-en-gi	8	GEN
	10	ki-uri-ke₄	9	appos
	
"king of Sumer (and) Akkad" (Q000953)

implicit genitive

	1	kišib₃	6	ABL
	2	ur-dšul-pa-e₃-ka	1	GEN
	3	bešeŋ	5	LOC
	4	ur-dba-u₂-ka	3	appos
	5	i₃-in-ŋal₂-la-ta	1	SUB
	6	tur-re-dam	0	root
	
“These (various animals) are to be subtracted from the sealed tablet of Uršulpae that is in the basket of Urbau.” (P113923)

The overt morphology (according to annotation) of ur-dba-u₂-ka provides the locative marker, but the genitive remains implicit. As for the annotation of implicit genitives as appos, we rely on morphology annotation. If the genitive is restored in morphology annotation, the dependency will be labelled GEN.

implicit copula

	17	{d}amar-{d}suen	21	ABS
	18	ki	19	ABS
	19	aŋ₂	17	SUB+appos
	20	urim₅{ki}-ma	19	GEN

"Amar-Suen, beloved of Ur" (name of a statue, Q000985)

This can also be interpreted as having an implicit copula (expected to be marked at 20, cf. Hayes 2000, p. 197)

Appositions and case-marked nominal dependents are post-modifying, i.e., the syntactic head of a noun phrase should be its first element. For exceptions to this rule established on semantic grounds (epithets/titles and units), premodifying nominals are marked as nmod.

### "Adjectival" modifiers: amod

Relative clauses without arguments are annotated as amod, cf. acl. All "adjectives" are nominalized verbs, and we follow the morphological analysis as to whether they are annotated as a amod or as appos. Titles or functionaries can be referred to with (lexicalized) nominalizations, and then, an annotation as appos would be preferrable.

Sumerian forms two different participles, the "passive participle" in -a (also used to signal clausal subordination) and the "active participle" in -0. The annotation of active participles follows the same pattern with respect to amod/acl distinction as the annotation of passive participles. However, active particiles are more commonly annotated as amod.

### Nominal modifiers: nmod

In CDLI annotation, nmod is exclusively used for prenominal nominal modifiers. Postnominal nominal modifiers are marked according to their case or as appos.

Sumerian NPs usually place the head of the NP at their left periphery. For semantic reasons, we deviate from this analysis for epithets (incl. titles, etc.) and units:

	4	sukkal	S[minister	5	nmod
	5	an-sig₇-ga-ri-a	PN=ABS]	6	ABS

"Minister Ansiga-ria" (Q000370)

In the mapping to UD interpretation, case-marked adnominal dependents of nominal heads are mapped to nmod. Most prominently, this includes genitives.

### Quantifiers: det

There are no determiners in Sumerian. The label det is used for postnominal quantifiers (themselves nominal).

	1	niŋ₂	P1thing	4	ABS
	2	na-me	P2some=P5ABS	1	det
	3	a₂-be₂	arm=3.SG.NH.POSS=ABL	4	ABL
	4	la-ba-ra-e₃	NEG-MID-ABL-leave-3.SG.S	0	root

"Nothing escaped their clutches." (Q000375)
	
### Syntactic coordination: conj, cc

Conjunction can be expressed morphologically or syntactically.

	22	e₂	N1=STEM	30	ABS
	23	lal₃	N1=STEM.N5=ABS	29	ABS
	24	i₃-nun	N1=STEM.N5=ABS	23	conj
	25	u₃	N1=STEM	23	cc
	26	ŋeštin	N1=STEM.N5=ABS	23	conj
	27	ki	N1=STEM	30	LOC
	28	sizkur₂-ra-ka-na	N1=STEM.N5=GEN.N3=3-SG-H-POSS.N5=L1	27	GEN
	29	nu-silig-ge	NV1=NEG.NV2=STEM.NV3=PF.N5=ABS	22	acl

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
- ziga, giri3
- total, date, agent
- list
- compound (in nominals)

Administrative texts often exhibit a list-like character without clear sentential structure. 

	1	1(disz)	1	2	nummod
	2	gu4	bull	0	root
	3	niga	barley-fattened	2	amod
	4	ma2	for the ship	2	TERM
	5	an-na	of An	4	GEN
	6	sza3	in	2	LOC
	7	unu{ki}-ga	Uruk	6	GEN
	8	giri3	the transmitter was		giri3
	9	bar-bar-re	B.	8	GEN 
	10	zi-ga	disembursement from	2	ziga
	11	be-li2-du10	B.	9	GEN
	12	iti	month of	13	nmod
	13	a2-ki-ti	Akiti	2	date
	14	mu	year	13	LOC
	15	an-sza-an{ki}	when Anshan	16	ABS
	16	ba-hul	was destroyed	14	acl
	
(P109483)

This text describes a single transaction, but without any explicit verbal element. The obligatory part of a transaction statement is the object being transferred. This is thus modelled as root. A transaction involves a number of functional roles, some of which are partially understood, only. These are identified by morphological case labels (if provided by the morphology annotation, here TERM, LOC), Sumerian technical terms (here ziga, giri3), or semantic role labels (date, agent [= unmarked receiver or supplier], total).

	1	83	83	2	nummod
	2	gud	bulls	0	root
	3	niga	barley-fattened	2	appos
	4	32	32	5	nummod
	5	gud	bulls	2	list
	6	u2	grass-fattened	5	appos
	7	20	18	8	nummod
	8	la1		7	compound
	9	2		7	compound
	10	ab2	cows	2	list
	11	mu	years	10	appos
	12	2	two (years old)	11	nummod
	13	niga	barley-fattened	10	appos
	14	4	4	15	nummod
	15	ab2	cows	2	list
	16	mu	years	15	appos
	17	2	two (years old)	16	nummod
	18	u2	grass-fattened	15	appos
	19	4	4	20	nummod
	20	amar	calves	2	list
	21	ga	milk-fed	20	appos
	22	szu-nigin2	total	2	total
	23	141	141	24	nummod
	24	gud-hi-a	assorted cattle	22	appos
	25	zig3-ga	disembursement	24	amod
	26	ud	of day	22	date
	27	30	29	26	nummod
	28	la1		27	compound
	29	1-kam		27	compound
	30	iti	month	31	nmod
	31	Sze-kar-ra-gal2	Shekaragal	26	LOC
	32	mu	year	31	LOC
	33	Si-mu-ru-um{ki}	(when) Simurum	39	ABS
	34	Lu-lu-bu-um{ki}	and Lulubum	39	ABS
	35	a-ra2	for the ninth time	39	dep
	36	10		35	nummod
	37	la1		36	compound
	38	1-kam		36	compound
	39	ba-hul	destroyed	32	acl

(no CDLI, Kang 252, Hayes 2000, p. 367)

The list relation holds between entitites of the same kind, here, the objects of transaction. The total is connected by a total relation

The internal structure of complex numerals is not analyzed, but represented by compound.

Note that the morphology and the relation of a-ra2 (35) are currently unclear and may be revised. Maybe, this is some kind of verbal form?

Note that administrative texts *can* actually use overt verbs, in this case, the verb is the root, and the object of the transition is assumed to be a terminative argument.

	1	1	1	2	nummod
	2	lulim	deer	20	TERM
	3	nitab	male	2	appos
	4	2	2	5	nummod
	5	lulim	deer	2	list
	6	munus	female	5	appos
	7	1	1	9	nummod
	8	amar	calf	9	nmod
	9	lulim	deer	2	list
	10	munus	milk-fed	9	appos
	11	ga	female	9	appos
	12	ba	dead.	13	ABS
	13	usz2		2	acl
	...
	18	{d}Szu-gi-uru-gu10	Shulgiurugu	20	ERG
	19	szu	received	20	ABS
	20	ba-ti		0	root

Archi and Pomponio 347, Hayes p.371, not in CDLI

TBC: As for technical terms, the respective person designated is assumed to represent the syntactic head, with the technical term treated like epithet or unit identifier

### Dates
==

Head of a date phrase is the first element (day, month or year), connected by a LOC relation. Days are identified by numbers, using the nummod relationship. The head of a day phrase is thus u3 "day". Months are identified by proper names, so that iti "month" is modelled like an epithet, with the month name as head. Year names are normally sentential, we consider the word "mu" as syntactic head, and the actual year name a relative clause.

	12	iti	month of	13	nmod
	13	a2-ki-ti	Akiti	2	date
	14	mu	year	13	LOC
	15	an-sza-an{ki}	when Anshan	16	ABS
	16	ba-hul	was destroyed	14	acl
	
(P109483)

	26	ud	of day	22	date
	27	30	29	26	nummod
	28	la1		27	compound
	29	1-kam		27	compound
	30	iti	month	31	nmod
	31	Sze-kar-ra-gal2	Shekaragal	26	LOC
	32	mu	year	31	LOC
	33	Si-mu-ru-um{ki}	(when) Simurum	39	ABS
	34	Lu-lu-bu-um{ki}	and Lulubum	39	ABS
	35	a-ra2	for the ninth time	39	dep
	36	10		35	nummod
	37	la1		36	compound
	38	1-kam		36	compound

(no CDLI, Kang 252, Hayes 2000, p. 367)

Days, months and years are assumed to be connected by a LOC (temporal) relationship because of their semantics.

Dates can be written discontinuously:

	7	1	1	9	nummod
	8	amar	calf	9	nmod
	9	lulim	deer	2	list
	10	munus	milk-fed	9	appos
	11	ga	female	9	appos
	12	ba	dead.	13	ABS
	13	usz2		2	acl
	14	ud		20	date
	15	25-kam		15	nummod
	16	ki	from Ludigira	20	LOC
	17	Lu2-digir-ra-ta		16	GEN
	18	{d}Szu-gi-uru-gu10	Shulgiurugu	20	ERG
	19	szu	received	20	ABS
	20	ba-ti		0	root
	21	iti	Month of Kisig-Ninazu.	22	nmod
	22	Ki-sig2-{d}Nin-a-zu		20	date
	23	mu	The year when Shashru was destroyed (Amar-Sin 6).	22	LOC
	24	Sza-asz-ru{ki}		25	ABS
	25	ba-hul		23	acl

(no CDLI, Archi and Pomponio 347, Hayes p.371)

In this case, create multiple date relations with the respective root element.

## Open issues

### Dependency syntax: Other uses of the copula

	1	šag₄	heart	6	ERG
	2	en-lil₂-la₂-ke₄	DN=GEN=ERG	1	GEN	
	3	id2idigna-am₃	WN=STM	1	STM	acl?
	4	a	water	6	ABS	
	5	dug₃-ga	sweet-PT=ABS	4	amod		
	6	nam-de₆	MOD-VEN-3.SG.NH.A-bring-3.SG.P	0	root
						
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

CoNLL dialects differ with respect to the kind of annotation they provide and the order of columns. The Annodoc visualization provides partial support for two CoNLL dialects, CoNLL-X and CoNLL-U, with a focus on syntactic dependencies. Note that the original column structure of the data may require adjustments when used in this document. 

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

The CoNLL-U format defines 10 columns separated by TAB (in Annodoc: space), again, only fields 1 `ID`, 2 `WORD`, 4 `POS`, 7 `HEAD` and 8 `EDGE` are visualized.

Note that Annodoc supports either space or tab as column separator, but no mixture. Furthermore, exactly ten columns are required, it is not admissable to omit the trailing empty columns.
Also note that Annodoc *requires* numerical IDs, starting with 1. CDLI IDs must be replaced, fragments from actual annotations must be adjusted in their ID and HEAD information.

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
