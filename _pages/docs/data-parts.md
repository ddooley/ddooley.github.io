---
layout: default
title: Describing parts
permalink: /docs/data-parts/
toc: true
sidebar:
  nav: "docs"
---

In the case where a value specification and/or measurement datum is about the conjunction of a few different things, the aboutness target can be a postcomposed expression of those components, with one component, usually a quality, providing the primary type of the measure.  For example "eye color" is primarily about color - and so limited to ways that can be reported, but secondarily about the body part being observed, and finally - in the instance, references a particular organism being observed. 

<img align="right" src="/assets/images/docs/data_john_eye.png">

Here is an example generic value specification pointing to John's eye color being brown (in this case "specifies value of" points directly to the value specification's essentially categorical value. 

This is our first example of measuring a quality of a part of something. An instance of the Uberon ontology [`eye`](http://purl.obolibrary.org/obo/UBERON_0000970) is part of an instance of Homo sapiens, and 'has quality' some instance of PATO [`brown`](http://purl.obolibrary.org/obo/PATO_0000952).  An instance of the add-on `color value specification` class points to the `brown` instance as well. `color value specification` class points to any subclass of [`color`](http://purl.obolibrary.org/obo/PATO_0000952) as being permitted for the instance.

"Homo sapiens has part some eye" is a parthood simplification for what some might need to model in a more complicated way.  For example, ophthalmologists need to distinguish left and right eyes, and allow each to have different iris colors (it happens!), and to describe the color of sclera or conjunctiva (e.g. for red eye or pink eye).  Uberon supports this with `left eye` and `right eye` terms as subclasses of `eye`, and says "`eye` `part of` some `visual system`" but it stops short of establishing a parthood chain between `eye` and `mammalia`.  In the future such standardizing axioms may be introduced which client ontologies and triple store databases can employ to ensure data structure compatibility.  Regardless, it is usually ok to use a simple `part of` relation to abbreviate a more intricate parthood chain if it fits your needed granularity of description.