---
layout: single
title: Value specification vs data property
permalink: /docs/vs-vs-dp/
sidebar:
  nav: "docs"
---
Using value specifications to record the values of entity qualities and other measurables reduces the need for a plethora of data properties. Rather than establish a `has age` data property, we express a value specification about age.  Both hold a value, but the latter allows us to focus on defining the semantics of the quality [`age`](http://purl.obolibrary.org/obo/PATO_0000011) and its subclasses and datums - [`age since fertilization measurement datum`](http://purl.obolibrary.org/obo/OBI_0001168), [`age since birth measurement datum`](http://purl.obolibrary.org/obo/OBI_0001169) etc. 

A data property is analogous to a kind of compressed and semantically opaque value specification because a data property's semantic detail is limited to a few attributes (functional, domain, and range constraints).  

## NOT YET TRUE !!!:

<img src="/assets/images/docs/data_lee_has_value.png">
*Shall we allow including ICE values directly, avoiding 'value specification' and just using **a new 'has value' data property** to connect an ICE to a value?*

*OBI provides a generic `has value`* data property that connects an instance of a quality or an information content entity to a literal value. This is a simple way to record a value that doesn't need anything more than one of the stock xml literal datatypes - xsd:decimal, xsd:string, xsd:anyURI, etc. in a process or data model.  Attach the quality or ICE to the entity it pertains to via. 'bearer of' object property. This may provide enough information to enable comparison when units are not involved, and to facilitate data exchange.*

Here are cases where we promote value specifications over data properties:

<img align="right" src="/assets/images/docs/data_lee_data_properties.png">

- Data property values don't support units directly. In the example diagram of Lee's data properties to right, is the `has weight` decimal value given in kilos or grams? Is height in meters or centimetres? Either assumptions are made about units associated with a data property, or a second set of data properties must be created to capture unit info.  Value specifications allow units to be expressed explicitly.

- A data property doesn't support a relevant time of measurement value.  For example, when was Lee's `has height` observed, and was it the same time as `has weight`, such that an accurate BMI can be calculated?  Admittedly, time differentiated data is rather complex to model in OWL. A pragmatic approach, if workable, is to only expose to an OWL reasoner data that doesn't need to be differentiated by time. In the BMI example, we could assume height and weight data properties are adequately close in time that any derivative calculations are appropriate. OBI does offer annother approach detailed in the `Time-stamped data` section.

- A data property cannot directly specify the range of ontology term choices (which are classes or individuals) for a categorical value since data property ranges can only be drawn from xml/rdf data types. "anon:Lee `has handedness` "http://purl.obolibrary.org/obo/PATO_0002201^^xsd:anyURI"" but the URI could point to anything on the internet. We can't express in OWL that the 'has handedness' data property URI range must fall within the class of PATO `handedness`.

- A string field like "name" may not be involved in one's process modelling per se.  However, there is a data harmonization use case that motivates adding extra detail to such a field by way of a value specification. If we can specify that a string field is about a first name or a last name, maiden name, full name, SIN number, postal code, etc. this then provides the core 'aboutness' information that guides the merging and federated querying of triple store graphs.

- If one does 

For these reasons, OBI has a handful of data properties (including `has specified value`), and a larger and growing set of measurement / setting / prediction datums and the material entity qualities that they are about, complements of PATO and other ontologies.

Below, categorical value specifications are referenced, units are provided, and qualities of parts of organisms are unambiguously described without resorting to data properties.

<img align="right" src="/assets/images/docs/data_lee_properties_as_vs.png">

***EDITOR NOTE***

*This diagram doesn't show instance level data. should it?*



