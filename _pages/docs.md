---
layout: default
title: Documentation
permalink: /docs/
sidebar:
  nav: "docs"
---

[//]: # (Please put comments like this one into the text to communicate with other OBI-ers)

This user manual is designed to explain the core functionality of OBI for newcomers, and to serve as a canonical reference for OBI developers. This is a work in progress, but here we detail and provide a roadmap for OBI building blocks.  In addition to reasoning prowess, using OBI and other OWL ontologies to detail types of assay data - parameters, measurables, independent and dependent variables - will encourage standardization of their usage, enable experimental reproducibility, and facilitate data exchange and conversion.

* **[Core Class Definitions](/docs/core-classes/)**: basic formulation of the types found in the ontology - start here to learn components of a biomedical investigation
* **[Data Modelling](/docs/data-intro/)**: explains how material entity qualities are modeled as process inputs and outputs, and how to define value specifications associated with them for data collection and analysis.)
* **[Process Modelling](/docs/process-intro/)**: explains how to carry out a strategy of top-down modelling)
* **[Data Types](/docs/data-types/)**: Basic ways to represent numeric, categorical, date, and duration datums)
* **[Robot Driven Templates](/docs/robot-intro)**: Chunks of OBI are composed using ROBOT by reading spreadsheets of term definitions.

<!-- 
* **Extended Class Definitions** (working models for specific subdomains and specializations of OBI beyond the core classes) 
* **Example Use Cases** (how we describe specific use cases with OBI) 
* **Implementation and Development Notes** (how we develop, extend and implement the ontology)
* **Community** (Description of the OBI development community. Who were are and what our goals are for this work)
-->

More background and detail on OBI vocabulary and functionality is available in papers listed on the [Media](/media/) page.

Most documentation diagrams are contained in a [/assets/files/data_obi3_draw.io.xml](/assets/files/data_obi3_draw.io.xml){:target="_blank"} file, in [draw.io](http://draw.io){:target="_blank"} diagram format for reuse in ontology design work.  The diagrams usually skip relation cardinality details (e.g. "X 'is about' {some / all / max 3 / only} Y"), but these do exist in OBI to enforce more structure, and are detailed in OWL code examples.

In the documentation, the first usage of an ontology term like [`patient role`](http://purl.obolibrary.org/obo/OBI_0000093) is hyperlinked to its PURL (permanent URL) web addresses for easy reference, usually on the Ontobee lookup servce where its position in the class hierarchy is shown, as well as equivalency and other subclass axioms, synonyms, definition, etc.


