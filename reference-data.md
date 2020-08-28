# Reference Data
This page is part of my "[Know Data](https://bit.ly/know-data)" collection. If you're interested in data, I suggest you have a look
at the resources I've indexed there.


## Definition of Reference Data
According to Wikipedia, [Reference Data](https://en.wikipedia.org/wiki/Reference_data) is "used to classify or categorize other data," 
and "... is sometimes referred to as 'controlled vocabulary' or '**lookup data**'". This is also how I use this term, though as any data 
person will tell you, Entity data can also be Reference Data depending on how you use it and if you own it. Reference data can also
be described as a **slowly changing dimension,** in the context of a data warehouse.

There are three types of reference data that I am concerned with in this page:

* Code Tables
* Translation Tables
* Slowly Changing Dimensions

As a rule, I prefer the more expansive features of a **[Slowly Changing Dimension](https://en.wikipedia.org/wiki/Slowly_changing_dimension)**
over the more basic "Code Table" or "Enumerated List". Code Tables and slowly changing dimensions (SCDs) are very similar, but are not the same;
the distinction is usually found within the physical data model, specific to storage of the data itself. An SCD can be published, and limited
to active values, which looks like a code table, but a code table is not an SCD if it doesn't have version and date information.

Many of the code tables referenced in the sources below are useful, but limited because do not have a temporal dimension that is usually 
critical for advanced analytics or longitudinal study; in simpler terms, they are only code tables. Using ISO country codes as an example, 
the publicly available lists provide codes, but do not have any associated dates, so you have no way of
knowing when a country has changed its name. Also, because there is no linkage, you have no way to connect 
"[Rhodesia](https://en.wikipedia.org/wiki/Rhodesia)" to "[Zimbabwe](https://en.wikipedia.org/wiki/Zimbabwe)". This problem can be solved 
using a slowly changing dimension, which is more suitable for research, historical/longitudinal analysis, and other advanced analytical 
uses.

Translation tables, sometimes called "crosswalk tables", are especially useful to translate semantically
similar lists from one to the other. A common translation table is a zip code/state table, where you can see all of the zip codes in a state, 
which allows you to translate from one geographic model to another. A more complex translation table example is ethnicity codes by different
systems. In some cases, there will be a direct match, but in others a policy decision will need to be made to map non-matching and semantically
similar codes. Ethnicity is an example of reference data that is very contextual, sometimes political, and often subject to the needs of
a system. It is usually easier to translate a small list into a larger list, than to go the other way.


Where possible, I prefer to catalog slowly changing dimensions rather than code tables, but it's important to have at least the code table
in many cases, so I include them here. I am always on the lookout for translation tables, and will catalog those here too.

## Reference Data Attributes
These attributes are defined for general use purposes, tailored to my own needs, but generally include the attributes you would
find in a slowly changing dimension.

|Attribute|Definition|Required (y/n)|Example|
|:--------|:---------|:-------------|:------|
|Code|A short, human readable code that is unique within the list of "active" codes.|Y| - |
|Label|Expanded Description of the code's meaning|Y| - |
|Antecedent|(Replaces) Used when this code replaces an older code, the is an array of code(s) that are no longer used, or for which this code should be used as of the effective date.|N| - |
|Descendent|(Replaced By) If a code is replaced by a different code, then versioning is not applicable and the code becomes inactive or deprecated. The new code is put here. |N| - |
|Effective Date|The date/time when this code starts to be used. Especially important for versioning or updating descriptions or related measurements, or the create date/time of the code for the first instance|Y| - |
|Effective End Date|The date/time when this code no longer applies or can be used.|N| - |

A slowly changing dimension can also include variable data, that is used for a time, but is eventually replaced. An example 
of this is annual "cost of living adjustment" (COLA), which is used to determine the amount of increase in income set by a
regulation or policy. The amount may change from annually, or it could remain the same for short or long periods of time.

Be careful when including variables in your reference dataset. You do not want your slowly changing dimension to become an operational or transactional
table, which would reduce the stability of your reference data overall. Try to limit related variables to those that are likely to have limited changes
over time. The **MSSA** dataset below is an example of a reference dataset that includes geographic linkage that changes very rarely.

It is also possible that there can be more than one code within a dataset. An example of this scenario is the ISO Country Codes, which have two-character,
three-character, and three-number codes for use under different circumstances. In these cases, all of the codes would need to be unique within the column
of data, for active records (specific to a specific point or span of time).

# Reference Data Resources
## Code Tables and Lists of Values

* Government of New Zealand
  * [Ministry of Health — Code Tables](https://www.health.govt.nz/nz-health-statistics/data-references/code-tables)
* State of California
  * [Data San Francisco — Reference Index](https://datasf.gitbook.io/draft-publishing-standards/appendix/reference-index)
* International Standards Organization
  * Country Codes — [1](https://www.iso.org/iso-3166-country-codes.html), [2](https://www.iso.org/obp/ui/#search0), [wikipedia](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)
  
## Slowly Changing Dimensions 

* State of California
  * [Medical Service Study Area (MSSA)](https://data.chhs.ca.gov/dataset/mssa-detail)


## Translation Tables
nothing yet.
