---
layout: single
title: Data Types
permalink: /docs/data-types/
toc: true
sidebar:
  nav: "docs"
---

[//]: # (Please put comments like this one into the text to communicate with other OBI-ers)

[//]: # (OWL-driven reasoning and SPARQL querying can be applied to data represented in a graph to compare sets of specimen qualities or phenotypes like weight, length, life stage, handedness, and other dimensions.) 

OWL inherits most of RDF's ability to specify XML string, numeric, datetime, and URI datatype values as data properties of an entity, and can compare data properties across entities (see [here](https://www.w3.org/TR/xmlschema-2/) and [here](https://www.w3.org/TR/swbp-xsch-datatypes){:target="_blank"}).  OWL can also be used to specify constraints on string value length and content, and can specify numeric bounds on numbers.  OBI currently focuses on reuse of RDF/XML datatypes to capture experimental data.  Those who need further functionality may find other datatype representations useful (e.g. [here](https://www.sciencedirect.com/science/article/pii/S0020025515005800){:target="_blank"}). 

Here a handful of the primitive datatypes from RDF which are used in OWL are discussed. The possibility of [user defined datatypes](https://www.w3.org/TR/swbp-xsch-datatypes/#sec-userDefined){:target="_blank"} is avoided in favour of using enhanced value specifications to do the same work.  Some examples below are expressed directly in OBI, while others can be constructed in an application ontology that draws on OBI components.  Although OWL 2.0 isn't suitable for doing all types of validation, we have shown how value specifications can be enhanced with basic numeric range and string content restrictions.


## Missing values

Data sources likely have a variety of ways to mark missing values. A food database example: “When the content of a food for a component is not known, a hyphen stands in place of the number. It is important for users to take into account these missing values and not to consider them as zero”<sup>6</sup>.  Currently, a simple way to express this is to have an instance of a value specification, but no 'has specified value' data property for it.

## Other metadata

Other metadata may need to be marked e.g. how to deal with: “In some cases, a component is detected in the food matrix, but it cannot be quantified precisely. The analytical result can therefore be considered as ‘trace’” (see [here](<sup>6</sup>https://ciqual.anses.fr/cms/sites/default/files/inline-files/TableCiqual2017_XML_docENG.pdf){:target="_blank"}). Another case is where a data item exists but has been obfuscated for privacy reasons.  OBI does not currently have a metadata standard that addresses these cases.

## "Other" values

## Data Sets

A collection of datums of a given data type is called a [`data set`](http://purl.obolibrary.org/obo/IAO_0000100){:target="_blank"}. A numeric data set (like a numeric spreadsheet column) can have statistical calculations performed on it by using an RDF query language like [SPARQL](https://en.wikipedia.org/wiki/SPARQL).  The [`member of`](http://purl.obolibrary.org/obo/RO_0002350){:target="_blank"} relation can connect datum or value specification instances to such a data set.

