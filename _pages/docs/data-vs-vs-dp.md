
## Value specification vs data property

<img align="right" src="figs/data_john_data_properties.png">

Using value specifications to record entity qualities and other measurables reduces the need for a plethora of data properties. Rather than establish a `has age` data property, we express a value specification about age.  Both hold a value, but the latter allows us to focus on defining the semantics of the quality 'age' and its subclasses - `age since planting` etc. In this view a data property is analogous to a kind of compressed and semantically opaque value specification because a data property's semantic detail is limited to a few attributes (functional, domain, and range constraints). Examples of why they are limiting is described below.

Data property values don't support units directly. In the example diagram of John's data properties to right, is the `has weight` decimal value given in kilos or grams? Is height in meters or centimetres? Either assumptions are made about units associated with a data property, or a second set of data properties must be created to capture unit info.  Value specifications allow units to be expressed explicitly.

A data property doesn't support a relevant time of measurement value.  For example in the diagram, when was John's `has height` observed, and was it the same time as `has weight`, such that an accurate BMI can be calculated?  Admittedly, time differentiated data is rather complex to model in OWL. A pragmatic approach, if workable, is to only load data into an OWL reasoner platform that doesn't need to be differentiated by time. In the BMI example, we could assume height and weight data properties are adequately close in time that any derivative calculations are appropriate. OBI does offer annother approach detailed in the `Time-stamped datums` section.

For these reasons, OBI has a handful of data properties (e.g. `has specified value`), and a larger and growing set of measurement / setting / prediction datums and the material entity qualities that they are about, complements of PATO and other ontologies.

<img align="right" src="figs/data_john_properties_as_vs.png">

***EDITOR NOTES***

*This diagram doesn't show instance level data. should it?*

*Some fields such as "name" may not be involved in any process modelling, and so may not need to appear in OWL modelling/inference per se. However, a cohesive platform for querying data could extend 'value specification' to them. The advantage is that we can then know when merging two graphs, whether the name elements are intended to match if the aboutness statements of their value specifications match.  This is a data harmonization use-case.*

Shall we allow including ICE values directly, avoiding 'value specification' and just using a new 'has value' data property to connect an ICE to a value? For example a "person 'bearer of' some name"; "anon instance of person has value John".

Can we allow identifier string values in value specification? See: [issue 985](https://github.com/obi-ontology/obi/issues/985)

Next section: [`Data types`](data-types.md)


