---
layout: single
title: Data Types
permalink: /docs/data-types/
toc: true
sidebar:
  nav: "docs"
---

[//]: # (Please put comments like this one into the text to communicate with other OBI-ers)


[//]: # (# Basic Implementation Issues: RDF, OWL, etc. )

[//]: # (OWL-driven reasoning and SPARQL querying can be applied to data represented in a graph to compare sets of specimen qualities or phenotypes like weight, length, life stage, handedness, and other dimensions.) 

OWL inherits most of RDF's ability to specify XML string, numeric, datetime, and URI datatype values as data properties of an entity, and can compare data properties across entities (see [here](https://www.w3.org/TR/xmlschema-2/) and [here](https://www.w3.org/TR/swbp-xsch-datatypes)).  OWL can also be used to specify constraints on string value length and content, and can specify numeric bounds on numbers.  OBI currently focuses on reuse of RDF/XML datatypes to capture experimental data.  Those who need further functionality may find other datatype representations useful (e.g. [here](https://www.sciencedirect.com/science/article/pii/S0020025515005800)). 

Here a handful of the primitive datatypes from RDF which are used in OWL are discussed. The possibility of [user defined datatypes](https://www.w3.org/TR/swbp-xsch-datatypes/#sec-userDefined) is avoided in favour of using enhanced value specifications to do the same work.  Some examples below are expressed directly in OBI, while others can be constructed in an application ontology that draws on OBI components.  Although OWL 2.0 isn't suitable for doing all types of validation, we have shown how value specifications can be enhanced with basic numeric range and string content restrictions.


## String
An OWL data property can hold a string as a plain literal with an optional language tag (see [here](https://www.w3.org/2007/OWL/wiki/PlainLiteral) ). This enables constraints on string length and its contents (by way of regular expressions).  

For example, one could construct the following representation to store and validate international postal codes generally, and the US Zip Code subclass (a string of 5 digits).

[//]: # (        Class: 'string value specification'        subClassOf 'has specified value' only xsd:string)

[//]: # (        subClassOf 'string value specification')

    Class: 'postal code specification'
        subClassOf 'value specification'
        subClassOf 'has specified value' only xsd:string[pattern "[0-9A-Za-z \-]{2,10}"]

    Class: 'ZIP code specification'
        subClassOf 'postal code specification'
        subClassOf 'specifies value of' some ('postal code' and 'is about' some (site and 'located in' some 'United States of America')
        subClassOf 'has specified value' only xsd:string[pattern "[0-9]{5}"]

[diagram]

String length constraints can be set via "length", "minLength" and "maxLength" parameters, e.g. "xsd:string[length "5"^^xsd:integer].  A "pattern" parameter supports [regular expression](https://www.regular-expressions.info/xml.html) syntax to some extent, allowing "[0-9] [a-z] [A-Z] . ? * + {m,n}" components.  Thus we can express fairly well-validated  [email addresses](http://purl.obolibrary.org/obo/IAO_0000429):

[//]: # (        subClassOf 'string value specification')

    Class: 'email address specification'
        subClassOf 'value specification'
        subClassOf 'specifies value of' only 'email address' 
        subClassOf 'has specified value' only xsd:string[pattern "[A-Za-z0-9]+([_.\-][A-Za-z0-9]+)*\@[A-Za-z0-9]+([.\-][A-Za-z0-9]+){1,3}"]

Note one quirk: In pattern matching, the "@" character must be escaped or else the remainder of test string is ignored (i.e. "@" is interpreted as a language facet addition to the string).  Also more work is required to cover possible validation of [international / UTF-8 strings](https://www.regular-expressions.info/unicode.html).

## Categorical

A categorical value specification is a flat list or hierarchic tree structure containing a finite number of pre-determined choices. Here we provide for choices whose values are either xsd:string or xsd:anyURI references to ontology terms.

### Categorical string choice

If a string must conform to a smaller set of choices, and nothing more needs to be axiomatized about each choice, then this can be accomplished with a value specification that is both string and categorical.  The value specification has a 'has specified value' component which uses a regular expression to enumerate the permitted strings. Note that in this approach one cannot easily provide other information (label, description) about choice in a user interface.

For example, an "E-coli K antigen value specification" can be represented as:

    Class: 'E-coli K antigen value specification'
        subClassOf 'categorical value specification'
        subClassOf 'specifies value of' only 'K antigen'
        subClassOf 'has specified value' only xsd:string[pattern "K(1|2a|2ac|3|4|5|6|7|8|9|10|11|12|13|14|15|16|18a|18ab|19|20|22|23|24|26|27|28|29|30|31|34|37|39|40|41|42|43|44|45|46|47|49|50|51|52|53|54|56|96|55|74|82|84|85ab|85ac|87|92|93|95|97|98|100|101|102|103|X104|X105|X106)"]]

[diagram]

This allows a reasoner to raise the unsatisfiable alarm when an instance of `E-coli K antigen value specification`  `has specified value` 'K17a'.

One can potentially leave the `has specified value` axiom out, in which case validation enforcement would need to occur outside the OWL reasoning context.

### Categorical ontology term choice

Categorical choice lists or trees of ontology terms (e.g. of organism taxonomy, of disease, etc.) essentially have an xsd:anyURI datatype since a selection is an ontology URI. The aim here is to point to existing ontology class or instance identifiers within one's application ontology and/or imported from 3rd party ontologies as selections for a categorical variable. However, some complications arise which the following example will explore.  We could try to capture a [`handedness`](http://purl.obolibrary.org/obo/PATO_0002201) quality with:

    Class: 'handedness value specification'
        subClassOf 'categorical value specification'
        subClassOf 'has specified value' only handedness 

However, this is not permitted in OWL since **`has specified value`** data property can only have a literal on the right side. The target could be expressed simply as "`has specified value` only xsd:anyURI", thus allowing values like xsd:anyURI [right-handedness](http://purl.obolibrary.org/obo/PATO_0002203) but this then requires some validation mechanism external to an OWL reasoner for limiting categorical values. The Class doesn't indicate what the choices are.

In a different approach, an OBI example using categorical value specification focuses on describing a tumor grading standard [`histologic grade according to AJCC 7th edition`](http://purl.obolibrary.org/obo/OBI_0002205).  Here the value specification class has individuals which are each interpreted as grades, and which could potentially be augmented with data properties that detail their assessment differentiae.  This approach is suited to cases where selections are not already established (and would not be in the future) as ontology classes situated within their own hierarchic context. 

Alternately one could use the `specifies value of` relation to point to existing categorical choices (qualities, etc.):

[//]: # (        subClassOf 'categorical ontology value specification')

    Class: 'handedness value specification'
        subClassOf 'categorical value specification'
        subClassOf 'specifies value of' only handedness

Now an instance of `handedness value specification` can have a **`specifies value of`** axiom pointing to a `handedness` class instance. This involves some extra setup because all `handedness` selections need to be "**punned**" since they can't be referenced directly as classes. In other words an individual needs to be created to mirror each categorical choice, so for example classes for left handedness, right handedness, ambidextrous handedness all need mirrored individuals - and in this case these are not native to the PATO ontology that the classes originate from. (Punning is accomplished manually in Protege by copying an existing class URI into the "Create a new Named individual" form, with the "new entity options ..." set to expect a user supplied name.  This preserves the same identifier for both class and individual).

[//]: # (Is punning somehow automated so that loading an ontology with [individual x] `specifies value of` [Class y] causes Class y to be punned automatically? )

[//]: # (A simplified model could shift the burden of choice enumeration directly to value specification. )

[//]: # (Note that as future versions of a standard occur, it may be feasible to attach individuals of past standards to them if no semantics have changed, thus simplifying data analysis.)

*Note that in the past OBI used/tried [`categorical measurement datum`](http://purl.obolibrary.org/obo/OBI_0000938) for enumerating categorical choices, with a [`has category label`](http://purl.obolibrary.org/obo/OBI_0000999) object property that linked to a set or class of permissible terms (as shown in OBI's existing `handedness value specification` example). This class and relation is being discouraged in favour of the categorical value specification approach.*

[//]: # (Slightly different from a boolean value specification below, a binary value specification is a categorical value specification with only two choices.)

## Boolean

Under discussion is the formalization of a "boolean value specification" datatype that pertains to the presence
or absence of a quality or categorical entity. Essentially any quality taken on its own can be treated as a boolean variable.  The information that an animal is characterized as a [`neonate`](http://www.ebi.ac.uk/efo/EFO_0001372), for example may be the focus of interest in a study even if a more comprehensive categorical value specification of its [`developmental stage`](http://www.ebi.ac.uk/efo/EFO_0000399)  could have been posed as a Likert scale.

[//]: # (    Class: 'boolean value specification'
        subClassOf 'has specified value' only xsd:boolean
)
[//]: # (        subClassOf 'boolean value specification')

    Class: 'neonate value specification'
        subClassOf 'value specification'
        subClassOf 'has specified value' only xsd:boolean
        subClassOf 'specifies value of' only 'neonate' 

Any categorical value specification choice instance can potentially be interpretable as a boolean too.

## Ordinal

OBI does not currently have a recommendation about how to define an ordered categorical variable. A ranking data property for each choice could be used; or potentially previous/next relations could be established between choices.

## Numeric

Currently all numeric value specifications are handled under the [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931) term, which implies that each must have a unit as well. 

 OWL introduced the owl:real data type as the most generic numeric type, and owl:rational as its subbordinate. Under owl:rational is xml:decimal, the general basis of more specific integer and float datatypes; numeric conversion appears to be smooth between these types. Any number type can be paired with a unit as described below. 

OBI currently does not provide functionality for dealing with numeric precision or error range. 

### Decimal

[//]: # (        Class 'decimal value specification'
        subClassOf 'has specified value' only xsd:decimal
)
[//]: # (        subClassOf 'decimal value specification')

Here the pH acidity scale is effectively characterized as a decimal between 0.0 and 14.0:

    Class 'ph value specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only 'pH' 
        subClassOf 'specifies value of' only 'pH measurement'
        subClassOf 'has specified value' only xsd:decimal[ >=0, <=14 ]))

Note that the Protege axiom editor can be very fussy about exactly how the >,>=,<,<= comparators are positioned with spaces with respect to brackets and numbers.

### Integer

Some variables are inherently integers - countable things that can't meaningfully have fractions except as intermediate calculations (quantities of water can be described in decimal to handle portions like 1.5 cups, while basepairs are not meaningful as fractions. Use xsd:integer where rounding during comparison won't be an issue.

[//]: # (    Class 'integer value specification'
        subClassOf 'has specified value' only xsd:integer
        subClassOf 'decimal value specification'
)
[//]: # (        subClassOf 'integer value specification')

    Class 'MIC diffusion measurement specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only 'millimeter' 
        subClassOf 'specifies value of' only 'MIC value'
        subClassOf 'has specified value' only xsd:integer[ >5 ,< 100]

(OWL actually provides access to further subclasses of integer such as xsd:positiveInteger, but OBI does not have a matching granularity of value specification classes.)

### Float

[//]: # (    Class 'float value specification'
        subClassOf 'decimal value specification'
        subClassOf 'has specified value' only xsd:float
)
[//]: # (        subClassOf 'float value specification')

    Class 'MIC dilution measurement specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only ('milligram per liter' or 'microgram per milliliter')
        subClassOf 'specifies value of' only 'MIC value'
        subClassOf 'has specified value' only xsd:float[ >=0.01f ,<= 2048.0f]


## Units
OBI uses the [`has measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039) relation to pair numeric scalar parameters with related units.  The [Units of Measurement Ontology](https://github.com/bio-ontology-research-group/unit-ontology) (UO) is the default unit ontology the OBOFoundry community uses, although there are other options<sup>2,3</sup>. It is left to a unit ontology to express the base units of the International System of Units, as well as compound units that have numerators and denominators sufficient for a problem space.

A value specification can select at a general level all the permissible units which underlying value specifications and their instances must conform to.

Units extend to countable things like nucleotide 'basepairs' and potentially even 'oranges' or 'fruit' etc. In this respect they indicate the aboutness of the value specification.

## Duration
A duration is a difference in time calculated from an interval of two time points. (Semantically the interval is about those points and the events they mark). Value specifications for date and time durations or intervals are generally handled by decimal value specifications with one or more time units attached to them. This allows for decimal fraction amounts, e.g. 2.5 days. An 'age since birth' value specification could be:

[//]: # (Class: 'duration value specification'
        subClassOf 'value specification'
        subClassOf 'specifies value of' only xsd:decimal
)
[//]: # (        subClassOf 'duration value specification')

    Class: 'age since birth value specification'
        subClassOf 'scalar value specification'
        subClassOf 'has specified value' only xsd:decimal
        subClassOf 'specifies value of' some 'age since birth'
        subClassOf 'has measurement unit label' only (year or month or day or hour)

## Datetime

Of XML's native date/time datatypes, OWL has currently adopted [xsd:date](http://www.datypic.com/sc/xsd11/t-xsd_date.html), [xsd:datetime](http://www.datypic.com/sc/xsd11/t-xsd_dateTime.html) (format [-]CCYY-MM-DDThh:mm:ss.sss[Z|(+||-)hh:mm] according to the ISO 8601 standard) and [xsd:dateTimeStamp](http://www.datypic.com/sc/xsd11/t-xsd_dateTimeStamp.html) (format CCYY-MM-DDThh:mm:ss.sss(Z||(+||-)hh:mm), i.e. time zone required) into its reasoning specification.  A Gregorian calendar 24 hour clock instant of time is used, and will be compared down to the second and timezone offset for xsd:dateTime/Stamp formats.
 
[//]: # (    Class: 'date value specification'
        subClassOf 'value specification'
        subClassOf 'has specified value' only xsd:date
)
[//]: # (        subClassOf 'date value specification')

    Class: 'hospital admission date specification'
        subClassOf 'scalar value specification'
        subClassOf 'has specified value' only xsd:date
        subClassOf 'specifies value of' only 'hospital admission date'

Often a need for date obfuscation arises when dealing with confidential data points. Pairing a unit such as year, month, day, hour etc. can convey the semantic granularity of the given xsd:datetime but won't have an effect on reasoner equality test, so the remainder of the datetime components need to be the same (zero'ed out for example) in order for an equality constraint to succeed.  This could be done as a pre-processing step.

If a more complex model of date/time is required, the "Time Ontology in OWL"<sup>4,5</sup> may suffice. 


## Missing values and other metadata

Data sources likely have a variety of ways to mark missing values. A food database example: “When the content of a food for a component is not known, a hyphen stands in place of the number. It is important for users to take into account these missing values and not to consider them as zero”<sup>6</sup>.  Currently, a simple way to express this is to have an instance of a value specification, but no 'has specified value' data property for it.

Other metadata may need to be marked e.g. how to deal with: “In some cases, a component is detected in the food matrix, but it cannot be quantified precisely. The analytical result can therefore be considered as ‘trace’.” Another case is where a data item exists but has been obfuscated for privacy reasons.  OBI does not currently have a metadata standard that addresses these cases.

## "Other" values

## Data Sets

A collection of datums of a given data type is called a [`data set`](http://purl.obolibrary.org/obo/IAO_0000100). A numeric data set (like a numeric spreadsheet column) can have statistical calculations performed on it by using an RDF query language like [SPARQL](https://en.wikipedia.org/wiki/SPARQL).  The [`member of`](http://purl.obolibrary.org/obo/RO_0002350) relation can connect datum or value specification instances to such a data set.

***
References: 

* https://github.com/obi-ontology/obi-legacy-svn/blob/master/trunk/src/examples/development/data-prototype.pdf
* https://mitpress.mit.edu/books/building-ontologies-basic-formal-ontology

***

<sup>2</sup>https://github.com/HajoRijgersberg/OM

<sup>3</sup>http://qudt.org/

<sup>4</sup>https://www.w3.org/2001/sw/BestPractices/OEP/Time-Ontology

<sup>5</sup>https://www.w3.org/TR/owl-time/

<sup>6</sup>https://ciqual.anses.fr/cms/sites/default/files/inline-files/TableCiqual2017_XML_docENG.pdf