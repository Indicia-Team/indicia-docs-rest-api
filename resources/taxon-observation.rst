taxon-observation
-----------------

The attributes of a single wildlife record. 

The API is based on but not exactly the same as the NBN data exchange format field
specifications to define taxon observations, as described in the guide to the NBN data
exchange format Version 2.7, September 2014. Field names are always lowercased. The
RecordKey field is replaced by an id field to keep taxon-observations consistent with
other entities exposed by the API. In addition to the fields defined by the NBN exchange
format, a lasteditdate field is required.

.. todo::

  Consider case issues here - should fields be lowercased? T/F values are also 
  inconsistently cased throughout the spec.

Taxon observations contain the following properties. Properties marked with a * are 
mandatory though check the property description for rules relating to the specific field.

  * id* - The unique identifier of the observation
  * href* - link to the observation’s URI. This can be omitted if the API implementation
    does not support access to a single observation by ID.
  * srchref - link to the URI of the object in its originating location, if different to
    href.
  * datasetName - name of the dataset this record was sourced from.
  * taxonVersionKey* - the Taxon Version Key from the UKSI species database.
  * taxonName* - the taxon name used by the recorder.
  * zeroAbundance - set to T to indicate an absence record or F otherwise. The
    default if not provided is F.
  * count - integer value representing the count.
  * delete - set to T to indicate this record has been deleted.
  * sensitive - set to T to indicate a sensitive record or F otherwise. The
    default if not provided is F.
  * startDate* - the start of the range of dates that the record covers, which will be the
    same as the enddate field when a record occurred on a single date.
  * endDate* - the end of the range of dates that the record covers, which will be the same
    as the startdate field when a record occurred on a single date.
  * dateType* - see the NBN Gateway Exchange format
    (http://www.nbn.org.uk/Share-Data/Providing-Data/NBN-Data-Exchange-format.aspx) for a
    definition of how date types are defined.
  * siteKey - a unique ID for the site if available.
  * siteName - the name of the site provided with the record.
  * gridReference* - the grid reference notation for the record. Mandatory unless east 
    and north are provided. British National Grid or Irish Grid notation depending on
    projection.
  * east* - position of record in east/west direction. Mandatory unless gridreference is
    provided. Either a decimal longitude or easting.
  * north* - position of record in north/south direction. Mandatory unless gridreference 
    is provided. Either a decimal latitude or northing.
  * projection* - indiciates the projection used for gridreference, east and north fields.
    Can be:

      * OSGB
      * OSI
      * WGS84
      * OSGB36

  * precision* - the spatial precision of the georeference in metres. Typically the size of
    the grid square.
  * recorder* - the recorder name(s).
  * determiner - the name of the person providing the initial identification.
  * lastEditDate - returns the date and time time of last edit. 

An example taxon-observation object is:

.. code-block:: json

  {
    "id":"BRC100",
    "href":"http://example.com/rest/taxon-observations/BRC100",
    "srchref":"http://source-server-at-brc.com/rest/taxon-observations/BRC100",
    "datasetName":"iRecord::Mammals::Dorset Mammal Group",
    "taxonVersionKey":"NHMSYS0000530482",
    "taxonName":"Red Kite",
    "startDate":"2014-07-12",
    "endDate":"2014-07-12",
    "dateType":"D",
    "gridReference":"SU956436",
    "projection":"OSGB",
    "precision":"8",
    "recorder":"Joe Brown",
    "lastEditDate":"2014-09-12T13:24:11"
  }
