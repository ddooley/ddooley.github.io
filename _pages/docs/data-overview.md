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
