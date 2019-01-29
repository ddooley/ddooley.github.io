---
layout: single
title: Categorical Datum
permalink: /docs/data-categorical/
toc: true
sidebar:
  nav: "docs"
---

A categorical value specification is a flat list or hierarchic tree structure containing a finite number of pre-determined choices. Here we provide for choices whose values are either a controlled list of xsd:string strings, or xsd:anyURI references to ontology terms.

### Categorical ontology choice

Categorical choice lists or trees of ontology terms (e.g. of organism taxonomy, of disease, etc.) are often used in datums and experimental metadata. The aim here is to point to existing ontology class or instance identifiers within existing ontologies as selections for a categorical variable. 

<img align="right" src="/assets/images/docs/data_john_sex_property.png">

The 'has quality' relation can capture this directly by pointing straight to the phenotypic quality, for example "male" is a subclass of "phenotypic sex", and one can express "An anonymous node of type Homo sapiens (representing John) 'has quality' another anonymous node of type 'male'".

<br clear="both">

One can detail which assay was used to make this assessment:

<img src="/assets/images/docs/data_john_sex_process.png">

<img align="right" src="/assets/images/docs/data_john_sex_vs.png">

If we involve a categorical value specification, we can point to the possible choices (which will vary depending on experimental protocol):

<br clear="both">

The complete contextual view:

<img src="/assets/images/docs/data_john_sex_context.png">

## Other approaches

You may see other ontologies might promote the use of a specially defined **object** property:

<img align="right" src="/assets/images/docs/data_john_sex_op.png">

Here "has phenotypic sex" would be an object property existing between a BFO independent continuent entity (the bearer) and a specifically dependent continuent (in this case, a quality) that is about an organism's sexuality. The quality is represented as a categorical value.

And other ontologies may allow a string value (or coded number) via a specially defined **data** property. Here a general data property containing a regular expression constrains possible values of a categorical variable.

<img align="right" src="/assets/images/docs/data_john_sex_dp.png">
Here "has phenotypic sex" is a data property existing between a BFO independent continuent entity (a physical organism) and some kind of string literal representing its sexuality. For analysis to succeed, the literals must be normalized to desired categorical values of sexuality, especially where merging with other graphs is likely.

<br clear="both">

In a different approach, an OBI example using categorical value specification focuses on describing a tumor grading standard [`histologic grade according to AJCC 7th edition`](http://purl.obolibrary.org/obo/OBI_0002205){:target="_blank"}.  Here the value specification class has individuals which are each interpreted as grades, and which could potentially be augmented with data properties that detail their assessment differentiae.  This approach is suited to cases where selections are not already established (and would not be in the future) as ontology classes situated within their own hierarchic context. 

Alternately one could use the `specifies value of` relation to point to existing categorical choices (qualities, etc.):
<!-- 
[//]: # (        subClassOf 'categorical ontology value specification')
-->

    Class: 'handedness value specification'
        subClassOf 'categorical value specification'
        subClassOf 'specifies value of' only handedness

Now an instance of `handedness value specification` can have a **`specifies value of`** axiom pointing to a `handedness` class instance. This involves some extra setup because all `handedness` selections need to be "**punned**" since they can't be referenced directly as classes. In other words an individual needs to be created to mirror each categorical choice, so for example classes for left handedness, right handedness, ambidextrous handedness all need mirrored individuals - and in this case these are not native to the PATO ontology that the classes originate from. (Punning is accomplished manually in Protege by copying an existing class URI into the "Create a new Named individual" form, with the "new entity options ..." set to expect a user supplied name.  This preserves the same identifier for both class and individual).

[//]: # (Is punning somehow automated so that loading an ontology with [individual x] `specifies value of` [Class y] causes Class y to be punned automatically? )

[//]: # (A simplified model could shift the burden of choice enumeration directly to value specification. )

[//]: # (Note that as future versions of a standard occur, it may be feasible to attach individuals of past standards to them if no semantics have changed, thus simplifying data analysis.)

## Unworkable , REVISE

However, some complications arise which the following example will explore.  We could try to capture a [`handedness`](http://purl.obolibrary.org/obo/PATO_0002201){:target="_blank"} quality with:

    Class: 'handedness value specification'
        subClassOf 'categorical value specification'
        subClassOf 'has specified value' only handedness 

However, this is not permitted in OWL since **`has specified value`** data property can only have a literal on the right side. The target could be expressed simply as "`has specified value` only xsd:anyURI", thus allowing values like xsd:anyURI [right-handedness](http://purl.obolibrary.org/obo/PATO_0002203){:target="_blank"} but this then requires some validation mechanism external to an OWL reasoner for limiting categorical values. The Class doesn't indicate what the choices are.


[//]: # (Slightly different from a boolean value specification below, a binary value specification is a categorical value specification with only two choices.)

### Categorical string choice

If a string must conform to a smaller set of choices, and nothing more needs to be axiomatized about each choice, then this can be accomplished with a value specification that is both string and categorical.  The value specification has a 'has specified value' component which uses a regular expression to enumerate the permitted strings. Note that in this approach one cannot easily provide other information (label, description) about choice in a user interface.

For example, an "E-coli K antigen value specification" can be represented as:

    Class: 'E-coli K antigen value specification'
        subClassOf 'categorical value specification'
        subClassOf 'specifies value of' only 'K antigen'
        subClassOf 'has specified value' only xsd:string[pattern "K(1|2a|2ac|3|4|5|6|7|8|9|10|11|12|13|14|15|16|18a|18ab|19|20|22|23|24|26|27|28|29|30|31|34|37|39|40|41|42|43|44|45|46|47|49|50|51|52|53|54|56|96|55|74|82|84|85ab|85ac|87|92|93|95|97|98|100|101|102|103|X104|X105|X106)"]]

This allows a reasoner to raise the unsatisfiable alarm when an instance of `E-coli K antigen value specification`  `has specified value` 'K17a'.

One can potentially leave the `has specified value` axiom out, in which case validation enforcement would need to occur outside the OWL reasoning context.

Note that in the past OBI used/tried [`categorical measurement datum`](http://purl.obolibrary.org/obo/OBI_0000938){:target="_blank"} for enumerating categorical choices, with a [`has category label`](http://purl.obolibrary.org/obo/OBI_0000999){:target="_blank"} object property that linked to a set or class of permissible terms (as shown in OBI's existing `handedness value specification` example). This class and relation is being discouraged in favour of the categorical value specification approach.


### Ordinal

OBI does not currently have a recommendation about how to define an ordered categorical variable. A ranking data property for each choice could be used; or potentially previous/next relations could be established between choices.
