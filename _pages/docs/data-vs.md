---
layout: default
title: "Value Specifications"
permalink: /docs/data-vs/
#toc: true
sidebar:
   nav: "docs"
---

OBI has introduced a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933)** (VS) class which more explicitly [`specifies value of`](http://purl.obolibrary.org/obo/OBI_0001927) a quality, datum, or postcomposed expression that it is about.  A value specification can be separated from a ICE by way of a "[ICE] [`has value specification`](http://purl.obolibrary.org/obo/OBI_0001938) [value specification]" object property.  There are a few different kinds of `value specification` for capturing needed details of numeric, string and categorical variables, which echo the combinations possible from direct connection of a datum to data properties:

<img src="/assets/images/docs/data_value_specs.png">

- A [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931) class includes a `has specified value` as described in the `data properties` section, and a `has measurement unit label` to define permitted unit classes.

- A [`categorical value specification`](http://purl.obolibrary.org/obo/OBI_0001930) class includes a `specifies value of` object property pointing to a root term in an ontology branch of terms which are thereby considered choices of the categorical value. Instances of `specifies value of` are selections within the class of choices.  

- `Datetime` and `duration` value specification classes enable a date or time duration, and associated units, to be described e.g. "5 days", or "week of 2018/01/01".

- A `boolean value specification` class indicates the presence (true) or absence (false) of a feature. This is semantically distinct from a binary (two-choice) categorization which is a categorical variable.

Explanations of the different types of categorical, numeric and datetime value specifications are contained in the [`Data Types`](data-types.md) documentation. Background information on how the value specification concept was developed is [here](https://github.com/obi-ontology/obi-legacy-svn/blob/master/trunk/src/examples/development/data-prototype.pdf).  Other related OBI repository issues: [#870](https://github.com/obi-ontology/obi/issues/870), [#945](https://github.com/obi-ontology/obi/issues/945) and [#833](https://github.com/obi-ontology/obi/issues/833).

<img align="right" src="/assets/images/docs/data_john_mass_value_spec.png">

A **value specification diagram** can have data about entities which bear various qualities, and their value specifications, without necessarily having connections to a model layer of processes and datums, so these components can fit seamlessly with process modelling, but can be stand-alone as well.  Tabular data column metadata can be detailed independently of experimental protocol process descriptions that explain how the data was generated.  

The diagram shows a "[`mass value specification`](http://purl.obolibrary.org/obo/OBI_0001929){:target="_blank"} `specifies value of` some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125){:target="_blank"}", as shown above. An instance of the VS `specifies value of` an instance of the mass quality which inheres in John. The VS instance has a kilogram unit, and a decimal value of 70.0 .

The connection between a measurement datum (or any ICE term) and a value specification is accomplished with the **[`has value specification`](http://purl.obolibrary.org/obo/OBI_0001938)** object property. Thus an [`age measurement datum`](http://purl.obolibrary.org/obo/OBI_0001167) could be linked to a numeric value specification which details the unit - year, month, day etc. of the measure. It could alternately be provided as a [`categorical value`](/docs/datatype-categorical/) for "mature", "immature", "neonatal", etc.

Here is a full-context value specification view of John's mass:

<img align="right" src="/assets/images/docs/data_john_mass_context.png">

In this example, instance data shows `age measurement datum`  `is about` Lee. Currently value specifications can be attached directly ICEs, but not to material entities, so in that case reference to an intermediate datum or quality is required.

<img src="/assets/images/docs/data_lee_age_value_specification.png">

Here is a pH measurement datum value specification.

<img src="/assets/images/docs/data_ph_measurement_vs.png">

Note that different assays may output the same measurement datum and value specification combination.  For example an [`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156) and integer year value specification could be output from assays that calculate or estimate by input tree ring count, carbon 14 analysis, planting date, height of species etc.  It is up to an ontology implementer to define a more specific process as a sub-class of an existing general process if needed; if it falls within the scope of OBI, it may be a candidate for inclusion.

Below, value specifications are used to supply catagorical values, units are provided, and qualities of parts of organisms are unambiguously described.

<img align="right" src="/assets/images/docs/data_lee_properties_as_vs.png">

