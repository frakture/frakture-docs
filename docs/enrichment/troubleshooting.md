# Data Troubleshooting


| Symptom         	| Where to look | Tables | Fields |
| ------------- |:-------------:| -----:| -----:|
| Acquisition or lifetime value isn't correct  | These are calculated from acquisition_cost in source_code_ | Facebook | End of Q1 |


Sample query for tracking down origin source people
select origin_source_code,count(*) from person_metadata where origin_source_code in (select (source_code) from source_code_dictionary_override where acquisition_source='Dems.com') group by 1;


* Constituent Groups
