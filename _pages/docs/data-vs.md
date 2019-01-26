---
layout: single
title: ""
permalink: /docs/data-vs/
toc: true
sidebar:
#  nav: "docs"
---

# Value Specifications

This brings us to the collection of data - where specific protocols or instruments are used, generating data on particular scales and scientific units.  One can have data about entities which bear various qualities, and their value specifications, without necessarily having connections to a model layer of processes and datums.  One can document tabular data column metadata independently of experimental protocol process descriptions that explain how the data was generated.  Here **data specification diagrams** are useful for showing a given observation's type of variable and permitted units. This diagram and modelling approach can exist independently of process modelling, but is designed to fit seamlessly with it as well.

<img align="right" src="/assets/images/docs/data_john_mass_value_spec.png">

To establish constraints on what a datum can have for a value, OBI introduces a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"}** (VS) class which can express those constraints in axioms (for example pertinent numeric data type, units, or valid categorical choices). An instance of a value specification can have a **[`has specified value`](http://purl.obolibrary.org/obo/OBI_0002135){:target="_blank"}** data property that holds its literal value. A value specification details allowable values for a given purpose. 

Explanations of the different types of categorical, numeric and datetime value specifications are contained in the [`Data Types`](data-types.md) documentation. Background information on how the value specification concept was developed is [here](https://github.com/obi-ontology/obi-legacy-svn/blob/master/trunk/src/examples/development/data-prototype.pdf){:target="_blank"}.  Other related OBI repository issues: [#870](https://github.com/obi-ontology/obi/issues/870){:target="_blank"}, [#945](https://github.com/obi-ontology/obi/issues/945){:target="_blank"} and [#833](https://github.com/obi-ontology/obi/issues/833){:target="_blank"}.

A value specification's primary aboutness is expressed using the **[`specifies value of`](http://purl.obolibrary.org/obo/OBI_0001927){:target="_blank"}** object relation.  For example "[`mass value specification`](http://purl.obolibrary.org/obo/OBI_0001929){:target="_blank"} `specifies value of` some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125){:target="_blank"}", as shown above. An instance of the VS `specifies value of` an instance of the mass quality which inheres in John. The VS instance has a kilogram unit, and a decimal value of 70.0 .

The connection between a measurement datum (or any ICE term) and a value specification is accomplished with the **[`has value specification`](http://purl.obolibrary.org/obo/OBI_0001938){:target="_blank"}** object property. Thus an [`age measurement datum`](http://purl.obolibrary.org/obo/OBI_0001167){:target="_blank"} could be linked to a numeric value specification which details the unit - year, month, day etc. of the measure. It could alternately be provided as a categorical value for "mature", "immature", "neonatal", etc.  (As mentioned in the `Data Types` section, OBI does not currently have a way to describe ordinal values beyond listing them as categorical choices.)

In the case where a value specification and/or measurement datum is about the conjunction of a few different things, the aboutness target can be a precomposed term or instance of those components, with one component, usually a quality, providing the primary type of the measure.  For example "eye color" is primarily about color - and so limited to ways that can be reported, but secondarily about the body part being observed, and finally - in the instance, references a particular organism being observed. An example generic value specification and measurement datum both pointing to John's eye color being brown (in this case "specifies value of" points directly to the value specification's essentially categorical value. Here the `color value specification` provides the range of choices permitted for the instance of color quality.

<img src="/assets/images/docs/data_john_eye.png">

Note that this is our first example of measuring a property of a part of something. Above, an instance of Uberon eye is part of an instance of Homo sapiens, a parthood simplification for what some might need to model in a more complicated way.  For example, optometrists need to distinguish left and right eyes, and allow each to have different iris colors (it happens!), and to describe the color of sclera or conjunctiva (e.g. for red eye or pink eye).  Uberon supports this with `left eye` and `right eye` terms as subclasses of `eye`, and says "`eye` `part of` some `visual system`" but it stops short of establishing a parthood chain between `eye` and `mammalia`.  In the future such standardizing axioms may be introduced which client ontologies and triple store databases can employ to ensure data structure compatibility.  Regardless, it is usually ok to use a simple `part of` relation to abbreviate a more intricate parthood chain if it fits your needed granularity of description.

Note that different assays may output the same measurement datum and value specification combination.  For example an [`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156){:target="_blank"} and integer year value specification could be output from assays that calculate or estimate by input tree ring count, carbon 14 analysis, planting date, height of species etc.  It is up to an ontology implementer to define a more specific process as a sub-class of an existing general process if needed; if it falls within the scope of OBI, it may be a candidate for inclusion.
