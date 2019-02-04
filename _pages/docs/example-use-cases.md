---
layout: single
title: Example Use Cases
permalink: /docs/robot-intro/
sidebar:
  nav: "docs"
---

Here we present a fully documented worked example from two subdomains. 

# Molecular Interaction Experiments

*GULLY TO DO*

# Biobanking 

TURBO is principally concerned with patient demographics and clinical findings.  It also addresses the design and objectives of material- and data-processing steps.  It's less concerned with experimental results.  So being able to tie a wide range of literal types (numbers, categories, strings, dates, etc.) to instances of OBI classes is of higher concern than (for example) being able to capture the precision of a data value.

We would especially like to compare notes with other people or groups instantiating data in an RDF graph (as opposed to "just" using OBI terms for tagging)

Representative TURBO data items:
* patient identifiers (open-ended nominal strings)
* encounter identifiers (open-ended nominal strings)
* encounter dates, DOB, and age at time of donation
    - are bare dates acceptable in OWL2, or do we have to use datetimes?
* weight (always a decimal value, but the units could be pounds or kilograms)
* height (numerical, potentially using cm, feet and or inches, and therefore potentially a composite value)
    - Our height/length source data could look like any one of these: 174 cm, 68.5 total inches, 5 feet + 8.5 inches
* BMI (always a decimal value)
* gender/sex (using OMRSE gender identity datums and PATO biological sex classes as categories)
* diagnoses (using ICD-X classes as categories, via MONDO)
* tumor grades and cancer stages (using OBIB  classes as categories)
* medications (free text -> RxNorm terms)
* ethnicity/race
* clinical test results, like blood glucose concentration.
    - Need to capture the magnitude of the result, the units, and the type of test.

TURBO native data properties... could some of these be value specifications?
* has literal value
* has Boolean value
* has date value
* has textual value... mostly for provenance

Easy case:  How to model weights or heights, which may come out of a relational database in one form, and then get materialized in the graph in another form (most likely kg or cm)

![TURBO mass value specification example](https://raw.githubusercontent.com/PennTURBO/Turbo-Documentation/master/images/turbo_mass_measurement_instances_curated.png)

The magnitude of the mass is instantiated with datatype triples using the `has specified value` predicate, like this:

```
prefix obo: <http://purl.obolibrary.org/obo/>
prefix owl: <http://www.w3.org/2002/07/owl#>
<urn:04ee92b7d3dc3ba7359860aae7740da> obo:OBI_0002135 "72.7"^^owl:real .
```


