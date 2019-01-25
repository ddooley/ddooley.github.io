
## Duration

A duration is a difference in time calculated from an interval of two time points. (Semantically the interval is about those points and the events they mark). Value specifications for date and time durations or intervals are generally handled by decimal value specifications with one or more time units attached to them. This allows for decimal fraction amounts, e.g. 2.5 days. An 'age since birth' value specification could be:

<!--
[//]: # (Class: 'duration value specification'
        subClassOf 'value specification'
        subClassOf 'specifies value of' only xsd:decimal
)
[//]: # (        subClassOf 'duration value specification')
-->

    Class: 'age since birth value specification'
        subClassOf 'scalar value specification'
        subClassOf 'has specified value' only xsd:decimal
        subClassOf 'specifies value of' some 'age since birth'
        subClassOf 'has measurement unit label' only (year or month or day or hour)

## Datetime

Of XML's native date/time datatypes, OWL has currently adopted [xsd:date](http://www.datypic.com/sc/xsd11/t-xsd_date.html), [xsd:datetime](http://www.datypic.com/sc/xsd11/t-xsd_dateTime.html) (format [-]CCYY-MM-DDThh:mm:ss.sss[Z|(+||-)hh:mm] according to the ISO 8601 standard) and [xsd:dateTimeStamp](http://www.datypic.com/sc/xsd11/t-xsd_dateTimeStamp.html) (format CCYY-MM-DDThh:mm:ss.sss(Z||(+||-)hh:mm), i.e. time zone required) into its reasoning specification.  A Gregorian calendar 24 hour clock instant of time is used, and will be compared down to the second and timezone offset for xsd:dateTime/Stamp formats.

<!--
[//]: # (    Class: 'date value specification'
        subClassOf 'value specification'
        subClassOf 'has specified value' only xsd:date
)
[//]: # (        subClassOf 'date value specification')
-->

    Class: 'hospital admission date specification'
        subClassOf 'scalar value specification'
        subClassOf 'has specified value' only xsd:date
        subClassOf 'specifies value of' only 'hospital admission date'

Often a need for date obfuscation arises when dealing with confidential data points. Pairing a unit such as year, month, day, hour etc. can convey the semantic granularity of the given xsd:datetime but won't have an effect on reasoner equality test, so the remainder of the datetime components need to be the same (zero'ed out for example) in order for an equality constraint to succeed.  This could be done as a pre-processing step.

If a more complex model of date/time is required, the "Time Ontology in OWL"<sup>4,5</sup> may suffice. 

