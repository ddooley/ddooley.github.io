---
layout: single
title: Categorical Datum
permalink: /docs/data-categorical/
toc: true
sidebar:
  nav: "docs"
---

A categorical value is a selection from a flat list or hierarchic tree structure containing a finite number of pre-determined choices ranging from organisms in a taxonomy, diseases, countries of the world or levels of an experimental variable.  Here we provide for choices whose values are either ontology terms, or a controlled set of literal xsd:string strings.

### Categorical ontology choice

The aim here is to provide a way to point to an ontology class or instance identifiers within existing ontologies as selections for a categorical variable.

<img align="right" src="/assets/images/docs/data_john_sex_property.png">

The 'has quality' relation can capture this directly by pointing straight to the phenotypic quality, for example "male" is a subclass of "phenotypic sex", and one can express "An anonymous node of type Homo sapiens (representing John) 'has quality' another anonymous node of type 'male'".

<br clear="both">

One can detail which assay was used to make this assessment:

<img src="/assets/images/docs/data_john_sex_process.png">

<img align="right" src="/assets/images/docs/data_john_sex_vs.png">

A categorical value specification can point to the possible choices (which will vary depending on experimental protocol):

<br clear="both">

The complete contextual view:

<img src="/assets/images/docs/data_john_sex_context.png">

In a different approach, an OBI example using categorical value specification focuses on describing a tumor grading standard [`histologic grade according to AJCC 7th edition`](http://purl.obolibrary.org/obo/OBI_0002205){:target="_blank"}.  Here the value specification class has individuals which are each interpreted as grades, and which could potentially be augmented with data properties that detail their assessment differentiae.  This approach is suited to cases where selections are not already established (and would not be in the future) as ontology classes situated within their own hierarchic context. 

## Complications - punning

A left/right/ambidextrous handedness example shows some complications one can run into visa vis classes and instances / individuals.

    Class: 'handedness value specification'
        subClassOf 'categorical value specification'
        subClassOf 'specifies value of' only handedness

Following this pattern, an instance of `handedness value specification` can have a **`specifies value of`** axiom pointing to a `handedness` class instance. This involves some extra setup because each `handedness` instance selection can't be referenced directly as a class - it needs to be "**punned**". In other words an individual needs to be created to mirror each categorical choice, so for example classes for left handedness, right handedness, ambidextrous handedness all need mirrored individuals - and in this case these are not native to the PATO ontology that the classes originate from. (Punning is accomplished manually in Protege by copying an existing class URI into the "Create a new Named individual" form, with the "new entity options ..." set to expect a user supplied name.  This preserves the same identifier for both class and individual). 

**As well Protege, when opening a file and encountering an object property with an instance reference at one end and a class reference at the other, will automatically create an instance for the class, and give it the same ontology URI identifier. This eliminates reasoning errors that would otherwise arise, but also means you may end up with namedIndividual instances you didn't manually create.**   A TRUE CHARACTERIZATION ???

The target could be expressed simply as "`has specified value` only xsd:anyURI", thus allowing values like xsd:anyURI [right-handedness](http://purl.obolibrary.org/obo/PATO_0002203){:target="_blank"} but this then requires some validation mechanism external to an OWL reasoner for limiting categorical values.

[//]: # (Slightly different from a boolean value specification below, a binary value specification is a categorical value specification with only two choices.)

### Categorical string choice

If a string must conform to a smaller set of choices, and nothing more needs to be axiomatized about each choice, then this can be accomplished with a value specification that is both string and categorical.  The value specification has a 'has specified value' component which uses a regular expression to enumerate the permitted strings. Note that in this approach one cannot easily provide other information (label, description) about choice in a user interface.

For example, an "E-coli K antigen value specification" can be represented as:

    Class: 'E-coli K antigen value specification'
        subClassOf 'categorical value specification'
        subClassOf 'specifies value of' only 'K antigen'
        subClassOf 'has specified value' only xsd:string[pattern "K(1|2a|2ac|3|4|5|6|7|8|9|10|11|12|13|14|15|16|18a|18ab|19|20|22|23|24|26|27|28|29|30|31|34|37|39|40|41|42|43|44|45|46|47|49|50|51|52|53|54|56|96|55|74|82|84|85ab|85ac|87|92|93|95|97|98|100|101|102|103|X104|X105|X106)"]]

This allows a reasoner to raise the unsatisfiable alarm when an instance of `E-coli K antigen value specification`  `has specified value` 'K17a'.

One can potentially leave the classes `has specified value` axiom out, in which case validation enforcement would need to occur outside the OWL reasoning context. (This is especially true if the computation load of validation by reasoner is too high.)

Note that in the past OBI used/tried [`categorical measurement datum`](http://purl.obolibrary.org/obo/OBI_0000938){:target="_blank"} for enumerating categorical choices, with a [`has category label`](http://purl.obolibrary.org/obo/OBI_0000999){:target="_blank"} object property (see OBI's existing `handedness value specification` example), but this class and relation is being discouraged.

### Ordinal Variables

OBI does not currently have a recommendation about how to define an ordered categorical variable. A ranking data property for each choice could be used; or potentially previous/next relations could be established between choices.

## "Other" values

A qualitative survey question may canvass users for an open-ended response if the given selections are inadequate or should be elaborated on. OBI would require a separate string value specification to capture this input.

## Other approaches

Other ontologies might use their own **object properties**, which OBI avoids (see [reasons](https://ddooley.github.io/docs/data-properties/)).

<img align="right" src="/assets/images/docs/data_john_sex_op.png">

Here `has phenotypic sex` would be an object property - a subclass of `has quality` - existing between a BFO independent continuent entity (the bearer) and a specifically dependent continuent that is about an organism's sexuality. The quality is represented as a categorical value. The range of `has phenotypic sex` can be constrained to PATO `phenotypic sex`.

Other ontologies may allow a string value (or number code) via a specially defined **data property**, a variant on `has specified value`. One could add a regular expression to validate a string to match possible values of a categorical variable as in above E-coli K antigen example.

<img align="right" src="/assets/images/docs/data_john_sex_dp.png">

Here `has phenotypic sex` is a data property existing between a BFO independent continuent entity (a physical organism) and a string literal code representing its sexuality. For axioms to work reliably with these values, the literals must be normalized to categorical values of sexuality.
