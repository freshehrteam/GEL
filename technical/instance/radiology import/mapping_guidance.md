# General principles

1. Every coded entry in openEHR needs a value (the textual representation or rubric), a code (the formal terminology code) and a terminology (e.g. SNOMED-CT).

```json
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code|value" : "CAPUG TERM",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code|code" : "CAPUG",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code|terminology" : "NICIP",
```

2. In addition you can add one or more mappings to other terminologies, and each of the mappings need a match (almost always '='), a code (the formal terminology code) and a terminology (e.g. SNOMED-CT).  Optionally you can also add a purpose (e.g. SNOMED-CT concept or SNOMED-CT description) to provide additional clarity. Mappings cannot currently carry textual representations or rubrics.

```json
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0|match" : "=",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0|purpose" : "SNOMED CT concept",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0/target|code" : "350981",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0/target|terminology" : "SNOMED-CT",
```

3. As a rule we have used the local or GEL terminologies as the primary terminology and mapped out to SNOMED-CT or OPCS-4, but you can switch those around if you find that most of the incoming data uses an external terminology - each data point can be different in this respect.

4. The key data points for coding and mapping are *imaging code*, *modality (or method)*, *anatomical location* and *anatomical side (or laterality)*, and each of these has their own value/code/terminology group and at least one mapping. The *imaging code* has three mappings:

```json
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code|value" : "CAPUG TERM",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code|code" : "CAPUG",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code|terminology" : "NICIP",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0|match" : "=",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0|purpose" : "SNOMED CT concept",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0/target|code" : "350981",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:0/target|terminology" : "SNOMED-CT",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:1|match" : "=",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:1|purpose" : "SNOMED CT description",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:1/target|code" : "350982",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:1/target|terminology" : "SNOMED-CT",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:2|match" : "=",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:2|purpose" : "OPCS-4 PRIMARY CODE",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:2/target|code" : "350984",
"radiology_result_report/imaging_examination_result:0/any_event:0/imaging_code/_mapping:2/target|terminology" : "OPCS-4",
```
