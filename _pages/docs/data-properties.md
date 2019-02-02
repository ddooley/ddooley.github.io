---
layout: single
title: Data Properties
permalink: /docs/data-properties/
sidebar:
  nav: "docs"
---

### Questions: Allow "has specified value" to have domain of any ICE?  Or introduce "has value" implementation?

<img align="right" src="/assets/images/docs/data_lee_data_property_age.png">

An ontology data property is a relation from an entity instance straight to some literal datatype (xsd:decimal, xsd:string, xsd:anyURI, etc.) that is a measure/estimate of what that data property is about. Below, the `has age` data property (which doesn't exist in OBI) tells us that Lee's age is 12.

<br clear="both">

<img align="right" src="/assets/images/docs/data_lee_data_property_ages.png">

The label of the data property tells humans in hopefully plain language what the value is about, but a computer will have a bad time guessing what the relation is equivalent to in other graphs that have differently named or identified relations, which spells trouble for data sharing unless the roster of data properties is already agreed upon.  The problem is magnified if other age quantities are involved.

<br clear="both">

<img align="right" src="/assets/images/docs/data_age_measurement_datums.png">

In fact there are many kinds of [`ages`](http://purl.obolibrary.org/obo/OBI_0001167) in the biomedical realm, as exemplified to right. We're either faced with creating a litany of data properties, or of trying another approach to differentiate the measurements and their semantics. OBI has chosen a data modelling vocabulary that focuses on describing a core entity's role, quality, information content and other descriptive components rather than having more semantically opaque data properties connected to it. Below is an example focusing on providing values for information content entities connected to an entity instance.

<img src="/assets/images/docs/data_lee_has_specified_value.png">

<img src="/assets/images/docs/data_lee_object_property_ages.png">

Data properties are frequently used when only the capabilities of xsd:PlainLiteral data types are needed. 

OBI uses data properties in a very limited way, via `has value`, `has measurement value`, and `has specified value`, and `has specified numeric value`, with the latter two described in the `value specification section`.  To explain why, we'll look at how to use object and data properties to represent data.


Although a common approach with other ontologies, a data property connected directly to an entity has little semantic detail - limited to a few attributes (functional, domain, and range constraints) and one of the stock xml literal datatypes - xsd:decimal, xsd:string, xsd:anyURI, etc. (and possibly some OWL facet constraints on those). The rest of its "meaning" is carried only in its label.  

So how does OBI get any semantic mileage out of just these four data properties?  OBI's approach is to focus on expressing each entity attribute (a quality or ICE) by using fairly generic object properties that explain their `aboutness`, and connecting those attributes in turn to literal values.  Rather than establish a `has age` data property, we express that [`age`](http://purl.obolibrary.org/obo/PATO_0000011) is a quality of our entity, and then focus on defining the semantics it and its subclasses and datums - [`age since fertilization measurement datum`](http://purl.obolibrary.org/obo/OBI_0001168), [`age since birth measurement datum`](http://purl.obolibrary.org/obo/OBI_0001169) etc. 

In this way a plethora of named data properties and object properties is avoided, as shown below for street address, email address, and social security number attributes.  We did not need to invent 'has email address', has 'social security number', etc. data properties or object properties. We drew instead from OBI's `has value` data property and generic RO relations.  This reduces the amount of language needed to describe entities, at the cost of a bit more structure. *Most importantly it enables entities to be the focus of semantic elaboration (axioms) rather than being surrounded by opaque relations.* The `aboutness` details have the extra benefit of facilitating appropriate data exchange between ontology-driven systems.  By specifying that a string field is about a first name or a last name, maiden name, full name, SIN number, postal code, etc. this then provides the core 'aboutness' information that guides the merging and federated querying of triple store graphs.

<br clear="both">

Suitable object properties:

- 'inheres in' object property if ...???
- 'denotes' if the ICE is a type of identifier, such as a [`centrally registered identifier symbol`](http://purl.obolibrary.org/obo/IAO_0000577) like a [`specimen identifier`](http://purl.obolibrary.org/obo/OBI_0001616) or a NCIT [`identifier`](http://purl.obolibrary.org/obo/NCIT_C25364) for example.
- 'location of' if the literal value X is locating the given entity by a geospatial reference. ????

## Limitations

There are however value details that a `has ... value` data property can't do by itself as the following examples illustrate, and that are resolved by the introduction of a `value specification` entity (described in the next section.)

<img align="right" src="/assets/images/docs/data_lee_data_properties.png">

- Data property values don't support units directly. In the example diagram of Lee's data properties to right, is the `has weight` decimal value given in kilos or grams? Is height in meters or centimetres? Either assumptions are made about units associated with a data property, or a second set of data properties must be created to capture unit info.  Value specifications allow units to be expressed explicitly.

- A data property doesn't support a relevant time of measurement value.  For example, when was Lee's `has height` observed, and was it the same time as `has weight`, such that an accurate BMI can be calculated?  Admittedly, time differentiated data is rather complex to model in OWL. A pragmatic approach, if workable, is to only expose to an OWL reasoner data that doesn't need to be differentiated by time. In the BMI example, we could assume height and weight data properties are adequately close in time that derivative calculations are ok. OBI does offer annother approach detailed in the `Time-stamped data` section to describe n-dimensional points that include time.

- A data property cannot directly specify the range of ontology term choices (which are classes or individuals) for a categorical value since data property ranges can only be drawn from xml/rdf data types. "anon:Lee `has handedness` "http://purl.obolibrary.org/obo/PATO_0002201^^xsd:anyURI"" but the URI could point to anything on the internet. We can't express in OWL that the 'has handedness' data property URI range must fall within the class of PATO `handedness`.

To answer the above needs, OBI introduced an additional `value specification` entity, as detailed in the next section.