#### Heading

### Lab Results  Import

#### Version:

1.0.0

25 Jan 2017

#### TemplateID:
`GEL - Generic Lab Report import.v0`

#### Summary AQL /query:

To populate the list of items when the heading is selected.

```
select
a/uid/value as uid,
a/composer/name as author,
a/context/start_time/value as date_created,
    a_b/data[at0001]/origin/value as sample_time,
    a_b/data[at0001]/events[at0002]/data[at0003]/items[at0005]/value/value as test_name,
    a_b/data[at0001]/events[at0002]/data[at0003]/items[at0005]/value/defining_code/code_string as test_name_code,
    a_b/data[at0001]/events[at0002]/data[at0003]/items[at0005]/value/defining_code/terminology_id/value as test_name_terminology,
    a_b/data[at0001]/events[at0002]/data[at0003]/items[at0073]/value/value as status,
    a_b/data[at0001]/events[at0002]/data[at0003]/items[at0057]/value/value as conclusion,
    a_a/items[at0002]/name/value as Laboratory_result_header,
    a_a/items[at0002]/items[at0001]/name/value as result_name,
    a_a/items[at0002]/items[at0001]/name/defining_code/code_string as result_name_code,
    a_a/items[at0002]/items[at0001]/name/defining_code/terminology_id/value as result_name_terminology,
    a_a/items[at0002]/items[at0001]/value/magnitude as result_magnitude,
    a_a/items[at0002]/items[at0001]/value/units as result_units,
    a_a/items[at0002]/items[at0001]/value/normal_range/lower/magnitude as normal_range_lower,
        a_a/items[at0002]/items[at0001]/value/normal_range/lower/units as normal_range_lower_units,
    a_a/items[at0002]/items[at0001]/value/normal_range/upper/magnitude as normal_range_upper,
        a_a/items[at0002]/items[at0001]/value/normal_range/upper/units as normal_range_upper_units,
    a_a/items[at0002]/items[at0001]/value/normal_range/lower_included as lower_included,
    a_a/items[at0002]/items[at0001]/value/normal_range/upper_included as upper_included,
    a_a/items[at0002]/items[at0001]/value/normal_range/lower_unbounded as lower_unbounded,
    a_a/items[at0002]/items[at0001]/value/normal_range/upper_unbounded as upper_unbounded
from EHR e[ehr_id/value='{{ehrId}}']
contains COMPOSITION a
contains
    OBSERVATION a_b[openEHR-EHR-OBSERVATION.laboratory_test.v0]
contains
    CLUSTER a_a[openEHR-EHR-CLUSTER.laboratory_test_panel.v0]
```

Alternative AQL using Resultset Objects (does not work on EtherCis)
```
select
    a/uid/value as uid,
    a/composer/name as author,
    a/context/start_time/value as date_created,
    a_b as lab_test
from EHR e[ehr_id/value='{{ehrId}}']
contains COMPOSITION a
contains OBSERVATION a_b[openEHR-EHR-OBSERVATION.laboratory_test.v0]
```

#### Detail AQL /query:
To populate the detailed view / edit when a single record within the heading is selected.

```
As above
```

#### Sample Composition(FLAT JSON) for POST/PUT /composition:

To create or update a composition for a single item via the /composition Ehrscape API call.

```
{
    "ctx/language": "en",
    "ctx/territory": "GB",
    "ctx/composer_name": "Silvia Blake",
    "ctx/time": "2017-01-28T18:40:49.715+01:00",
    "ctx/id_namespace": "HOSPITAL-NS",
    "ctx/id_scheme": "HOSPITAL-NS",
    "ctx/health_care_facility|name": "Hospital",
    "ctx/health_care_facility|id": "9091",
    "laboratory_result_report/laboratory_test:0/requested_test|value": "Urea, electrolytes and creatinine measurement",
    "laboratory_result_report/laboratory_test:0/requested_test|code": "444164000",
    "laboratory_result_report/laboratory_test:0/requested_test|terminology": "SNOMED-CT",
    "laboratory_result_report/laboratory_test:0/specimen:0/specimen_type": "Plasma",
    "laboratory_result_report/laboratory_test:0/specimen:0/datetime_collected": "2017-01-28T18:40:49.715+01:00",
    "laboratory_result_report/laboratory_test:0/specimen:0/collection_method": "Venous sample",
    "laboratory_result_report/laboratory_test:0/specimen:0/processing/datetime_received": "2017-01-29T18:40:49.716+01:00",
    "laboratory_result_report/laboratory_test:0/test_status|code": "at0038",
    "laboratory_result_report/laboratory_test:0/test_status_timestamp": "2017-01-28T18:40:49.716+01:00",
    "laboratory_result_report/laboratory_test:0/clinical_information_provided": "History of angina",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_name|value": "Urea",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_name|code": "365755003",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_name|terminology": "SNOMED-CT",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/value2|magnitude": 4.3,
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/value2|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/lower|magnitude": "2.5",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/upper|magnitude": "6.6",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/comment": "raised",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_status|code": "at0009",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_name|value": "Creatinine",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_name|code": "70901006",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_name|terminology": "SNOMED-CT",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/value2|magnitude": 101.4,
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/value2|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/comment": "normal",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_status|code": "at0009",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/lower|magnitude": "80",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/upper|magnitude": "10",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_name|value": "Sodium",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_name|code": "365761000",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_name|terminology": "SNOMED-CT",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/value2|magnitude": 133,
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/value2|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/lower|magnitude": "133",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/upper|magnitude": "146",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/comment": "low",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_status|code": "at0009",
    "laboratory_result_report/laboratory_test:0/conclusion": "Not consistent with renal failure",
    "laboratory_result_report/laboratory_test:0/responsible_laboratory/name_of_organisation": "Royal Free",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number": "cbf3c55e-ea2e-4860-a5a5-508e8a962d3d",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number|issuer": "royalfree",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number|assigner": "royalfree",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number|type": "Lab_order",
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number": "66cac634-545b-445f-9098-5c651ff54056",
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number|issuer": "gp",
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number|assigner": "gp",
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number|type": "Lab_order",
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/ordering_provider/ordering_provider/given_name": "Ian",
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/ordering_provider/ordering_provider/family_name": "McNicoll",
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier": "361a30c1-a56e-4381-8ac6-9e52c6cf32bd",
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier|issuer": "GMC",
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier|assigner": "GMC",
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier|type": "GMC Number"
}
```

#### Sample Composition(FLAT JSON) for POST/PUT /composition with HL7v2 Markup
```
{
    "ctx/language": "en",
    "ctx/territory": "GB",
    "ctx/composer_name": "Silvia Blake",
    //MSH.7-TS.1
    "ctx/time": "2017-01-28T18:40:49.715+01:00",
    //HD.3
    "ctx/id_namespace": "HOSPITAL-NS",
    "ctx/id_scheme": "HOSPITAL-NS",
    //HD.1
    "ctx/health_care_facility|name": "Royal Free",
    //HD.2
    "ctx/health_care_facility|id": "9091",
    //OBR.4 - CE.1
    "laboratory_result_report/laboratory_test:0/requested_test|value": "Urea, electrolytes and creatinine measurement",
      //OBR.4 - CE.2
    "laboratory_result_report/laboratory_test:0/requested_test|code": "444164000",
    //OBR.4 - CE.2
    "laboratory_result_report/laboratory_test:0/requested_test|terminology": "SNOMED-CT",
    //OBR.15-SPS.1-CE.1
      "laboratory_result_report/laboratory_test:0/specimen:0/specimen_type": "Plasma",
    //OBR.7 - TS.1
    "laboratory_result_report/laboratory_test:0/specimen:0/datetime_collected": "2017-01-28T18:40:49.715+01:00",
    //OBR.15-SPS.4-CE.1
    "laboratory_result_report/laboratory_test:0/specimen:0/collection_method": "Venous sample",
    //OBR.14-TS.1
    "laboratory_result_report/laboratory_test:0/specimen:0/processing/datetime_received": "2017-01-29T18:40:49.716+01:00",
    //OBR-25 Mappings
    //OBR.25 = P
		//"healthlink_lab_report/laboratory_test:0/test_status|code": "at0037",
		//"healthlink_lab_report/laboratory_test:0/test_status|value": "Partial",

		//OBR.25 = F
		//"healthlink_lab_report/laboratory_test:0/test_status|code": "at0038",
		//"healthlink_lab_report/laboratory_test:0/test_status|value": "Final",

		//OBR.25 = C
		//"healthlink_lab_report/laboratory_test:0/test_status|code": "at0115",
		//"healthlink_lab_report/laboratory_test:0/test_status|value": "Corrected"

	//	OBR.25 = X
	//	"healthlink_lab_report/laboratory_test:0/test_status|code": "at0074",
	//	"healthlink_lab_report/laboratory_test:0/test_status|value": "Cancelled"
    "laboratory_result_report/laboratory_test:0/test_status|code": "at0038",
    "laboratory_result_report/laboratory_test:0/test_status_timestamp": "2017-01-28T18:40:49.716+01:00",

    "laboratory_result_report/laboratory_test:0/clinical_information_provided": "History of angina",

    //OBX.1 - CE.1
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_name|value": "Urea",

    //OBX.1 - CE.2
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_name|code": "365755003",

    //OBX.1 - CE.3
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_name|terminology": "SNOMED-CT",


    //OBX.5
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/value2|magnitude": 4.3,

    //OBX.6
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/value2|unit": "mmol/l",

    //OBX-7
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/lower|magnitude": "2.5",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/upper|magnitude": "6.6",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_value/_normal_range/lower|unit": "mmol/l",


    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/comment": "raised",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:0/result_status|code": "at0009",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_name|value": "Creatinine",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_name|code": "70901006",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_name|terminology": "SNOMED-CT",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/value2|magnitude": 101.4,
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/value2|unit": "mmol/l",
    //NTE.1 - NTE.3
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/comment": "normal",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_status|code": "at0009",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/lower|magnitude": "80",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/upper|magnitude": "10",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:1/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_name|value": "Sodium",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_name|code": "365761000",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_name|terminology": "SNOMED-CT",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/value2|magnitude": 133,
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/value2|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/lower|magnitude": "133",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/upper|magnitude": "146",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_value/_normal_range/lower|unit": "mmol/l",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/comment": "low",
    "laboratory_result_report/laboratory_test:0/laboratory_test_panel:0/laboratory_result:2/result_status|code": "at0009",
    "laboratory_result_report/laboratory_test:0/conclusion": "Not consistent with renal failure",
    "laboratory_result_report/laboratory_test:0/responsible_laboratory/name_of_organisation": "Royal Free",

    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number": "cbf3c55e-ea2e-4860-a5a5-508e8a962d3d",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number|issuer": "royalfree",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number|assigner": "royalfree",
    "laboratory_result_report/laboratory_test:0/test_request_details/placer_order_number|type": "Lab_order",
//OBR.3 - EI.1
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number": "66cac634-545b-445f-9098-5c651ff54056",
    //OBR.3 - EI.3
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number|issuer": "chem path",
    //OBR.3 - EI.1
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number|assigner": "chem path",
    //OBR.3 - EI.1
    "laboratory_result_report/laboratory_test:0/test_request_details/filler_order_number|type": "chem path",
// MSH.6-HD.1 - not sure why this is structured, unstructred name is possible too.
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/ordering_provider/ordering_provider/given_name": "Ian",
// MSH.6-HD.1
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/ordering_provider/ordering_provider/family_name": "McNicoll",
// MSH.6-HD.2
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier": "361a30c1-a56e-4381-8ac6-9e52c6cf32bd",
    // MSH.6-HD.3
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier|issuer": "GMC",
    // MSH.6-HD.3
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier|assigner": "GMC",
    // MSH.6-HD.3
    "laboratory_result_report/laboratory_test:0/test_request_details/requester/professional_identifier|type": "GMC Number"
}
```


#### Notes:

Commit not currently working in Ethercis.
