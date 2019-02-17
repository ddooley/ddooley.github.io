---
layout: default
title: "Process timing"
permalink: /docs/process-timing/
toc: true
sidebar:
  nav: "docs"
---

## Marking process start, end and duration

#### *Looks like this will be a topic discussed at upcomming US2TS meeting???*

Process timing can be abstractly conveyed via the dependencies established between processes using `has specified input` and `has specified output`.  However, for experimental protocols, plans, or in observed results it may be necessary to indicate specific start and end times and process durations.

### ISSUES:

- Do we allow `is duration of` (subproperty of `is about`) for start, end and duration? Do we make them qualities (e.g. birth date = (`date process started` and `quality of` mammal ...) and then use `has quality` relation?
  - Do we allow these dates to have [`date process started`](http://purl.obolibrary.org/obo/OBI_0002471) `has xsd:dateTime value` yyyy-mm-ddThh:mm:ss?
  - **if `process start date` and `end date` are datums, then shouldn't `age` be as well**? 
Datum [`is duration of`](http://purl.obolibrary.org/obo/IAO_0000413) entity if datum is a [`time measurement datum`](http://purl.obolibrary.org/obo/IAO_0000416) that is a duration of a process.  This also inludes links to the [`date process started`](http://purl.obolibrary.org/obo/OBI_0002471) or `process end date` datetime value of a process (in that case the duration about the reference calendar start to the given start or ending timepoint.)


<img src="/assets/images/docs/data_process_datetime.png">

<img src="/assets/images/docs/data_process_datetime_context.png">
