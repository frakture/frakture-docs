# Cleaning Operations

Frakture provides various cleaning operations that will unify the representation of your data and provide you with data that is easier to use.
A list of methods and their descriptions can be found below:

- *name*: Apply uniform capitalization to names (fixing things such as "JOHN" and "john" to "John"), applying to both given_name and family_name
- *email*: Lowercase and remove invalid characters from the e-mail addresses in your 
- *country*: Determine the country code for the defined country (United States of America becomes "US")
- *language*: This will determine the long form name of a language based on short hands (transforming "FR" to "French"
- *region*: Clean up the region (state/province/etc) associated with the record. This applies uniform capitalization, and for a few countries it will standardize to their proper region names
- *city*: Applies uniform capitalization to the city name
- *address*:
- *postalCode*: Ensures postal code is digits, and follows the postal code format of the country (if present)
- *genderDetect*: Uses the given name to infer the gender of a record (strictly for reporting purposes)
- *phoneIntl*: Formats the phone number for the record using international standards (country code, etc)
- *geographicalRegion*: Appends the geographical region based on country
