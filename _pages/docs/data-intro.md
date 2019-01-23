---
layout: single
title: Introduction to OBI data modelling
permalink: /docs/data-intro/
toc: true
sidebar:
  nav: "docs"
---

[//]: # (Please put comments like this one into the text to communicate with other OBI-ers)

*One of OBI's missions, to model the logical structure of experimental assays, requires a close study of entity attributes, processes and their participants, and data being collected. Below we introduce the general framework for describing processes, datums used as process input or output, and data collection specifications. Some stakeholders are involved only in process modelling in order to document study design and/or protocol details as metadata; others are turning to OBI ontology to provide standardization of data collection and exchange; software developers will require knowledge in both these areas in order to provide the next generation of integration tools. We aim to provide analysis approaches and diagrams to satisfy these needs.*

In addition to reasoning prowess, using an OWL ontology to detail types of assay data - parameters, measurables, independent and dependent variables - will encourage standardization of their usage, enable experimental reproducibility, and facilitate data exchange and conversion.

Note that the diagrams in this section are contained in a [figs/data_obi_draw.io.xml](/docs/figs/data_obi_draw.io.xml) file, in [draw.io](http://draw.io) diagram format for reuse in ontology design work.  *Most of the diagrams below skip relation cardinality details (e.g. "X 'is about' [[some / all / max 3 / only]] Y"), but these do exist in OBI to enforce more structure, and are detailed in OWL code examples.*

*Aligning with BFO, OBI divides references about study design and assay structure into roughly four domains - **[`material entities`](http://purl.obolibrary.org/obo/BFO_0000040)**, their observable **[`qualities`](http://purl.obolibrary.org/obo/BFO_0000019)**, **[`planned processes`](http://purl.obolibrary.org/obo/OBI_0000011)**, and **[`information artifacts`](http://purl.obolibrary.org/obo/IAO_0000030)**, which all show up in process and data modelling.*

## Material entities and their properties

*Under `material entity` we find OBI's **[`organism`](http://purl.obolibrary.org/obo/OBI_0100026)** - the usual focus of biomedical investigations. Organism related terms - whether in OBI or in other ontologies that cover taxonomic, anatomic, developmental, pathological, environmental etc. aspects - will likely occur in study design objectives, protocols and experimental observations.*

<img align="right" src="/docs/figs/data_john_mass_entity_property.png">

<img align="right" src="/_pages/docs/figs/data_john_mass_entity_property.png">

<img align="right" src="/data_john_mass_entity_property.png">

*We use **entity property diagrams** to show material entities and selected object properties (that link them to qualities) and class-subclass relations, which together illustrate OBI core "terminological component" (Tbox) contents. In this example, a `material entity` [`has quality`](http://purl.obolibrary.org/obo/RO_0000086) some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125). This axiom is not currently in OBI but is included to show the potential for relation inheritance.  Formally, `has quality` is a generic object property existing between a BFO independent continuent entity (the bearer) and a quality, which is a dependent continuent (i.e. something that depends on the existence of its continuent).  [`Homo sapiens`](http://purl.obolibrary.org/obo/NCBITaxon_9606) is shown as a descendent of `organism`, a subclass of `material entity`, so the descendants also inherit a mass quality that can be referenced.  (A dashed arrow between entities indicates that several intermediate taxon classes have been omitted)*

*An optional rose-tinted box may be provided to illustrate how to compose instances of classes and relations - this is "assertion component" (Abox) content. Abox content can form the bulk of a triple-store graph database, with the reasoning axioms of related ontologies added separately when validation of data structures and models is desired. In this example it is stated that "John" is an instance of Homo sapiens, and bears an instance of mass (or mass quality) that can then be referenced by other expressions.*

*Note for novices: An **[`anonymous or blank node`](https://en.wikipedia.org/wiki/Blank_node)** contains a data structure which has not itself been given a full URI resource identifier (for example a statement made within the context of another entity). These will occur in de-serialized triple store databases and ontologies for any bracketed conjunction or disjunction expression. So, to be precise, the diagram shows an anonymous node that is of type `Homo sapiens` which would also have an annotation or data property of name "John", and which has a `has quality` relation to another anonymous node of type `mass`.*

## Information content entities

*All information items that are derived from material entities (i.e. statements that reference material qualities and are factual claims about an entity) fall under the domain of* **[`information content entity`](http://purl.obolibrary.org/obo/IAO_0000030)** (ICE), very generally defined as a type of entity which bears information about something<sup>1</sup>.  Any ICE class may have **[`is about`](http://purl.obolibrary.org/obo/IAO_0000136)** object relations that connect it to other material entities or ICEs which define its _aboutness_.  Examples: an "[`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156) `is about` some [`Spermatophyta`](http://purl.obolibrary.org/obo/NCBITaxon_58024)" (among other things); a "[`minimal inhibitory concentration`](http://purl.obolibrary.org/obo/OBI_0001514) `is about` some [`dose response curve`](http://purl.obolibrary.org/obo/OBI_0001172)", another ICE.  Aboutness axioms should reinforce the content of term definitions.  

[//]: # (The defining characteristic of an `Information Content Entity` is that it is 'about' something. Thus, the scope of the OBI representation of data is to capture the details and characteristics of the information, rather than the thing that it describes. This is a crucial scoping step in developing representations in OBI.)

<img align="right" src="/docs/figs/data_iao_branch.png">

The `information content entity` **[`data item`](http://purl.obolibrary.org/obo/IAO_0000027)** class holds singular entities or collections of entities that specifically record inputs or outputs of processes / equipment / human interaction. OBI distinguishes the following singular types of data items, usually called "datums", as follows:

* A **[`measurement datum`](http://purl.obolibrary.org/obo/IAO_0000109)** class names and models the datum outputs of an assay, and their contextual semantics. 
* A **[`settings datum`](http://purl.obolibrary.org/obo/IAO_0000140)** class which enables modeling an apparatus control input.
* A **[`predicted data item`](http://purl.obolibrary.org/obo/OBI_0302867)** class that applies to output of a [`prediction`](http://purl.obolibrary.org/obo/OBI_0302910) process.

All ICEs are allowed a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933)** that records some pertinent categorical or numeric value about an entity; more on this in the data collection section.

## Process modelling basics

*Generally a **[`process`](http://purl.obolibrary.org/obo/BFO_0000015)** can have other processes as parts, and can have instances with start and end times associated with them.  A **[`planned process`](http://purl.obolibrary.org/obo/OBI_0000011)** is carried out by agent(s) who are guided by some kind of **[`plan specification`](http://purl.obolibrary.org/obo/IAO_0000104)**, an ICE which has **[`objective`](http://purl.obolibrary.org/obo/IAO_0000005)** and **[`action`](http://purl.obolibrary.org/obo/IAO_0000007)** components. A **[`study design`](http://purl.obolibrary.org/obo/OBI_0500000)** and its **[`protocol`](http://purl.obolibrary.org/obo/OBI_0000272)** part(s) are subclasses of `plan specification`. This is documented in the [`Study Design`]() page.* 

<img align="right" src="/docs/figs/data_assay_2.png">

*A **process / datum model diagram** shows how material entities or data items can be an input or output of some process. This diagram often includes parts of entity property diagrams in order to reference components as inputs or in aboutness clauses.*

*The **[`assay`](http://purl.obolibrary.org/obo/OBI_0000070)** process diagram to right details axioms that enable types of assay to inherit requirements: [paraphrasing] that an assay input is a material entity playing an evaluant role, and that an assay outputs one or more data items.*

<br clear="both">


<img align="right" src="/docs/figs/data_john_mass_process.png">

*The next example shows a **[`mass measurement assay`](http://purl.obolibrary.org/obo/OBI_0000445)** which takes in some material and outputs a **[`mass measurement datum`](http://purl.obolibrary.org/obo/IAO_0000414)**.  The output datum is stated to be a measure of (only) mass quality. The **[`is quality measurement of`](http://purl.obolibrary.org/obo/IAO_0000221)** object property is actually a sub-property of `is about` which is used when the target of aboutness is a quality.*

*The Abox shows John as an input (standing on a scale, say), and documents that a `mass measurement datum` has been taken by the `mass measurement assay`. A process modeller can work at this more abstract level, avoiding references to specific protocols or instruments involving, say, units of measure. Alternately, by merging process modelling with specific value specifications (described below), we can describe particular equipment used in an experimental protocol or execution - say a brand and model of weight scale that is only capable of measuring in grams. (That level of detail promotes an ontology-driven plug-and-play future of equipment selection and protocol design.)*

### Process modelling with inputs playing roles

**Mark's doctor/patient interaction event example here....**

*Processes can have other participants besides inputs and outputs, such as operators and material consumables.*






### Material processing

<img align="right" src="/docs/figs/data_processed_material.png">

*Processes don't necessarily generate information products.  The OBI [`material processing`](http://purl.obolibrary.org/obo/OBI_0000094) class covers many kinds of process such as sample preparation, manufacturing, and staining. [`processed specimen`](http://purl.obolibrary.org/obo/OBI_0000953) is likely needed as part of experimental protocol modeling involving biosamples. It remains a material entity, rather than a `data item` that assays output.* 

<br clear="both">

## Process modelling - a top-down approach

**Hande's content**



##Data value specification

*This brings us to the collection of data - where specific protocols or instruments are used, generating data on particular scales and scientific units.  One can have data about entities which bear various qualities, and their value specifications, without necessarily having connections to a model layer of processes and datums.  One can document tabular data column metadata independently of experimental protocol process descriptions that explain how the data was generated.  Here **data specification diagrams** are useful for showing a given observation's type of variable and permitted units. This diagram and modelling approach can exist independently of the process model described above, but is designed to fit seamlessly with it as well.*

<img align="right" src="/docs/figs/data_john_mass_value_spec.png">

To establish constraints on what a datum can have for a value, OBI introduces a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933)** (VS) class which can express those constraints in axioms (for example pertinent numeric data type, units, or valid categorical choices). An instance of a value specification can have a **[`has specified value`](http://purl.obolibrary.org/obo/OBI_0002135)** data property that holds its literal value. A value specification details allowable values for a given purpose. 

*Explanations of the different types of categorical, numeric and datetime value specifications are contained in the [`Data Types`](data-types.md) documentation. Background information on how the value specification concept was developed is [here](https://github.com/obi-ontology/obi-legacy-svn/blob/master/trunk/src/examples/development/data-prototype.pdf).  Other related OBI repository issues: [#870](https://github.com/obi-ontology/obi/issues/870), [#945](https://github.com/obi-ontology/obi/issues/945) and [#833](https://github.com/obi-ontology/obi/issues/833)*.

A value specification's primary aboutness is expressed using the **[`specifies value of`](http://purl.obolibrary.org/obo/OBI_0001927)** object relation.  For example "[`mass value specification`](http://purl.obolibrary.org/obo/OBI_0001929) `specifies value of` some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125)", as shown above. An instance of the VS `specifies value of` an instance of the mass quality which inheres in John. The VS instance has a kilogram unit, and a decimal value of 70.0 .

The connection between a measurement datum (or any ICE term) and a value specification is accomplished with the **[`has value specification`](http://purl.obolibrary.org/obo/OBI_0001938)** object property. Thus an [`age measurement datum`](http://purl.obolibrary.org/obo/OBI_0001167) could be linked to a numeric value specification which details the unit - year, month, day etc. of the measure. It could alternately be provided as a categorical value for "mature", "immature", "neonatal", etc.  (As mentioned in the `Data Types` section, OBI does not currently have a way to describe ordinal values beyond listing them as categorical choices.)

In the case where a value specification and/or measurement datum is about the conjunction of a few different things, the aboutness target can be a precomposed term or instance of those components, with one component, usually a quality, providing the primary type of the measure.  For example "eye color" is primarily about color - and so limited to ways that can be reported, but secondarily about the body part being observed, and finally - in the instance, references a particular organism being observed. An example generic value specification and measurement datum both pointing to John's eye color being brown (in this case "specifies value of" points directly to the value specification's essentially categorical value. Here the `color value specification` provides the range of choices permitted for the instance of color quality.

<img src="/docs/figs/data_john_eye.png">

***DRAFT NOTE: Is it best to say "eye part of some mamallia", or "eye located in mammalia" as a shortcut? Or do we say the complete UBERON ... "eye part of some visual system", "visual system part of some mammalia?***

*Currently most statements about which qualities inhere in which physical objects are left to client ontologies to define, but uncontroversial universals (such as "material entity has quality some mass") should eventually be established in core ontologies.)*

*Note that different assays may output the same measurement datum and value specification combination.  For example an [`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156) and integer year value specification could be output from assays that calculate or estimate by input tree ring count, carbon 14 analysis, planting date, height of species etc.  It is up to an ontology implementer to define a more specific process as a sub-class of an existing general process if needed; if it falls within the scope of OBI, it may be a candidate for inclusion.*

## A Combined View

*A diagram that combines material entity, quality, process, data collection standards, and derived information, allows us to see the big picture - the data structure architecture that enables constructive reasoning. By tracing classes further up the inheritance hierarchy, we can see the impact on instance data.*

<img align="right" src="/docs/figs/data_john_mass.png">

([full-sized image](figs/data_john_mass.png))

Next section: [`Value specifications vs data properties`](data-value-specs-vs-data-properties.md)

***
References: 


* https://mitpress.mit.edu/books/building-ontologies-basic-formal-ontology

***
<sup>1</sup>The ability of an ICE to bear information depends on the coding scheme and medium it inheres in, hence it is a generically dependent continuant.