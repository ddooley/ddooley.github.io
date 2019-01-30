---
layout: single
title: Information content entities
permalink: /docs/data-ice/
toc: false
sidebar:
  nav: "docs"
---

All information items that are derived from material entities (i.e. statements that reference material qualities and are factual claims about an entity) fall under the domain of **[`information content entity`](http://purl.obolibrary.org/obo/IAO_0000030){:target="_blank"}** (ICE), very generally defined as a type of entity which bears information about something<sup>1</sup>.  Any ICE class may have **[`is about`](http://purl.obolibrary.org/obo/IAO_0000136){:target="_blank"}** object relations that connect it to other material entities or ICEs which define its _aboutness_.  Examples: an "[`age since planting measurement datum`](http://purl.obolibrary.org/obo/OBI_0001156){:target="_blank"} `is about` some [`Spermatophyta`](http://purl.obolibrary.org/obo/NCBITaxon_58024){:target="_blank"}" (among other things); a "[`minimal inhibitory concentration`](http://purl.obolibrary.org/obo/OBI_0001514){:target="_blank"} `is about` some [`dose response curve`](http://purl.obolibrary.org/obo/OBI_0001172){:target="_blank"}", another ICE.  Aboutness axioms should reinforce the content of term definitions.  

[//]: #(The defining characteristic of an `Information Content Entity` is that it is 'about' something. Thus, the scope of the OBI representation of data is to capture the details and characteristics of the information, rather than the thing that it describes. This is a crucial scoping step in developing representations in OBI.)

<img align="right" src="/assets/images/docs/data_iao_branch.png">

The `information content entity` **[`data item`](http://purl.obolibrary.org/obo/IAO_0000027){:target="_blank"}** class holds singular entities or collections of entities that specifically record inputs or outputs of processes / equipment / human interaction. OBI distinguishes the following singular types of data items, usually called "datums", as follows:

* A **[`measurement datum`](http://purl.obolibrary.org/obo/IAO_0000109){:target="_blank"}** class names and models the datum outputs of an assay, and their contextual semantics. 
* A **[`settings datum`](http://purl.obolibrary.org/obo/IAO_0000140){:target="_blank"}** class which enables modeling an apparatus control input.
* A **[`predicted data item`](http://purl.obolibrary.org/obo/OBI_0302867){:target="_blank"}** class that applies to output of a [`prediction`](http://purl.obolibrary.org/obo/OBI_0302910){:target="_blank"} process.

All ICEs are allowed a **[`value specification`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"}** that records some pertinent categorical or numeric value about an entity; more on this in the data collection section.
