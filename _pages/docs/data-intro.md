---
layout: single
title: Introduction to OBI data modelling
permalink: /docs/data-intro/
toc: true
sidebar:
  nav: "docs"
---

One of OBI's missions, to model the logical structure of experimental assays, requires a close study of entity attributes, processes and their participants, and data being collected. Below we introduce the general framework for describing processes, datums used as process input or output, and data collection specifications. Some stakeholders are involved only in process modelling in order to document study design and/or protocol details as metadata; others are turning to OBI ontology to provide standardization of data collection and exchange; software developers will require knowledge in both these areas in order to provide the next generation of integration tools. We aim to provide analysis approaches and diagrams to satisfy these needs.

In addition to reasoning prowess, using an OWL ontology to detail types of assay data - parameters, measurables, independent and dependent variables - will encourage standardization of their usage, enable experimental reproducibility, and facilitate data exchange and conversion.

Note that the diagrams in this section are contained in a [/assets/files/data_obi_draw.io.xml](/assets/files/data_obi_draw.io.xml){:target="_blank"} file, in [draw.io](http://draw.io){:target="_blank"} diagram format for reuse in ontology design work.  Most of the diagrams below skip relation cardinality details (e.g. "X 'is about' {some / all / max 3 / only} Y"), but these do exist in OBI to enforce more structure, and are detailed in OWL code examples.

Aligning with BFO, OBI divides references about study design and assay structure into roughly four domains - **[`material entities`](http://purl.obolibrary.org/obo/BFO_0000040){:target="_blank"}**, their observable **[`qualities`](http://purl.obolibrary.org/obo/BFO_0000019){:target="_blank"}**, **[`planned processes`](http://purl.obolibrary.org/obo/OBI_0000011){:target="_blank"}**, and **[`information artifacts`](http://purl.obolibrary.org/obo/IAO_0000030){:target="_blank"}**, which all show up in process and data modelling.

## Material entities and their properties

Under `material entity` we find OBI's **[`organism`](http://purl.obolibrary.org/obo/OBI_0100026){:target="_blank"}** - the usual focus of biomedical investigations. Organism related terms - whether in OBI or in other ontologies that cover taxonomic, anatomic, developmental, pathological, environmental etc. aspects - will likely occur in study design objectives, protocols and experimental observations.

<img align="right" src="/assets/images/docs/data_john_mass_entity_property.png">

We use **entity property diagrams** to show material entities and selected object properties (that link them to qualities) and class-subclass relations, which together illustrate OBI core "terminological component" (Tbox) contents. In this example, a `material entity` [`has quality`](http://purl.obolibrary.org/obo/RO_0000086){:target="_blank"} some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125){:target="_blank"}. This axiom is not currently in OBI but is included to show the potential for relation inheritance.  Formally, `has quality` is a generic object property existing between a BFO independent continuent entity (the bearer) and a quality, which is a dependent continuent (i.e. something that depends on the existence of its continuent).  [`Homo sapiens`](http://purl.obolibrary.org/obo/NCBITaxon_9606){:target="_blank"} is shown as a descendent of `organism`, a subclass of `material entity`, so the descendants also inherit a mass quality that can be referenced.  (A dashed arrow between entities indicates that several intermediate taxon classes have been omitted).

An optional rose-tinted box may be provided to illustrate how to compose instances of classes and relations - this is "assertion component" (Abox) content. Abox content can form the bulk of a triple-store graph database, with the reasoning axioms of related ontologies added separately when validation of data structures and models is desired. In this example it is stated that "John" is an instance of Homo sapiens, and bears an instance of mass (or mass quality) that can then be referenced by other expressions.

## Anonymous nodes

Note for novices: An **[`anonymous or blank node`](https://en.wikipedia.org/wiki/Blank_node){:target="_blank"}** contains a data structure which has not itself been given a full URI resource identifier (for example a statement made within the context of another entity). These will occur in de-serialized triple store databases and ontologies for any bracketed conjunction or disjunction expression. So, to be precise, the diagram above shows an anonymous node that is of type `Homo sapiens` which would also have an annotation or data property of name "John", and which has a `has quality` relation to another anonymous node of type `mass`.




## Information content entities

All information items that are derived from material entities (i.e. statements that reference material qualities and are factual claims about an entity) fall under the domain of **[`information content entity`](http://purl.obolibrary.org/obo/IAO_0000030){:target="_blank"}** (ICE), very generally defined as a type of entity which bears information about something<sup>1</sup>.  Any ICE class may have **[`is about`](http://purl.obolibrary.org/obo/IAO_0000136){:target="_blank"}** object relations that connect it to other material entities or ICEs which define its _aboutness_.  Examples: an "[`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156){:target="_blank"} `is about` some [`Spermatophyta`](http://purl.obolibrary.org/obo/NCBITaxon_58024){:target="_blank"}" (among other things); a "[`minimal inhibitory concentration`](http://purl.obolibrary.org/obo/OBI_0001514){:target="_blank"} `is about` some [`dose response curve`](http://purl.obolibrary.org/obo/OBI_0001172){:target="_blank"}", another ICE.  Aboutness axioms should reinforce the content of term definitions.  

[//]: #(The defining characteristic of an `Information Content Entity` is that it is 'about' something. Thus, the scope of the OBI representation of data is to capture the details and characteristics of the information, rather than the thing that it describes. This is a crucial scoping step in developing representations in OBI.)

<img align="right" src="/assets/images/docs/data_iao_branch.png">

The `information content entity` **[`data item`](http://purl.obolibrary.org/obo/IAO_0000027){:target="_blank"}** class holds singular entities or collections of entities that specifically record inputs or outputs of processes / equipment / human interaction. OBI distinguishes the following singular types of data items, usually called "datums", as follows:

* A **[`measurement datum`](http://purl.obolibrary.org/obo/IAO_0000109){:target="_blank"}** class names and models the datum outputs of an assay, and their contextual semantics. 
* A **[`settings datum`](http://purl.obolibrary.org/obo/IAO_0000140){:target="_blank"}** class which enables modeling an apparatus control input.
* A **[`predicted data item`](http://purl.obolibrary.org/obo/OBI_0302867){:target="_blank"}** class that applies to output of a [`prediction`](http://purl.obolibrary.org/obo/OBI_0302910){:target="_blank"} process.

All ICEs are allowed a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"}** that records some pertinent categorical or numeric value about an entity; more on this in the data collection section.

## Process modelling basics

Generally a **[`process`](http://purl.obolibrary.org/obo/BFO_0000015){:target="_blank"}** can have other processes as parts, and can have instances with start and end times associated with them.  A **[`planned process`](http://purl.obolibrary.org/obo/OBI_0000011){:target="_blank"}** is carried out by agent(s) who are guided by some kind of **[`plan specification`](http://purl.obolibrary.org/obo/IAO_0000104){:target="_blank"}**, an ICE which has **[`objective`](http://purl.obolibrary.org/obo/IAO_0000005){:target="_blank"}** and **[`action`](http://purl.obolibrary.org/obo/IAO_0000007){:target="_blank"}** components. A **[`study design`](http://purl.obolibrary.org/obo/OBI_0500000){:target="_blank"}** and its **[`protocol`](http://purl.obolibrary.org/obo/OBI_0000272){:target="_blank"}** part(s) are subclasses of `plan specification`. This is documented in the [`Study Design`]() page.

<img align="right" src="/assets/images/docs/data_assay_2.png">

A **process / datum model diagram** shows how material entities or data items can be an input or output of some process. This diagram often includes parts of entity property diagrams in order to reference components as inputs or in aboutness clauses.

The **[`assay`](http://purl.obolibrary.org/obo/OBI_0000070){:target="_blank"}** process diagram to right details axioms that enable types of assay to inherit requirements: [paraphrasing] that an assay input is a material entity playing an evaluant role, and that an assay outputs one or more data items.

<br clear="both">


<img align="right" src="/assets/images/docs/data_john_mass_process.png">

The next example shows a **[`mass measurement assay`](http://purl.obolibrary.org/obo/OBI_0000445){:target="_blank"}** which takes in some material and outputs a **[`mass measurement datum`](http://purl.obolibrary.org/obo/IAO_0000414){:target="_blank"}**.  The output datum is stated to be a measure of (only) mass quality. The **[`is quality measurement of`](http://purl.obolibrary.org/obo/IAO_0000221){:target="_blank"}** object property is actually a sub-property of `is about` which is used when the target of aboutness is a quality.

The Abox shows John as an input (standing on a scale, say), and documents that a `mass measurement datum` has been taken by the `mass measurement assay`. A process modeller can work at this more abstract level, avoiding references to specific protocols or instruments involving, say, units of measure. Alternately, by merging process modelling with specific value specifications (described below), we can describe particular equipment used in an experimental protocol or execution - say a brand and model of weight scale that is only capable of measuring in grams. (That level of detail promotes an ontology-driven plug-and-play future of equipment selection and protocol design.)

### Processes with inputs playing roles

**Mark's doctor/patient interaction event example here....**

Processes can have other participants besides inputs and outputs, such as operators and material consumables.






### Material processing

<img align="right" src="/assets/images/docs/data_processed_material.png">

Processes don't necessarily generate information products.  The OBI [`material processing`](http://purl.obolibrary.org/obo/OBI_0000094){:target="_blank"} class covers many kinds of process such as sample preparation, manufacturing, and staining. [`processed specimen`](http://purl.obolibrary.org/obo/OBI_0000953){:target="_blank"} is likely needed as part of experimental protocol modeling involving biosamples. It remains a material entity, rather than a `data item` that assays output.

<br clear="both">

## A Combined View

A diagram that combines material entity, quality, process, data collection standards, and derived information, allows us to see the big picture - the data structure architecture that enables constructive reasoning. By tracing classes further up the inheritance hierarchy, we can see the impact on instance data.

<img align="right" src="/assets/images/docs/data_john_mass.png">

([full-sized image](/assets/images/docs/data_john_mass.png){:target="_blank"})

Next section: [`Value specifications vs data properties`](/docs/vss-vs-dp/)

***
<sup>1</sup>The ability of an ICE to bear information depends on the coding scheme and medium it inheres in, hence it is a generically dependent continuant.