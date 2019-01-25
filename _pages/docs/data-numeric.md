---
layout: single
title: Numeric Datums
permalink: /docs/data-numeric/
toc: true
sidebar:
  nav: "docs"
---

## Numeric

Currently all numeric value specifications are handled under the [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931) term, which implies that each must have a unit as well. 

 OWL introduced the owl:real data type as the most generic numeric type, and owl:rational as its subbordinate. Under owl:rational is xml:decimal, the general basis of more specific integer and float datatypes; numeric conversion appears to be smooth between these types. Any number type can be paired with a unit as described below. 

OBI currently does not provide functionality for dealing with numeric precision or error range. 

### Decimal

<!--
[//]: # (        Class 'decimal value specification'
        subClassOf 'has specified value' only xsd:decimal
)
[//]: # (        subClassOf 'decimal value specification')
-->

Here the pH acidity scale is effectively characterized as a decimal between 0.0 and 14.0:

    Class 'ph value specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only 'pH' 
        subClassOf 'specifies value of' only 'pH measurement'
        subClassOf 'has specified value' only xsd:decimal[ >=0, <=14 ]))

Note that the Protege axiom editor can be very fussy about exactly how the >,>=,<,<= comparators are positioned with spaces with respect to brackets and numbers.

### Integer

Some variables are inherently integers - countable things that can't meaningfully have fractions except as intermediate calculations (quantities of water can be described in decimal to handle portions like 1.5 cups, while basepairs are not meaningful as fractions. Use xsd:integer where rounding during comparison won't be an issue.

<!-- 
[//]: # (    Class 'integer value specification'
        subClassOf 'has specified value' only xsd:integer
        subClassOf 'decimal value specification'
)
[//]: # (        subClassOf 'integer value specification')
-->

    Class 'MIC diffusion measurement specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only 'millimeter' 
        subClassOf 'specifies value of' only 'MIC value'
        subClassOf 'has specified value' only xsd:integer[ >5 ,< 100]

(OWL actually provides access to further subclasses of integer such as xsd:positiveInteger, but OBI does not have a matching granularity of value specification classes.)

### Float

<!--
[//]: # (    Class 'float value specification'
        subClassOf 'decimal value specification'
        subClassOf 'has specified value' only xsd:float
)
[//]: # (        subClassOf 'float value specification')
-->

    Class 'MIC dilution measurement specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only ('milligram per liter' or 'microgram per milliliter')
        subClassOf 'specifies value of' only 'MIC value'
        subClassOf 'has specified value' only xsd:float[ >=0.01f ,<= 2048.0f]

