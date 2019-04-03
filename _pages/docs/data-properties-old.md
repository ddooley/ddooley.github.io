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

A given datum value from the left may match one of four scenarios, the first two involving a data properties directly, and the latter two involving a multi-component "value specification" representation as described below.  An ontology **`data property`** provides a relation to attach an entity instance to some literal datatype value (an RDF number, string or date for example) that is a measure or estimate of what that data property is about. There is also the need to detail a [`composite datum`](/docs/data-properties/#composite-datum/) which has datum components.

### Datum / data property compatible

OBI can attach a number of [OWL-compatible RDF/XML datatype](https://www.w3.org/2007/OWL/wiki/DatatypeRescue) values directly to "atomic" ICE datums using a [`has literal value`](???) data property.

#### Scalar datum

A specific numeric datatype can be indicated to capture the numeric type of a spreadsheet field for example.  Numeric datatypes are detailed in the [Numeric Datums](/docs/datatype-numeric/) section.  Also note the [measurement unit](/docs/data-properties/#measurement-units) description below. Suffice to say, the strings "20g", "20 grams", and "0.02kg" may differ by string comparison, but can be translated into identical value + unit atomic components: a decimal 20.0 and a "gram" mass unit.

- [`xsd:decimal`](???) datatype for storing decimal values.
- [`xsd:integer`](???) datatype for storing counts and other integers, e.g. a pH measurement.
- [`xsd:float`](???) datatype for storing floating point decimal values.

- [`xsd:dateTime`](???)  for a datum containing a xsd:dateTime formatted date or time, or [`xsd:dateTimeStamp`](???), which includes time zone too.  Details are in [Date, Time, and Duration Datums](/docs/datatype-time/); examples of use are in the [Time stamped data](/docs/data-time-stamped/) section.


### Categorical value specification compatible

A [`categorical value specification`](http://purl.obolibrary.org/obo/OBI_0001930) describes a categorical variable like color, which can match selections from a string list of terms or from a branch of ontology terms (e.g. terms from a standardized color wheel).  See [docs/data-vs](docs/data-vs) for more details.

#### Boolean datum

- A [`xsd:boolean`](??) datum represents a yes/no or true/false value.  See [Boolean Datums](/docs/datatype-boolean/).

#### String datum 

- A [`xsd:string`](???) textual datum can at the very least be compared to other strings.  See [String Datums](/docs/datatype-string/).  Example: The (fictitious) [`Social Security Number`](http://purl.obolibrary.org/obo/NCIT_C25686) "000-11-2222", an identifier which serves a data matchmaking role, and which is for practical purposes atomic (although sub-sequences of 0's do signal fictitious records).

#### Resource datum

- A [`xsd:anyURI`](???) value contains a URI pointing to a document or other type of resource file.  Example: an ICE [`analytical cytology data file`](http://purl.obolibrary.org/obo/OBI_0000210) specification ["https://onlinelibrary.wiley.com/doi/epdf/10.1002/cyto.990110303"](https://onlinelibrary.wiley.com/doi/epdf/10.1002/cyto.990110303)



### Textual representation

Separately from the above `has literal value`, one can add [`has textual representation'](???) values that are linguistically or computationally coded. Such a value holds "undigested" data, say, in preparation for parsing by SPARQL etc. into more atomic components.  Other object relations may be provided to enable interpretation of such values. It can store values that may or may not fit directly on a numeric or categorical scale, as well as linguistic content (words, phrases, sentences with an optional OWL language facet).  For example, a sexuality datum instance `has parsable value` "m" that is not yet translated to PATO [`male`]( http://purl.obolibrary.org/obo/PATO_0000384).  The string "16500 Mullholland Dr., Los Angeles, CA, USA" can be attached to a [`street address`](http://purl.obolibrary.org/obo/NCIT_C25690) datum. The value needs parsing to extract house/apartment number, street, city, country, etc.  "20g" may be held as a parsable value en route to becoming a scalar value + unit data property pair.

Parsable strings could technically be stored as annotations but the potential for referencing them as input our output of process axioms (e.g. in natural language processing) is then lost.


## Data Property Implementation Approach

Before we detail the use of `has literal value` etc. data properties, we will discuss OBI's philosophy about data properties in general.  In an ontology one might find a `has age` data property used to express that Lee's age is 12, as shown to the right. OBI shies away from this approach, as explained below.

<img src="/assets/images/docs/data_lee_data_property_age.png">

<img align="right" src="/assets/images/docs/data_lee_data_property_ages.png">

The label of the data property tells humans in hopefully plain language what the value is about, but a reasoner will have a bad time guessing what the relation is equivalent to in other graphs that have differently named or identified relations that mean the same thing.  As shown, the problem is magnified if other age quantities are involved.

A second problem is revealed in the age example - is John 12 years old or 12 months? Has it been 19 months since he was fertilized or 19 years! A general way to provide units is required.

<br clear="right">

<img align="right" src="/assets/images/docs/data_age_measurement_datums.png">

In fact there are many kinds of [`ages`](http://purl.obolibrary.org/obo/OBI_0001167) in the biomedical and biological research realm; a number of related datums from OBI are listed here. Rather than creating a litany of data properties, OBI has chosen an alternative approach - a data modelling vocabulary that focuses on describing a core entity's role, quality, information content and other descriptive components rather than directly connecting semantically opaque data properties. This is not to say non-OBI `data properties` are forbidden in application ontologies - but going through the exercise of defining them in terms of a generic BFO/OBI/OBO Foundry set of terms may help anticipate data sharing issues.

<br clear = "both">

### OBI Object Property "Aboutness" Approach

To address these issues, rather than establish a `has age` data property, OBI expresses that [`age`](http://purl.obolibrary.org/obo/PATO_0000011) is a quality of our entity, and then focuses on defining the semantics of it and its subclasses.  This approach reduces the amount of language needed to describe entities, at the cost of a bit more structure. *Most importantly it enables entities to be the focus of semantic elaboration (axioms) rather than being surrounded by opaque relations.* Below, an age datum instance's value and unit are represented by way of `has literal value` and `has measurement unit label`:

<img src="/assets/images/docs/data_lee_object_property_age_unit.png">

The `aboutness` details have the extra benefit of facilitating appropriate data exchange between ontology-driven systems.  By specifying that a string field is about a first name or a last name, maiden name, full name, SIN number, postal code, etc. this 'aboutness' information can guide the merging and federated querying of triple store graphs.  

### Measurement Units

Stating units is especially important for enabling data exchange unambiguously - units implicitly assumed for a data property may work internally to a system, but are likely to fail when exchanging information with other systems. OBI provides a [`has measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039) object property for this reason.  If a numeric or datetime value needs a unit (e.g. metre, kilogram, hour, minute) the [`has measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039) object property can be used to point to a [`measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000003) entity such as one of the [`Units of Measure Ontology`](http://purl.obolibrary.org/obo/UO_0000000) (UO) terms. The [Units of Measure Ontology](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3468815/) is provided in two versions, one which enumerates particular units like `meter` as individuals of a parent unit class, while the other version supplies all units as classes.  OBI works with units as individuals.

A 2009 editor note in [`is quality measurement of`](http://purl.obolibrary.org/obo/IAO_0000221) explains `has measurement unit label`: *"We decided to hedge on what units of measure are, instead talking about measurement unit labels, which are the information content entities that are about whatever measurement units are. For IAO we need that information entity in any case."*

In the diagram below, other types of age measurements are described. The need for units is evident:

<img src="/assets/images/docs/data_lee_object_property_ages.png">

Below is another example focusing on providing values for information content entities typically connected to a person instance.

<img src="/assets/images/docs/data_lee_has_specified_value.png">

And here is a pH measurement example, showing the datum as an output of a process, and alternately with a unit (which some may allow as optional - UO has the [`pH`](http://purl.obolibrary.org/obo/UO_0000196) unit, though techically the formula yields a dimensionless number).

<img src="/assets/images/docs/data_ph_object_property.png">

Here is John's mass measurement. In the instance expressions, it isn't necessary to mention the `quality` class here insofar as the `mass measurement datum` can be said to be `about` the instance of John directly. 

<img src="/assets/images/docs/data_john_mass_data_property.png">


## Missing values

Data sources may mark missing values in a variety of ways - by an empty string, or a hyphen instead of a number or date for example.  Instance subject-verb-object triples don't have an equivalent way to express this. However there are a few ways one could indicate missing values.

- A datum instance lacks a `has rdfs:Literal value` data property or subproperty (especially if one is indicated in the datum class).

## Suitable object properties

It is straightforward to see a material entity connected to a pertinent quality via `has quality`, but there are other object properties that connect a material entity to other types of things:

- More broadly, an information content entity (ICE) [`is about`](http://purl.obolibrary.org/obo/IAO_0000136) material entity if the ICE is calculated from qualities of the material entity.

- Thing [`denotes`](http://purl.obolibrary.org/obo/IAO_0000219) material entity if the thing is a type of **identifier**, such as a [`centrally registered identifier symbol`](http://purl.obolibrary.org/obo/IAO_0000577) like a [`specimen identifier`](http://purl.obolibrary.org/obo/OBI_0001616) or a NCIT [`identifier`](http://purl.obolibrary.org/obo/NCIT_C25364) for example.

- Material entity [`located in`](http://purl.obolibrary.org/obo/RO_0001025) geospatial reference.  Note the editor's note: "Most location relations will only hold at certain times, but this is difficult to specify in OWL." 

<br clear="right">

<img src="/assets/images/docs/data_personal_status_monitor.png" width="400" align="right">

One can also use cardinality to specify more than one data property is allowed or required in a given data structure.  Shown is an example taken from figure 2 in ["Ontology Based Annotation of Contextualized Vital Signs"](http://ceur-ws.org/Vol-1060/icbo2013_submission_18.pdf), "Parts of a Personal Status Monitor (PSM) measurement datum for a single accelerometer and single pulse rate sensor". Note that some OWL reasoning profiles don't work with cardinality. 

<br clear="right">

## Data property limitations

Besides the need to specify measurement units, there are a few other limitations of coupling data properties too tightly to the entities they describe.

<img align="right" src="/assets/images/docs/data_lee_data_properties.png">

A data property doesn't directly support a relevant time of measurement value.  For example, when was Lee's `has height` observed, and was it the same time as `has weight`, such that an accurate BMI can be calculated?  Admittedly, time differentiated data is rather complex to model in OWL. A pragmatic approach, if workable, is to only expose to an OWL reasoner data that doesn't need to be differentiated by time. In the BMI example, we could assume height and weight data properties are adequately close in time that derivative calculations are ok. OBI does offer annother approach detailed in the [`Time-stamped data`](/docs/data-time-stamped/) section to describe n-dimensional points that include time.

A data property cannot directly specify the range of ontology term choices (which are classes or individuals) for a categorical value since data property ranges can only be drawn from xml/rdf data types, none of which incorporates ontology term entities. One could express a `has handedness` data property instance

    Lee `has handedness` "http://purl.obolibrary.org/obo/PATO_0002201^^xsd:anyURI"

but the above URI could point to any internet URI, and so could not be validated as a categorical choice. We can't express in OWL that the 'has handedness' data property URI range must fall within the class of PATO `handedness` (this could only be imposed via a string pattern matcher in a class data property axiom). 

Multi-dimensional datums - time-stamped observations, or geographic lat/long location for example - require a more complicated datum structure. To meet these needs, one either needs to use `composite datum` or `value specification` entities.

## Composite datum

...

## Other metadata

Other metadata may need to be marked e.g. how to deal with: “In some cases, a component is detected in the food matrix, but it cannot be quantified precisely. The analytical result can therefore be considered as ‘trace’” (see [here](https://ciqual.anses.fr/cms/sites/default/files/inline-files/TableCiqual2017_XML_docENG.pdf)). Another case is where a data item exists but has been obfuscated for privacy reasons.  OBI does not currently have a metadata standard that addresses these cases.


DISCUSS:
### Scalar value specification compatible: OBI implementers may prefer to isolate the value data collected from assays from the [`measurement datum`](http://purl.obolibrary.org/obo/IAO_0000109) representation level of assay output.  OBI provides a [`has value specification`]() object property that points to a [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931) which can take on the same value and measurement unit label data and object properties as described above.  See [docs/data-vs](docs/data-vs) for more details.

