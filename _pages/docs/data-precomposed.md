---
layout: single
title: Pre-composed and Post-composed terms
permalink: /docs/data-precomposed/
sidebar:
  nav: "docs"
---

*Mark's content  here*

## Anonymous nodes

**[`Anonymous or blank nodes`](https://en.wikipedia.org/wiki/Blank_node){:target="_blank"}** play key roles in ontolgies and triple store databases for storing a classes' component axioms and for holding query pattern matching structures. An anonymous node contains a data structure which has not itself been given a full URI resource identifier. (Internally, in a triple store database, an anonymous node has an identifier that relations can reference, but this is not a permanent URI like the ones issued to ontology terms.) Anonymous nodes will occur in de-serialized triple store databases and ontologies for any bracketed conjunction or disjunction expression, for example the "(A and B)" expression in an "X subClassOf (A and B)" axiom. 

OBI defines various "pre-composed" [`value specifications`](http://purl.obolibrary.org/obo/OBI_0001933){:target="_blank"} including [`mass value specification`](http://purl.obolibrary.org/obo/OBI_0001929){:target="_blank"}` but it doesn't have one for color.  One can logically achieve exactly the same thing by using the expression:

    "(`value specification` and `specifies value of` only `color`)"

On its own, that expression will match the same set of things wherever it is used.  If it is frequently needed, that may be a sufficient reason for adding a `color value specification` term to OBI. 

Anonymous node expressions are used to avoid combination bombs of terms.  For example, tuberculosis can occur in many parts of the body - pulmonary, knee, a particular bone, one of 500+ lymph nodes - but to create a term for TB x body part x location would lead to an overwhelming number of terms as far as a human is concerned (e.g. mediastinal lymph node tuberculosis), and we haven't even turned to cancer.  An ontology design question for a biomedical investigation study design is to see how much it can rely on anonymous class expressions to hold data and match patterns being sought. Conversely, which expressions are frequently used and so merit precomposed terms?