---
layout: default
title: Data Properties
permalink: /docs/data-properties/
sidebar:
  nav: "docs"
---

In addition to study design, protocol and execution, OBI aims to describe the field-level data of resulting datasets, which are currently likely to be found in text files, relational databases, or spreadsheets, and which need to be transformed into a RDF triple store structure to bring out the best analytic power of OBI, BFO, and other OBO Foundry ontologies.

Diagrammed on the left side are typical examples of field data related to a research subject, and on the right are datatypes that OWL reasoners and SPARQL querying engines can work with.   

<img align="right" src="/assets/images/docs/data_raw.png">

A given datum value from the left may match one of four scenarios, the first two involving a data properties directly, and the latter two involving a multi-component "value specification" representation as described below. There is also the need to handle [`composite datums`](/docs/data-properties/#composite-datum/) which are composed of datum parts.

### OWL datum - data property compatible

OBI can attach a number of [`OWL-compatible RDF/XML datatype`](https://www.w3.org/2007/OWL/wiki/DatatypeRescue) values directly to `atomic` ICE datums using a `has xsd:Literal value` data property or one of its sub-properties, as described below. (Representation of [`rational`](https://www.w3.org/2007/OWL/wiki/OWL_Rational) numbers is a bit more tricky.)

#### Scalar datum

- `has xsd:float value` data property for storing floating point decimal values.
- `has xsd:decimal value` data property for storing decimal values.
  - `has xsd:integer value` data property for storing counts and other integers, e.g. a pH measurement.

- `has xsd:dateTime value` or `has xsd:dateTimeStamp value` (includes time zone)for a datum containing a xsd:dateTime formatted date or time. Has xsd:dateTime or xsd:dateTimeStamp range, respectively. Examples of use are in the [`Time stamped data`](/docs/time-stamped-data/) section

If a numeric or datetime value needs a unit associated with it (e.g. metre, kilogram, hour, minute) the [`has measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039) object property can be used to point to a unit entity.  For example, the strings "20g", "20 grams", and "0.02kg" may differ by string comparison, but can be translated into identical value + unit atomic components: a decimal 20.0 and a "gram" mass unit.

#### Boolean datum

- `has xsd:boolean value` for a datum which is represented as a yes/no or true/false value.

#### String (symbol????) datum

- `has xsd:string value` for a textual datum that does not fit on a categorical scale but which can be compared (like a token) to other strings.  Example: The (fictitious) [Social Security Number](http://purl.obolibrary.org/obo/NCIT_C25686) "000-11-2222", an identifier which is not really on a scale or a categorical value.  It is essentially atomic; it serves a data matchmaking role.

#### Other resource datum

- `has xsd:anyURI value` for a datum which contains a URI pointing to a document or other type of resource file.  Example: an ICE [`analytical cytology data file`](http://purl.obolibrary.org/obo/OBI_0000210) specification ["https://onlinelibrary.wiley.com/doi/epdf/10.1002/cyto.990110303"](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cyto.990110303)

### String representation compatible

A datum can have a linguistically or computationally coded textual value using OBI's `has xsd:string representation` data property.  A string representation value can hold "undigested" data, say, in preparation for parsing by SPARQL etc. into more atomic components.  Other object relations may be provided to enable interpretation of such values. It can store values that may or may not fit directly on a numeric or categorical scale, as well as linguistic content (words, phrases, sentences with an optional OWL language facet.  For example:

- The address "16500 Mullholland Dr., Los Angeles, CA, USA" can be attached to a [`street address`](http://purl.obolibrary.org/obo/NCIT_C25690) datum. The value needs parsing to extract house/apartment number, street, city, country, etc.

- "20g" may be held as a string representation en route to becoming a scalar value + unit data property pair or a [`scalar value specification`](/docs/data-vs/).

Such data could technically be stored as annotations but the potential for referencing it as input our output of process axioms (e.g. in natural language processing) is then lost.

### Scalar value specification compatible

OBI implementers may prefer to isolate the value data collected from assays from the `measurement datum` representation level of assay output.  OBI provides a `has value specification` object property that points to a [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931) which can take on the same value and measurement unit label data and object properties as described in the Scalar datum section above.  See [docs/data-vs](docs/data-vs) for more details.

### Categorical value specification compatible

A [`categorical value specification`](http://purl.obolibrary.org/obo/OBI_0001930) describes a categorical variable like color, which can match selections from a string list of terms, or from a branch of ontology terms (e.g. terms from a standardized color wheel).  See [docs/data-vs](docs/data-vs) for more details.

## Data Property Implementation Approach

Before we detail the use of `has rdfs:Literal value` etc. data properties, we will discuss OBI's philosophy about data properties in general. 

<img align="right" src="/assets/images/docs/data_lee_data_property_age.png">

An ontology **`data property`** is a relation from an entity instance straight to some literal datatype value (an RDF number, string or date for example) that is a measure/estimate of what that data property is about. In an ontology one might find a `has age` data property used to express that Lee's age is 12, as shown to the right. OBI shies away from this approach, as explained below.  

<br clear="right">

<img align="right" src="/assets/images/docs/data_lee_data_property_ages.png">

The label of the data property tells humans in hopefully plain language what the value is about, but a reasoner will have a bad time guessing what the relation is equivalent to in other graphs that have differently named or identified relations that mean the same thing.  As shown, the problem is magnified if other age quantities are involved.

<br clear="right">

<img align="right" src="/assets/images/docs/data_age_measurement_datums.png">

In fact there are many kinds of [`ages`](http://purl.obolibrary.org/obo/OBI_0001167) in the biomedical and biological research realm; a number of related datums from OBI are listed here. Rather than creating a litany of data properties, OBI has chosen an alternative approach - a data modelling vocabulary that focuses on describing a core entity's role, quality, information content and other descriptive components rather than directly connecting semantically opaque data properties. This is not to say non-OBI `data properties` are forbidden in application ontologies - but going through the exercise of defining them in terms of a generic BFO/OBI/OBO Foundry set of terms may help anticipate data sharing issues.

OBI allows an age datum instance's value and unit to be represented by way of `has xsd:decimal value` and `has measurement unit label`:

<img src="/assets/images/docs/data_lee_object_property_age_unit.png">

Stating units is especially important for enabling data exchange unambiguously - units associated with a data property that may work internally to a system, but are likely to fail when exchanging information with other systems. OBI provides a [`has measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039) object property for this reason.  In the diagram below, other types of age measurements are described. The need for units is evident:

<img src="/assets/images/docs/data_lee_object_property_ages.png">

To summarize, rather than establish a `has age` data property, OBI expresses that [`age`](http://purl.obolibrary.org/obo/PATO_0000011) is a quality of our entity, and then focuses on defining the semantics of it and its subclasses.  This approach reduces the amount of language needed to describe entities, at the cost of a bit more structure. *Most importantly it enables entities to be the focus of semantic elaboration (axioms) rather than being surrounded by opaque relations.* The `aboutness` details have the extra benefit of facilitating appropriate data exchange between ontology-driven systems.  By specifying that a string field is about a first name or a last name, maiden name, full name, SIN number, postal code, etc. this 'aboutness' information can guide the merging and federated querying of triple store graphs.   

Below is another example focusing on providing values for information content entities typically connected to a person instance.

<img src="/assets/images/docs/data_lee_has_specified_value.png">

And here is a pH measurement example, showing the datum as an output of a process, and also with a unit (which some may argue is optional because there is only one unit possible):
\
<img src="/assets/images/docs/data_ph_object_property.png">


## Missing values

Data sources may mark missing values in a variety of ways - by an empty string, or a hyphen instead of a number or date for example.  Instance subject-verb-object triples don't have an equivalent way to express this. However there are a few ways one could indicate missing values.

- A datum instance lacks a `has rdfs:Literal value` data property or subproperty where one is indicated in the datum class.

## Suitable object properties

It is straightforward to see a material entity connected to a pertinent quality via `has quality`, but there are other object properties that connect a material entity to other types of things:

- **More broadly, an information content entity (ICE) [`inheres in`](http://purl.obolibrary.org/obo/RO_0000052) material entity or material entity [`bearer of`](http://purl.obolibrary.org/obo/RO_0000053) ICE if the ICE is calculated from qualities of the material entity ????????**

- Thing [`denotes`](http://purl.obolibrary.org/obo/IAO_0000219) material entity if the thing is a type of **identifier**, such as a [`centrally registered identifier symbol`](http://purl.obolibrary.org/obo/IAO_0000577) like a [`specimen identifier`](http://purl.obolibrary.org/obo/OBI_0001616) or a NCIT [`identifier`](http://purl.obolibrary.org/obo/NCIT_C25364) for example.

- Material entity [`located in`](http://purl.obolibrary.org/obo/RO_0001025) geospatial reference.  Note the editor's note: "Most location relations will only hold at certain times, but this is difficult to specify in OWL." 

One can also use cardinality to specify more than one data property is allowed or required. However, some OWL reasoning profiles don't work with cardinality.

## Data property limitations

Besides the need to specify measurement units, there are a few other limitations of coupling data properties too tightly to the entities they describe.

<img align="right" src="/assets/images/docs/data_lee_data_properties.png">

- A data property doesn't directly support a relevant time of measurement value.  For example, when was Lee's `has height` observed, and was it the same time as `has weight`, such that an accurate BMI can be calculated?  Admittedly, time differentiated data is rather complex to model in OWL. A pragmatic approach, if workable, is to only expose to an OWL reasoner data that doesn't need to be differentiated by time. In the BMI example, we could assume height and weight data properties are adequately close in time that derivative calculations are ok. OBI does offer annother approach detailed in the [`Time-stamped data`](/docs/time-stamped-datums) section to describe n-dimensional points that include time.

- A data property cannot directly specify the range of ontology term choices (which are classes or individuals) for a categorical value since data property ranges can only be drawn from xml/rdf data types. "Lee `has handedness` "http://purl.obolibrary.org/obo/PATO_0002201^^xsd:anyURI"" but the URI could point to anything on the internet. We can't express in OWL that the 'has handedness' data property URI range must fall within the class of PATO `handedness`. An object property is required for this reference.

This doesn't provide the necessary structure for describing multi-dimensional datums - time-stamped observations, or geographic lat/long location for example. To meet these needs, one either needs to use a `composite datum` or one needs an additional `value specification` entity.

## Composite datum

...