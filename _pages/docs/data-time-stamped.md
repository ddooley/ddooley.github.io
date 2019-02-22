---
layout: default
title: Time stamped data
permalink: /docs/time-stamped-data/
sidebar:
  nav: "docs"
---

Process models and data items can be enhanced with time information in a few ways.   

- Assays and other processes can be marked with start and/or stop times, and therefore any specified output could have those time points to mark its relevance. 

## OBI allows time-stamped datums via both datum parthood, and via the VS approach!

## Time stamped data via datum parthood

Alan Ruttenberg, Melanie Courtot & others created this structure which is simple enough if connecting data properties directly; it ends up looking too complicated when used with value specifications. It illustrates datums being part of a datum, using `part of` subproperties to disambiguate the time dimension from the other (one or more) measurement datum components.

Using:

- [`time stamped measurement datum`](http://purl.obolibrary.org/obo/IAO_0000582)
  - [`has time stamp`](http://purl.obolibrary.org/obo/IAO_0000416)
    - [`time measurement datum`](http://purl.obolibrary.org/obo/IAO_0000416) that has only [`measurement unit label`](http://purl.obolibrary.org/obo/IAO_0000039) some [`time unit`]()
  - [`has measurement datum`](http://purl.obolibrary.org/obo/IAO_0000583) 
    - [`measurement datum`](http://purl.obolibrary.org/obo/IAO_0000109) 

 
<img src="/assets/images/docs/data_timestamp_length.png">

An example, using `has content datum` rather than `has measurement datum` when object isn't necessarily a measurement datum. `has time stamp` is a subproperty of `has part`

    `time stamped measurement datum`:
    - `has time stamp` exactly 1 `time measurement datum` 
    - `has measurement datum` some `measurement datum`

    `geolocation coordinate datum`:
    - `has content datum` exactly 1 `latitude datum` 
    - `has content datum` exactly 1 `longitude datum`

    `time stamped geolocation coordinate datum`:
    - `has time stamp` exactly 1 `time measurement datum` 
    - `has content datum` exactly 1 `geolocation coordinate datum`


## Time stamped data via value specifications

- Any datum's existing value specification(s) can be accompanied by a time value specification, effectively making it a 2-dimensional or n-dimensional observation. In other words, value specifications, as long as they are unambiguously about (`specifies value of`) different things, are additive. 

Here is a diagram showing a generic "time stamped measurement datum" that is about some time and quality.

<img src="/assets/images/docs/data_timestamp_datum_2.png">

More specifically, here's a `time stamped geolocation datum` about a latitude and longitude. It references two seperate value specifications which have degree units but are distinguishable by what they are about. Each of these value specifications could detail (i.e. be the metadata for) a column in a spreadsheet. The instance tripple below would be the conversion into owl/rdf of the row fields.

<img src="/assets/images/docs/data_timestamped_geolocation_3.png">

In summary, n-dimensional datums are achieved by either:

<img src="/assets/images/docs/data_timestamp_datum_conjunction.png">

