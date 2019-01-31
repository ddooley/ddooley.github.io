---
layout: single
title: Introduction to OBI data modelling
permalink: /docs/data-intro/
toc: true
sidebar:
  nav: "docs"
---

One of OBI's missions, to model the logical structure of experimental assays, requires a close study of entity attributes, processes and their participants, and data being collected. Below we introduce the general framework for describing processes, datums used as process input or output, and data collection specifications. Some stakeholders are involved only in process modelling in order to document study design and/or protocol details as metadata; others are turning to OBI ontology to provide standardization of data collection and exchange; software developers will require knowledge in both these areas in order to provide the next generation of integration tools. We aim to provide analysis approaches and diagrams to satisfy these needs.

Aligning with BFO, OBI divides references about study design and assay structure into roughly four domains - **[`material entities`](http://purl.obolibrary.org/obo/BFO_0000040){:target="_blank"}**, their observable **[`qualities`](http://purl.obolibrary.org/obo/BFO_0000019){:target="_blank"}**, **[`planned processes`](http://purl.obolibrary.org/obo/OBI_0000011){:target="_blank"}**, and **[`information artifacts`](http://purl.obolibrary.org/obo/IAO_0000030){:target="_blank"}**, which all show up in process and data modelling.

The following documentation sections will focus on various parts needed to detail processes and their input and output data.  The diagram below shows how OBI expresses the statement "John's mass is 70kg" using triples, and the related material entity, process, datum, quality and value specification ontology components hovering in the background.  It shows the big picture - by tracing classes further up the inheritance hierarchy, we can see the impact on instance data. Details on each of these sections follow.

<img align="right" src="/assets/images/docs/data_john_mass_context.png">

([full-sized image](/assets/images/docs/data_john_mass_context.png){:target="_blank"})


## Material entities and their properties/qualities

Under `material entity` we find OBI's **[`organism`](http://purl.obolibrary.org/obo/OBI_0100026){:target="_blank"}** - the usual focus of biomedical investigations. Organism related terms - whether in OBI or in other ontologies that cover taxonomic, anatomic, developmental, pathological, environmental etc. aspects - will likely occur in study design objectives, protocols and experimental observations.

<img align="right" src="/assets/images/docs/data_john_mass_entity_property.png">

We use **entity property diagrams** to show material entities and selected object properties (that link them to qualities) and class-subclass relations, which together illustrate OBI core "terminological component" (Tbox) contents. In this example, a `material entity` [`has quality`](http://purl.obolibrary.org/obo/RO_0000086){:target="_blank"} some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125){:target="_blank"}. This axiom is not currently in OBI but is included to show the potential for relation inheritance.  Formally, `has quality` is a generic object property existing between a BFO independent continuent entity (the bearer) and a quality, which is a dependent continuent (i.e. something that depends on the existence of its continuent).  [`Homo sapiens`](http://purl.obolibrary.org/obo/NCBITaxon_9606){:target="_blank"} is shown as a descendent of `organism`, a subclass of `material entity`, so the descendants also inherit a mass quality that can be referenced.  (A dashed arrow between entities indicates that several intermediate classes have been omitted).

An optional rose-tinted box may be provided to illustrate how to compose instances of classes and relations - this is "assertion component" (Abox) content. Abox content can form the bulk of a triple-store graph database, with the reasoning axioms of related ontologies added separately when validation of data structures and models is desired. In this example it is stated that "John" is an instance of Homo sapiens, and bears an instance of mass (or mass quality) that can then be referenced by other expressions.

# ISSUE: How to define Quality?

BFO: a quality is a specifically dependent continuant that, in contrast to roles and dispositions, does not require any further process in order to be realized.

~ specifically dependent continuant that is ALWAYS realized.

PATO: A dependent entity that inheres in a bearer by virtue of how the bearer is related to other entities

e.g. if a bearer has a surface, and there is another entity "light" around, then the bearer can exhibit the quality "color"?


*A hard-line view is that a quality is only a directly measureable thing - something one measures instantaniously or over a short period of time.  An object's color, weight etc. This rules out age - because age is inevitably a calculation (a translation) of some other quality observation, or involves time, something not directly observable. It also rules out BMI, a calculation based on two qualities.*

*A looser position is that a quality can be a product of qualities: So body mass index (BMI) is a quality because it is a function of only mass and height.*

*Or we could let time in the door, allowing age to be a quality, a measure of interval, whose semantic bookends are not themselves qualities.*

***
<sup>1</sup>The ability of an ICE to bear information depends on the coding scheme and medium it inheres in, hence it is a generically dependent continuant.