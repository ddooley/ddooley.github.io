---
layout: default
title: Data Sets
permalink: /docs/data-sets/
sidebar:
  nav: "docs"
---

[//]: # (Please put comments like this one into the text to communicate with other OBI-ers)

A collection of datums of a given data type is called a [`data set`](http://purl.obolibrary.org/obo/IAO_0000100){:target="_blank"}. A numeric data set (like a numeric spreadsheet column) can have statistical calculations performed on it by using an RDF query language like [SPARQL](https://en.wikipedia.org/wiki/SPARQL).  The [`member of`](http://purl.obolibrary.org/obo/RO_0002350){:target="_blank"} relation can connect datum or value specification instances to such a data set.

James Overton offers a detailed tutorial in how to convert a spreadsheet to an ontology-driven triple store graph.  He provides a script for [`mapping`](https://github.com/jamesaoverton/obo-tutorial/blob/master/docs/using-and-reusing.md#mapping-terms) spreadsheet cell contents to ontology equivalents, assuming you have set up sufficient ontology to steer the conversion.  As well, the next step is to convert this to a [`triple store graph`](https://github.com/jamesaoverton/obo-tutorial/blob/master/docs/processing-data.md).
