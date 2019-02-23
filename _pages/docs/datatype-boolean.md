---
layout: default
title: Boolean Datum
permalink: /docs/datatype-boolean/
toc: true
sidebar:
  nav: "docs"
---

Under discussion is the formalization of a "boolean value specification" datatype that pertains to the presence
or absence of a quality or categorical entity. Essentially any quality taken on its own can be treated as a boolean variable.  The information that an animal is characterized as a [`neonate`](http://www.ebi.ac.uk/efo/EFO_0001372){:target="_blank"}, for example may be the focus of interest in a study even if a more comprehensive categorical value specification of its [`developmental stage`](http://www.ebi.ac.uk/efo/EFO_0000399){:target="_blank"} could have been posed as a Likert scale.

<!-- 
[//]: # (    Class: 'boolean value specification'
        subClassOf 'has specified value' only xsd:boolean
)
[//]: # (        subClassOf 'boolean value specification')
-->

    Class: 'neonate value specification'
        subClassOf 'value specification'
        subClassOf 'has specified value' only xsd:boolean
        subClassOf 'specifies value of' only 'neonate' 

Any categorical value specification choice instance can potentially be interpretable as a boolean too.
