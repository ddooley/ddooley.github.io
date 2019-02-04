---
layout: single
title: Body Mass Index Example
permalink: /docs/data-bmi/
toc: false
sidebar:
  nav: "docs"
---

The Body Mass Index example explains how OBI models the basic BMI calculation (mass / height^2) in terms of processes, datums, qualities, and value specifications.  The actual BMI value calculation would likely be set by SPARQL say, rather than a reasoner which is ok at comparisons but not arithmetic. The entity property diagram states what type of thing the inputs and outputs for BMI are.

<img src="/assets/images/docs/data_john_bmi_properties.png">

Here the various processes for generating input and output are detailed.

<img src="/assets/images/docs/data_john_bmi_process.png">

The value specification diagram details the tripple store or tabular data metadata required to carry out the calculation.

<img src="/assets/images/docs/data_john_bmi_vs.png">

The full context view shows an instance of the subject, processes applied, and measured or calculated output. 

<img src="/assets/images/docs/data_john_bmi_context.png">
[full-sized image](/assets/images/docs/data_john_bmi_context.png)
