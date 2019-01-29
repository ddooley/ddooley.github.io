---
layout: single
title: Time-stamped Datums
permalink: /docs/time-stamped-datums/
sidebar:
  nav: "docs"
---

Process models and data items can be enhanced with time information in a few ways.   

- Assays and other processes can be marked with start and/or stop times, and therefore any specified output would have those time points to mark its relevance [**using which relations????**]. 

- Any datum's existing value specification(s) can be accompanied by a time value specification, effectively making it a 2-dimensional or n-dimensional observation.

<img src="/assets/images/docs/data_timestamp_datum_2.png">

<br clear="both">

<img src="/assets/images/docs/data_timestamped_geolocation_3.png">

In OBI a [`time stamped measurement datum`](http://purl.obolibrary.org/obo/IAO_0000582) exists to associate time directly with a datum; however this older term is complex (it offers a datum within a datum) and may be retired.