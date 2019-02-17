---
layout: default
title: Numeric Datums
permalink: /docs/data-numeric/
toc: true
sidebar:
  nav: "docs"
---

OWL introduced the owl:real data type as the most generic numeric type, and owl:rational as its subbordinate. Under owl:rational is xml:decimal, the general basis of more specific integer and float datatypes; numeric conversion appears to be smooth between these types. Any number type can be paired with a unit as described below. 

OBI generally has two ways to represent a datum's numeric value, depending on whether or not a unit needs to be included.  The simple, unit-less case can be handled by the numeric "has xsd:real" or subordinate "has xsd:decimal" or "has xsd:integer" data properties.  This makes sense for dimensionless numbers like counts.

OBI currently also shows that datums can have a `has measurement unit label`
Currently all numeric value specifications are handled under the [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931){:target="_blank"}{:target="_blank"} term, which implies that each must have a unit as well. 


OBI currently does not provide functionality for specifying numeric precision or error range. 

### Decimal

A [`pH measurement datum`](http://purl.obolibrary.org/obo/GENEPIO_0001736) is an example of a dimensionless measure that nevertheless has a unit: [`pH`](http://purl.obolibrary.org/obo/UO_0000196).  One could choose not to make the unit mandatory in this case, as there is no alternate unit possibility, in which case a simple data property will do:



Here an example class one could compose  for collecting a pH acidity measurement, using the Unit Ontology's  [`pH`](http://purl.obolibrary.org/obo/UO_0000196) unit, and GenEpiO's [`pH measurement`](http://purl.obolibrary.org/obo/GENEPIO_0001736). 

    Class 'ph value specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only 'pH' 
        subClassOf 'specifies value of' only 'pH measurement'
        subClassOf 'has specified value' only xsd:decimal

As it stands however, this accepts pH values greater than 14, which are usually experimentally out of bounds. To ensure pH acidity scale is limited to a decimal between 0.0 and 14.0, substitute this `has specified value` axiom into the definition above:

        subClassOf 'has specified value' only xsd:decimal[ >=0, <=14 ]))

This places upper and lower limits on the decimal - called facet restrictions (see [here](https://www.w3.org/TR/owl2-quick-reference/#Facets) and [here](https://www.w3.org/TR/owl2-syntax/#Datatype_Maps) - and will trigger an unsatisfiability error when a reasoner encounters instance triples that violate the range. This level of validation may not be necessary for your modelling purposes, but it can help to standardize data sharing.

Note that the Protege axiom editor can be very fussy about exactly how the constraint comparators (>,>=,<,<=) are positioned with spaces with respect to brackets and numbers.

### Integer

Some variables are inherently integers - countable things that can't meaningfully have fractions except as intermediate calculations (quantities of water can be described in decimal to handle portions like 1.5 cups, while basepairs are not meaningful as fractions. Use xsd:integer where rounding during comparison won't be an issue. Here we define a minimum inhibitory concentration measurement (MIC) to measure the performance of an antimicrobial agent against the growth of a bacterium.

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
        subClassOf 'has specified value' only xsd:integer

Again, if you want to ensure a numeric range that validates data, substitue this line into the above:

        subClassOf 'has specified value' only xsd:integer[ >5 ,< 100]

OWL also allows access to subclasses of integer such as xsd:positiveInteger.

### Float

<!--
[//]: # (    Class 'float value specification'
        subClassOf 'decimal value specification'
        subClassOf 'has specified value' only xsd:float
)
[//]: # (        subClassOf 'float value specification')
-->

This MIC dilution (different from diffusion above) can be measured with a floating point number which should always be >= .015 mg/L and <= 2048.0 .

    Class 'MIC dilution measurement specification'
        subClassOf 'scalar value specification'
        subClassOf 'has measurement unit label' only ('milligram per liter' or 'microgram per milliliter')
        subClassOf 'specifies value of' only 'MIC value'
        subClassOf 'has specified value' only xsd:float[ >=0.015f ,<= 2048.0f]


## Units

OBI uses the [`has measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039){:target="_blank"} relation to pair numeric scalar parameters with related units.  The [Units of Measurement Ontology](https://github.com/bio-ontology-research-group/unit-ontology){:target="_blank"} (UO) is the default unit ontology the OBOFoundry community uses, although there are other options (e.g. [QUDT](http://qudt.org/){:target="_blank"}, [OM](https://github.com/HajoRijgersberg/OM){:target="_blank"}). It is left to a unit ontology to express the base units of the International System of Units, as well as compound units that have numerators and denominators sufficient for a problem space.

A value specification can select at a general level all the permissible units which underlying value specifications and their instances must conform to.

Units extend to countable things like nucleotide 'basepairs' and potentially even 'oranges' or 'fruit' etc. In this respect they indicate the aboutness of the value specification.

A particular datum may be allowed a choice of unit, for example age may be measured in years, months, days, or hours.  Value specifications can support a choice of units (as can be seen in the [`duration`](/docs/data-time/#duration) example, but OWL does not have a unit-quantity conversion mechanism - that normalization must be done directly on a triple store or at point of data entry.

