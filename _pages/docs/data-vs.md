---
layout: default
title: "Value Specifications"
permalink: /docs/data-vs/
#toc: true
sidebar:
   nav: "docs"
---

OBI has introduced a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"}** (VS) class which more explicitly [`specifies value of`](http://purl.obolibrary.org/obo/OBI_0001927) a quality, datum, or postcomposed expression that it is about.  A value specification can be separated from a ICE by way of a "[ICE] `has value specification` [value specification]" object property.  There are a few different kinds of `value specification` for capturing needed details of numeric, string and categorical variables, which echo the combinations possible from direct connection of a datum to data properties:

<img src="/assets/images/docs/data_value_specs.png">

- A [`scalar value specification`](http://purl.obolibrary.org/obo/OBI_0001931) class includes a `has specified value` as described in the `data properties` section, and a `has measurement unit label` to define permitted unit classes.

- A [`categorical value specification`](http://purl.obolibrary.org/obo/OBI_0001930) class includes a `specifies value of` object property pointing to a root term in an ontology branch of terms which are thereby considered choices of the categorical value. Instances of `specifies value of` are selections within the class of choices.  

- `Datetime` and `duration` value specification classes enable a date or time duration, and associated units, to be described e.g. "5 days", or "week of 2018/01/01".

- A `boolean value specification` class indicates the presence (true) or absence (false) of a feature. This is distinct from a binary (two-choice) categorization which is a subclass of categorical variable.)

Explanations of the different types of categorical, numeric and datetime value specifications are contained in the [`Data Types`](data-types.md) documentation. Background information on how the value specification concept was developed is [here](https://github.com/obi-ontology/obi-legacy-svn/blob/master/trunk/src/examples/development/data-prototype.pdf){:target="_blank"}.  Other related OBI repository issues: [#870](https://github.com/obi-ontology/obi/issues/870){:target="_blank"}, [#945](https://github.com/obi-ontology/obi/issues/945){:target="_blank"} and [#833](https://github.com/obi-ontology/obi/issues/833){:target="_blank"}.

<img align="right" src="/assets/images/docs/data_john_mass_value_spec.png">

A **value specification diagram** can have data about entities which bear various qualities, and their value specifications, without necessarily having connections to a model layer of processes and datums, so these components can fit seamlessly with process modelling, but can be stand-alone as well.  Tabular data column metadata can be detailed independently of experimental protocol process descriptions that explain how the data was generated.  

The diagram shows a "[`mass value specification`](http://purl.obolibrary.org/obo/OBI_0001929){:target="_blank"} `specifies value of` some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125){:target="_blank"}", as shown above. An instance of the VS `specifies value of` an instance of the mass quality which inheres in John. The VS instance has a kilogram unit, and a decimal value of 70.0 .

The connection between a measurement datum (or any ICE term) and a value specification is accomplished with the **[`has value specification`](http://purl.obolibrary.org/obo/OBI_0001938){:target="_blank"}** object property. Thus an [`age measurement datum`](http://purl.obolibrary.org/obo/OBI_0001167){:target="_blank"} could be linked to a numeric value specification which details the unit - year, month, day etc. of the measure. It could alternately be provided as a [`categorical value`](/docs/data-categorical/) for "mature", "immature", "neonatal", etc.

In the case where a value specification and/or measurement datum is about the conjunction of a few different things, the aboutness target can be a postcomposed expression of those components, with one component, usually a quality, providing the primary type of the measure.  For example "eye color" is primarily about color - and so limited to ways that can be reported, but secondarily about the body part being observed, and finally - in the instance, references a particular organism being observed. 

<img align="right" src="/assets/images/docs/data_john_eye.png">

An example generic value specification and measurement datum both pointing to John's eye color being brown (in this case "specifies value of" points directly to the value specification's essentially categorical value. 

This is our first example of measuring a quality of a part of something. An instance of the Uberon ontology [`eye`](http://purl.obolibrary.org/obo/UBERON_0000970) is part of an instance of Homo sapiens, and 'has quality' some instance of PATO [`brown`](http://purl.obolibrary.org/obo/PATO_0000952).  An instance of the add-on `color value specification` class points to the `brown` instance as well. `color value specification` class points to any subclass of [`color`](http://purl.obolibrary.org/obo/PATO_0000952) as being permitted for the instance.

"Homo sapiens has part some eye" is a parthood simplification for what some might need to model in a more complicated way.  For example, ophthalmologists need to distinguish left and right eyes, and allow each to have different iris colors (it happens!), and to describe the color of sclera or conjunctiva (e.g. for red eye or pink eye).  Uberon supports this with `left eye` and `right eye` terms as subclasses of `eye`, and says "`eye` `part of` some `visual system`" but it stops short of establishing a parthood chain between `eye` and `mammalia`.  In the future such standardizing axioms may be introduced which client ontologies and triple store databases can employ to ensure data structure compatibility.  Regardless, it is usually ok to use a simple `part of` relation to abbreviate a more intricate parthood chain if it fits your needed granularity of description.

Note that different assays may output the same measurement datum and value specification combination.  For example an [`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156){:target="_blank"} and integer year value specification could be output from assays that calculate or estimate by input tree ring count, carbon 14 analysis, planting date, height of species etc.  It is up to an ontology implementer to define a more specific process as a sub-class of an existing general process if needed; if it falls within the scope of OBI, it may be a candidate for inclusion.

Below, value specifications are used to supply catagorical values, units are provided, and qualities of parts of organisms are unambiguously described.

<img align="right" src="/assets/images/docs/data_lee_properties_as_vs.png">

<br clear="both">

## Other metadata

Other metadata may need to be marked e.g. how to deal with: “In some cases, a component is detected in the food matrix, but it cannot be quantified precisely. The analytical result can therefore be considered as ‘trace’” (see [here](https://ciqual.anses.fr/cms/sites/default/files/inline-files/TableCiqual2017_XML_docENG.pdf)). Another case is where a data item exists but has been obfuscated for privacy reasons.  OBI does not currently have a metadata standard that addresses these cases.

*In the future numeric value specifications will likely include precision and error attributes.*
