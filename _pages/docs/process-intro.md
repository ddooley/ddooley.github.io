---
layout: single
title: ""
permalink: /docs/process-intro/
toc: true
sidebar:
  nav: "docs"
---

# Process model basics

[//]: # (Please put comments like this one into the text to communicate with other OBI-ers)

Generally a **[`process`](http://purl.obolibrary.org/obo/BFO_0000015){:target="_blank"}** can have other processes as parts, and can have instances with start and end times associated with them.  A **[`planned process`](http://purl.obolibrary.org/obo/OBI_0000011){:target="_blank"}** is carried out by agent(s) who are guided by some kind of **[`plan specification`](http://purl.obolibrary.org/obo/IAO_0000104){:target="_blank"}**, an ICE which has **[`objective`](http://purl.obolibrary.org/obo/IAO_0000005){:target="_blank"}** and **[`action`](http://purl.obolibrary.org/obo/IAO_0000007){:target="_blank"}** components. A **[`study design`](http://purl.obolibrary.org/obo/OBI_0500000){:target="_blank"}** and its **[`protocol`](http://purl.obolibrary.org/obo/OBI_0000272){:target="_blank"}** part(s) are subclasses of `plan specification`. This is documented in the [`Core Classes`](/docs/core-classes/) page.

<img align="right" src="/assets/images/docs/data_assay_2.png">

A **process / datum model diagram** shows how material entities or data items can be an input or output of some process. This diagram often includes parts of entity property diagrams in order to reference components as inputs or in aboutness clauses.

The **[`assay`](http://purl.obolibrary.org/obo/OBI_0000070){:target="_blank"}** process diagram to right details axioms that enable types of assay to inherit requirements: [paraphrasing] that an assay input is a material entity playing an evaluant role, and that an assay outputs one or more data items.

<br clear="both">


<img align="right" src="/assets/images/docs/data_john_mass_process.png">

The next example shows a **[`mass measurement assay`](http://purl.obolibrary.org/obo/OBI_0000445){:target="_blank"}** which takes in some material and outputs a **[`mass measurement datum`](http://purl.obolibrary.org/obo/IAO_0000414){:target="_blank"}**.  The output datum is stated to be a measure of (only) mass quality. The **[`is quality measurement of`](http://purl.obolibrary.org/obo/IAO_0000221){:target="_blank"}** object property is actually a sub-property of `is about` which is used when the target of aboutness is a quality.

The Abox shows John as an input (standing on a scale, say), and documents that a `mass measurement datum` has been taken by the `mass measurement assay`. A process modeller can work at this more abstract level, avoiding references to specific protocols or instruments involving, say, units of measure. Alternately, by merging process modelling with specific value specifications (described below), we can describe particular equipment used in an experimental protocol or execution - say a brand and model of weight scale that is only capable of measuring in grams. (That level of detail promotes an ontology-driven plug-and-play future of equipment selection and protocol design.)

## Processes with inputs playing roles

**Mark's doctor/patient interaction event example here....**

Processes can have other participants besides inputs and outputs, such as operators and material consumables.






## Material processing

<img align="right" src="/assets/images/docs/data_processed_material.png">

Processes don't necessarily generate information products.  The OBI [`material processing`](http://purl.obolibrary.org/obo/OBI_0000094){:target="_blank"} class covers many kinds of process such as sample preparation, manufacturing, and staining. [`Processed specimen`](http://purl.obolibrary.org/obo/OBI_0000953){:target="_blank"} is likely needed as part of experimental protocol modeling involving biosamples. It remains a material entity, rather than a `data item` that assays output.
