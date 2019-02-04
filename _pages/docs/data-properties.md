---
layout: single
title: Data Properties
permalink: /docs/data-properties/
sidebar:
  nav: "docs"
---

### Questions: Allow "has specified value" to have domain of any ICE?  Or introduce "has value" implementation?

This brings us to the collection of data - where specific protocols or instruments are used, generating data on particular scales and scientific units.  

FOR BJORN!: *First, OBI makes the distinction between values that can be placed directly on a categorical or numeric scale, and those that require some further parsing to extract atomic elements from, e.g. the strings "20g", "20 grams", and "0.02kg" which are the same quantity, but which differ by string comparison.  For this "undigested data" OBI provides a [`has representation`]() annotation that holds a string or a resource identifier which is not expected to play a direct role in OWL data-related axioms.*

<img align="right" src="/assets/images/docs/data_lee_data_property_age.png">

An ontology **`data property`** is a relation from an entity instance straight to some literal datatype value (an RDF number or string for example) that is a measure/estimate of what that data property is about. In an ontology one might find a `has age` data property used to express that Lee's age is 12, as shown to the right. OBI shies away from this approach, as explained below.  

<br clear="both">

<img align="right" src="/assets/images/docs/data_lee_data_property_ages.png">

The label of the data property tells humans in hopefully plain language what the value is about, but a computer will have a bad time guessing what the relation is equivalent to in other graphs that have differently named or identified relations that mean the same thing, which spells trouble for data sharing unless the roster of data properties is a common standard.  As shown, the problem is magnified if other age quantities are involved.

<br clear="both">

<img align="right" src="/assets/images/docs/data_age_measurement_datums.png">

In fact there are many kinds of [`ages`](http://purl.obolibrary.org/obo/OBI_0001167) in the biomedical and biological research realm; a number from OBI are listed here. Rather than creating a litany of data properties, OBI has chosen an alternative approach - a data modelling vocabulary that focuses on describing a core entity's role, quality, information content and other descriptive components rather than directly connecting semantically opaque data properties. **This is not to say non-OBI `data properties` are forbidden in application ontologies - but going through the exercise of defining them in terms of a generic BFO set of terms is a good exercise that may anticipate data conversion issues.**

Below is an example focusing on providing values for information content entities typically connected to a person instance.

<img src="/assets/images/docs/data_lee_has_specified_value.png">

OBI uses data properties in a limited way, via `has measurement value`,  `has specified value`, and `has specified numeric value`, and relies on the subject of the relation to provide `aboutness` semantics.  This approach reduces the amount of language needed to describe entities, at the cost of a bit more structure. *Most importantly it enables entities to be the focus of semantic elaboration (axioms) rather than being surrounded by opaque relations.* The `aboutness` details have the extra benefit of facilitating appropriate data exchange between ontology-driven systems.  By specifying that a string field is about a first name or a last name, maiden name, full name, SIN number, postal code, etc. this then provides the core 'aboutness' information that guides the merging and federated querying of triple store graphs.

## Missing values

Data sources may mark missing values in a variety of ways - by an empty string, or a hyphen instead of a number or date for example.  Instance subject-verb-object triples don't have an equivalent way to express this. However there are a few ways one could indicate missing values.

- An entity's object property lacks a `has specified value` relation where one is expected.

- For an entity that `has quality` some instance of a quality which is described by an instance of a `categorical value specification`, if the quality instance is the same as the CVS class `specifies value of` target, then no choice has been made, and no information is carried.

Suitable object properties:

- `inheres in` or `bearer of` object property if ...???
- `denotes` if the ICE is a type of **identifier**, such as a [`centrally registered identifier symbol`](http://purl.obolibrary.org/obo/IAO_0000577) like a [`specimen identifier`](http://purl.obolibrary.org/obo/OBI_0001616) or a NCIT [`identifier`](http://purl.obolibrary.org/obo/NCIT_C25364) for example.
- 'location of' if the literal value X is locating the given entity by a geospatial reference. ????

One can also use cardinality to specify more than one data property is allowed or required. Note that some OWL reasoning profiles don't work with cardinality.

Now, back to the age example, it looks like we could supply various age measurements like this:

<img src="/assets/images/docs/data_lee_object_property_ages.png">

To summarize, rather than establish a `has age` data property, OBI expresses that [`age`](http://purl.obolibrary.org/obo/PATO_0000011) is a quality of our entity, and then focuses on defining the semantics of it and its subclasses.  However, there are some limitations of the `has ... value` data property that this diagram and the one below expose.

<img align="right" src="/assets/images/docs/data_lee_data_properties.png">

- Data properties can't support units directly, so a second data property is required to eliminate ambiguity.  Is Lee a 12 year old youth, or a 12 month old toddler?  We need the **unit of measure**, in minutes, days, months, or years.   In the example diagram of Lee's data properties to right, is the `has weight` decimal value given in kilos or grams? Is height in meters or centimetres? Without an explicit unit, assumptions are made about units associated with a data property.

- A data property doesn't support a relevant time of measurement value.  For example, when was Lee's `has height` observed, and was it the same time as `has weight`, such that an accurate BMI can be calculated?  Admittedly, time differentiated data is rather complex to model in OWL. A pragmatic approach, if workable, is to only expose to an OWL reasoner data that doesn't need to be differentiated by time. In the BMI example, we could assume height and weight data properties are adequately close in time that derivative calculations are ok. OBI does offer annother approach detailed in the `Time-stamped data` section to describe n-dimensional points that include time.

- A data property cannot directly specify the range of ontology term choices (which are classes or individuals) for a categorical value since data property ranges can only be drawn from xml/rdf data types. "anon:Lee `has handedness` "http://purl.obolibrary.org/obo/PATO_0002201^^xsd:anyURI"" but the URI could point to anything on the internet. We can't express in OWL that the 'has handedness' data property URI range must fall within the class of PATO `handedness`.

- There is no direct way to indicate that an instance of paricular data property has a missing value since its object must have some value.  The data property as a whole could be omitted, and this may be sufficient for querying purposes.

To answer the above needs, OBI introduced an additional `value specification` entity, as detailed in the next section.