---
layout: single
title: OBI Term Guidelines
permalink: /obi-term-guidelines/
---

OBI is a community effort, and we greatly appreciate submissions of new terms! Here are some tips to help you get started.

## Existing Terms

Before you submit a new term, please search [`OntoBee`](http://www.ontobee.org/) or [`BioPortal`](https://bioportal.bioontology.org/){:target="_blank"} or [`OLS`](https://www.ebi.ac.uk/ols/index){:target="_blank"} for the term you want and its synonyms. OBI might already include the term you want under a different name.

If you find a term that’s close enough, but would like additions or changes made to it, please submit a new ticket to our issue tracker and be sure to include:

- the name of the term in the title of the ticket
- the [`IRI`](https://en.wikipedia.org/wiki/Internationalized_resource_identifier){:target="_blank"} that identifies the term (something like [`http://pur l.obolibrary.org/obo/OBI_0000070`](http://purl.obolibrary.org/obo/OBI_0000070){:target="_blank"})
- a description of the changes you would like made and reasons for the changes

When you are ready, follow this link to create a new ticket: [`https://github.com/obi-ontology/obi/issues/new`](https://github.com/obi-ontology/obi/issues/new){:target="_blank"}

(A GitHub account is required.)

## New Terms

If you don’t find the term you’re looking for, but it’s within OBI’s scope of biomedical investigations, please suggest that we add it to OBI as a new term. We’ll need the following information before we can add your term (more details below):

1. editor preferred term: a unique, unambiguous label for the term in American English
1. alternative terms: common synonyms or translations
1. textual definition
1. definition source for the textual definition
1. logical definition (or parent term)
1. example of usage
1. term editor: your name, and that of any collaborators, as it should appear in OBI

When you’ve collected as much of this information as possible, please follow this link to submit a term request to our tracker:

[`https://github.com/obi-ontology/obi/issues/new`](https://github.com/obi-ontology/obi/issues/new){:target="_blank"}

(A GitHub account is required.)

## More Details

OBI belongs to the [`OBO Foundry`](http://obofoundry.org/){:target="_blank"} and strives to follow the [`OBO Foundry Principles`](http://www.obofoundry.org/principles/fp-000-summary.html){:target="_blank"}. We have rules for the [`minimal metadata [**broken link**`]() for every term, and we use the [`IAO Ontology Metadata`](https://code.google.com/archive/p/information-artifact-ontology/wikis/OntologyMetadata.wiki){:target="_blank"} annotations for them. Here are some more details about the information we require for each new term.

1. The **[`editor preferred term`](http://purl.obolibrary.org/obo/IAO_0000111){:target="_blank"}** is an unambiguous label that uniquely identifies the term within the OBO Foundry. There must be one and only one editor preferred term, and it must be in American English. It should not contain any acronyms or jargon words, and it should make sense when read outside the context of a scientific investigation. As you might expect, all these requirements combine to make many of OBI’s editor preferred terms long and ugly. But the most important thing is that they’re clear! (See also the OBO Foundry [`naming conventions`](http://www.obofoundry.org/principles/fp-012-naming-conventions.html){:target="_blank"}.)

2. There can be many **[`alternative term`](http://purl.obolibrary.org/obo/IAO_0000118){:target="_blank"}** annotations for a given term in OBI. They can include acronyms and jargon – in fact, if the editor preferred term spells out an acronym then it’s a good idea to put the abbreviated form in an alternative term annotation. They can be in any language, but make sure to specify which language if it is not American English so we can note that. Alternative term annotations do not have to be unique across OBI or the OBO Foundry.

3. The **[`textual definition`](http://purl.obolibrary.org/obo/IAO_0000115){:target="_blank"}** is the most important annotation because it expresses the meaning of your term. Definitions should have Aristotelian form: “An A is a B that C” where A is your new term, B is the parent term, and C spells out how A is a special kind of B. Every term needs one and only one textual definition, in American English, and definitions must be unique across the OBO Foundry. (See also the OBO Foundry Principle on [`textual definitions`](http://www.obofoundry.org/principles/fp-006-textual-definitions.html).)

4. Every textual definition should have a **[`definition source`](http://purl.obolibrary.org/obo/IAO_0000119){:target="_blank"}**. If you created the definition, then that source would be you, and we’ll record your name. If the definition was adapted from Wikipedia or some other website, then this annotation should contain the permanent URL. If it was adapted from a paper, use its [`DOI`](https://en.wikipedia.org/wiki/Digital_object_identifier){:target="_blank"} or PubMed URL.

5. The **logical definition** of a term is almost as important as the textual definition. I say “almost” because, in case of misunderstandings, the textual definition takes precedence. The logical definition expresses the meaning of the term in a machine-readable way using the [`Web Ontology Language (OWL) version 2`](https://www.w3.org/TR/owl2-overview/){:target="_blank"}. Most OBI terms are OWL Classes (i.e. general nouns) and every one of these requires a single parent class. Many of them have more complex logical definitions. If you aren’t comfortable specifying a logical definition, that’s fine. OBI developers are happy to help create one based on your textual definition.

6. One or more **[`example of usage`](http://purl.obolibrary.org/obo/IAO_0000112){:target="_blank"}** annotations can really clarify the meaning of a term. While the textual definition must be general enough to cover all cases, the examples provide specific cases that show the term in action. Examples of usage can be common cases that demonstrate the prototypical usage, or uncommon edge cases that delimit the scope of the term. While not strictly required, every new term should have one or more examples of usage.

7. Finally, we want to give you credit for your work. We will add one or more **[`term editor`](http://purl.obolibrary.org/obo/IAO_0000117){:target="_blank"}** annotations with your name, and the names of others who have collaborated on creating this term for OBI.
