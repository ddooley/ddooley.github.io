---
layout: default
title: Data Overview
permalink: /docs/data-overview/
sidebar:
  nav: "docs"
---
This set of diagrams attempts to set a future target for how we want to evolve the ability of OBI to describe data. It aims to expose how we'd apply a new roster of `has rdfs:Literal` datatypes to datums directly, or via value specifications.  THESE ARE DAMION'S opinions so far ... throwing it out to you all ...

Here is an overview diagram of how OBI is basically using `value specifications` for capturing numeric values; and has a `has measurement unit labe l` and `has measurement value` combo that allows any datum to be connected to a unit and rdfs:Literal or other datatype. The approach is focused currently on "measurement datum", though full process modelling will often require setting and prediction datums too.

![Current OBI Datum Value Structure](/assets/images/docs/data_overview_current.png)

<hr/>

### Data Item and Value Primitives

I think what we need is a low-level vocabulary (set of entities) that we can use as building blocks for post-composing measurement, setting, prediction, etc. datums.

![Datum Role x Measurement type x RDFS ](/assets/images/docs/data_overview_matrix.png)

<hr/>

### Data Item to Data Property
Then this would be a datum-data-property focused solution, which echoes previous work done on the `time stamped measurement datum`.  Note it doesn't really need numeric value specification. But it needs something like the `categorical value specification`.

![Datum + Data Properties ](/assets/images/docs/data_overview_datum.png)

<hr/>

### Data Item to Value Specification

And here is a `value specificaiton` friendly approach, which has only 1 `has string representation` linkage to `data item`; all other uses of `rdfs:Literal` find themselves inside new `value specification` subclasses.  This doesn't provide a `data item` rdfs:integer or rdfs:decimal shortcut to set a unitless number, or a string identifier, URI, etc.

![Datum + Value Specification ](/assets/images/docs/data_overview_vs.png)

<hr/>

### Notes about current OBI setup:

A `has xsd:Literal value` or `has measurement value` data property can be attached directly to an instance of a datum in the case of numeric measurements, and those qualities inherently come with `has measurement unit label` abstractly set to the base SI unit of quality dimension in question, so its easy to express "length of 2m", "weight of 50kg" that way.  What motivates us to use a value spec in this case?  The theoretical distinction exists between a datum as a process input/output that should only describe its aboutness; and a value specification that specifies the measurement value's form, seems to be blown with respect to qualities about SI dimensions. The current feature of allowing datums to be associated with units would need to be dropped to enforce the distinction. But this seems to deny the fundamental semantics of what these SI datums have?!

As well, in relation to processes, is it so easy to say that a datum is the specified output of a process, rather than a value specfication?  The diagram below points out that many processes are realizations of functions provided by devices - devices with very specific I/O.  A specific process may output a weight reading in grams. Is it in fact the datum that should be attached to the VS, rather than the other way around?


![Datum and Value Specification](/assets/images/docs/data_datum_vs.png)
