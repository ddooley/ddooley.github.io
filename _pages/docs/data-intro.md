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

<img align="right" src="/assets/images/docs/data_john_mass.png">

([full-sized image](/assets/images/docs/data_john_mass.png){:target="_blank"})


## Material entities and their properties/qualities

Under `material entity` we find OBI's **[`organism`](http://purl.obolibrary.org/obo/OBI_0100026){:target="_blank"}** - the usual focus of biomedical investigations. Organism related terms - whether in OBI or in other ontologies that cover taxonomic, anatomic, developmental, pathological, environmental etc. aspects - will likely occur in study design objectives, protocols and experimental observations.

<img align="right" src="/assets/images/docs/data_john_mass_entity_property.png">

We use **entity property diagrams** to show material entities and selected object properties (that link them to qualities) and class-subclass relations, which together illustrate OBI core "terminological component" (Tbox) contents. In this example, a `material entity` [`has quality`](http://purl.obolibrary.org/obo/RO_0000086){:target="_blank"} some [`mass`](http://purl.obolibrary.org/obo/PATO_0000125){:target="_blank"}. This axiom is not currently in OBI but is included to show the potential for relation inheritance.  Formally, `has quality` is a generic object property existing between a BFO independent continuent entity (the bearer) and a quality, which is a dependent continuent (i.e. something that depends on the existence of its continuent).  [`Homo sapiens`](http://purl.obolibrary.org/obo/NCBITaxon_9606){:target="_blank"} is shown as a descendent of `organism`, a subclass of `material entity`, so the descendants also inherit a mass quality that can be referenced.  (A dashed arrow between entities indicates that several intermediate classes have been omitted).

An optional rose-tinted box may be provided to illustrate how to compose instances of classes and relations - this is "assertion component" (Abox) content. Abox content can form the bulk of a triple-store graph database, with the reasoning axioms of related ontologies added separately when validation of data structures and models is desired. In this example it is stated that "John" is an instance of Homo sapiens, and bears an instance of mass (or mass quality) that can then be referenced by other expressions.

## Anonymous nodes

**[`Anonymous or blank nodes`](https://en.wikipedia.org/wiki/Blank_node){:target="_blank"}** play key roles in ontolgies and triple store databases for storing data and for holding logical pattern matching structures. An anonymous node contains a data structure which has not itself been given a full URI resource identifier. The diagram above shows an anonymous node (always with a dashed perimiter) that is of type `Homo sapiens` which would also have an annotation or data property of name "John", and which has a `has quality` relation to another anonymous node of type `mass`. The bulk of instance data is made with them. Internally, in a triple store database, an anonymous node has an identifier that relations can reference, but this is not a permanent URI like the ones issued to ontology terms.

Anonymous nodes will occur in de-serialized triple store databases and ontologies for any bracketed conjunction or disjunction expression, for example the "(A and B)" expression in an "X subClassOf (A and B)" axiom. 

The other essential use of an anonymous node is to reference a class of thing without having to assign a new ontology term to it - this is called an anonymous class. For example, OBI defines various "pre-composed" [`value specifications`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"}` including [`mass value specification`](http://purl.obolibrary.org/obo/OBI_0001929){:target="_blank"}` but it doesn't have one for color.  For now one can logically achieve exactly the same thing by using the expression "(`value specification` and `specifies value of` only `color`)" instead. On its own, that expression will match the same set of things wherever it is used.  If it is frequently needed, that may be a sufficient reason for adding a `color value specification` term to OBI. 

Anonymous node expressions are used to avoid combination bombs of terms.  For example, tuberculosis can occur in many parts of the body - pulmonary, knee, a particular bone, one of 500+ lymph nodes - but to create a term for TB x body part x location would lead to an overwhelming number of terms as far as a human is concerned (e.g. mediastinal lymph node tuberculosis), and we haven't even turned to cancer.  An ontology design question for a biomedical investigation study design is to see how much it can rely on anonymous class expressions to hold data and match patterns being sought. Conversely, which expressions are frequently used and so merit a pre-composed term? 

## Information content entities

All information items that are derived from material entities (i.e. statements that reference material qualities and are factual claims about an entity) fall under the domain of **[`information content entity`](http://purl.obolibrary.org/obo/IAO_0000030){:target="_blank"}** (ICE), very generally defined as a type of entity which bears information about something<sup>1</sup>.  Any ICE class may have **[`is about`](http://purl.obolibrary.org/obo/IAO_0000136){:target="_blank"}** object relations that connect it to other material entities or ICEs which define its _aboutness_.  Examples: an "[`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156){:target="_blank"} `is about` some [`Spermatophyta`](http://purl.obolibrary.org/obo/NCBITaxon_58024){:target="_blank"}" (among other things); a "[`minimal inhibitory concentration`](http://purl.obolibrary.org/obo/OBI_0001514){:target="_blank"} `is about` some [`dose response curve`](http://purl.obolibrary.org/obo/OBI_0001172){:target="_blank"}", another ICE.  Aboutness axioms should reinforce the content of term definitions.  

[//]: #(The defining characteristic of an `Information Content Entity` is that it is 'about' something. Thus, the scope of the OBI representation of data is to capture the details and characteristics of the information, rather than the thing that it describes. This is a crucial scoping step in developing representations in OBI.)

<img align="right" src="/assets/images/docs/data_iao_branch.png">

The `information content entity` **[`data item`](http://purl.obolibrary.org/obo/IAO_0000027){:target="_blank"}** class holds singular entities or collections of entities that specifically record inputs or outputs of processes / equipment / human interaction. OBI distinguishes the following singular types of data items, usually called "datums", as follows:

* A **[`measurement datum`](http://purl.obolibrary.org/obo/IAO_0000109){:target="_blank"}** class names and models the datum outputs of an assay, and their contextual semantics. 
* A **[`settings datum`](http://purl.obolibrary.org/obo/IAO_0000140){:target="_blank"}** class which enables modeling an apparatus control input.
* A **[`predicted data item`](http://purl.obolibrary.org/obo/OBI_0302867){:target="_blank"}** class that applies to output of a [`prediction`](http://purl.obolibrary.org/obo/OBI_0302910){:target="_blank"} process.

All ICEs are allowed a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"}** that records some pertinent categorical or numeric value about an entity; more on this in the data collection section.

***
<sup>1</sup>The ability of an ICE to bear information depends on the coding scheme and medium it inheres in, hence it is a generically dependent continuant.