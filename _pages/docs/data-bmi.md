---
layout: default
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

Here a direct datum / data property structure is illustrated, showing (in ABox) instance data that can be used to carry out the calculation. Mass, Length and body fat ratio terms are shown for contextual information but aren't necessary as far as instance data is concerned.

<img src="/assets/images/docs/data_john_bmi_data_properties.png">

The alternative value specification diagram.

<img src="/assets/images/docs/data_john_bmi_vs.png">

The value specification full context view shows an instance of the subject, processes applied, and measured or calculated output. 

<img src="/assets/images/docs/data_john_bmi_context.png">
[full-sized image](/assets/images/docs/data_john_bmi_context.png)
