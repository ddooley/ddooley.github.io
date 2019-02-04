---
layout: single
title: String Datums
permalink: /docs/data-string/
toc: true
sidebar:
  nav: "docs"
---


## ISSUE: *Can we allow identifier string values in value specification? See: [issue 985](https://github.com/obi-ontology/obi/issues/985){:target="_blank"}*


"Free text" string data are often not amenable to data analysis by OWL reasoning unless the values happen to be categorical (see [`categorical`](/docs/data-categorical/){:target="_blank"} data section).  This includes strings like "20g" which haven't been parsed into their numeric and unit components. These can be recorded in an annotation for a given entity ICE component; OBI is currently discussing adding a `has representation` annotation to serve this purpose (see issue [`#985`](https://github.com/obi-ontology/obi/issues/985){:target="_blank"}).

Textual identifiers that act as keys to unify records can be useful - these might include alphanumeric health care identifiers, postal codes, or the scientific taxonomic names of plants and animals. The following detail mainly pertains to validating strings that operate as keys having a particular format which should encourage data standardization. 

An OWL data property can hold a string as a plain literal with an optional language tag (see [here](https://www.w3.org/2007/OWL/wiki/PlainLiteral){:target="_blank"} ). String length constraints can also be set via "length", "minLength" and "maxLength" parameters, e.g. "xsd:string[length "5"^^xsd:integer]. A "pattern" parameter is available which supports [regular expression](https://www.regular-expressions.info/xml.html){:target="_blank"} syntax to some extent, allowing "[0-9] [a-z] [A-Z] . ? * + {m,n}" components.

For example, one can construct the following representation to store and validate international postal codes generally, and the US Zip Code subclass (a string of 5 digits). 

<!--
[//]: # (        Class: 'string value specification'        subClassOf 'has specified value' only xsd:string)

[//]: # (        subClassOf 'string value specification')
-->

    Class: 'postal code specification'
        subClassOf 'value specification'
        subClassOf 'has specified value' only xsd:string[pattern "[0-9A-Za-z \-]{2,10}"]

    Class: 'ZIP code specification'
        subClassOf 'postal code specification'
        subClassOf 'specifies value of' some ('postal code' and 'is about' some (site and 'located in' some 'United States of America')
        subClassOf 'has specified value' only xsd:string[pattern "[0-9]{5}"]

Fairly well-validated [`email addresses`](http://purl.obolibrary.org/obo/IAO_0000429){:target="_blank"} can be expressed using:

<!--
[//]: # (        subClassOf 'string value specification')
-->

    Class: 'email address specification'
        subClassOf 'value specification'
        subClassOf 'specifies value of' only 'email address' 
        subClassOf 'has specified value' only xsd:string[pattern "[A-Za-z0-9]+([_.\-][A-Za-z0-9]+)*\@[A-Za-z0-9]+([.\-][A-Za-z0-9]+){1,3}"]

Note one quirk: In pattern matching, the "@" character must be escaped or else the remainder of test string is ignored (i.e. "@" is interpreted as a language facet addition to the string).  Also more work is required to cover possible validation of [international / UTF-8 strings](https://www.regular-expressions.info/unicode.html){:target="_blank"}.
