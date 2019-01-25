---
layout: single
title: Categorical Datum
permalink: /docs/data-categorical/
toc: true
sidebar:
  nav: "docs"
---

A categorical value specification is a flat list or hierarchic tree structure containing a finite number of pre-determined choices. Here we provide for choices whose values are either xsd:string or xsd:anyURI references to ontology terms.

### Categorical ontology choice

Categorical choice lists or trees of ontology terms (e.g. of organism taxonomy, of disease, etc.) essentially have an xsd:anyURI datatype since a selection is an ontology URI. The aim here is to point to existing ontology class or instance identifiers within one's application ontology and/or imported from 3rd party ontologies as selections for a categorical variable. However, some complications arise which the following example will explore.  We could try to capture a [`handedness`](http://purl.obolibrary.org/obo/PATO_0002201){:target="_blank"} quality with:

    Class: 'handedness value specification'
        subClassOf 'categorical value specification'
        subClassOf 'has specified value' only handedness 

However, this is not permitted in OWL since **`has specified value`** data property can only have a literal on the right side. The target could be expressed simply as "`has specified value` only xsd:anyURI", thus allowing values like xsd:anyURI [right-handedness](http://purl.obolibrary.org/obo/PATO_0002203){:target="_blank"} but this then requires some validation mechanism external to an OWL reasoner for limiting categorical values. The Class doesn't indicate what the choices are.

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

*Note that in the past OBI used/tried [`categorical measurement datum`](http://purl.obolibrary.org/obo/OBI_0000938){:target="_blank"} for enumerating categorical choices, with a [`has category label`](http://purl.obolibrary.org/obo/OBI_0000999){:target="_blank"} object property that linked to a set or class of permissible terms (as shown in OBI's existing `handedness value specification` example). This class and relation is being discouraged in favour of the categorical value specification approach.*

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

## Ordinal

OBI does not currently have a recommendation about how to define an ordered categorical variable. A ranking data property for each choice could be used; or potentially previous/next relations could be established between choices.
