taxon-observation
-----------------

The attributes of a single wildlife record. 

Taxon observations contain the following fields:

  * id - The unique identifier of the observation
  * href - link to the observation’s URI. This can be omitted if the API implementation
    does not support access to a single observation by ID.
  * srchref - link to the URI of the object in its originating location, if different to
    href.
  * DatasetName - name of the dataset this record was sourced from.
  * TaxonVersionKey - the Taxon Version Key from the UKSI species database.
  * TaxonName - the taxon name used by the recorder.
  * ZeroAbundance - optional, set to T to indicate an absence record or F otherwise. The
    default if not provided is F.
  * Count - optional. Integer value representing the count.
  * Delete - optional, set to T to indicate this record has been deleted
  * sensitive - optional, set to T to indicate a sensitive record or F otherwise. The
    default if not provided is F.
  * StartDate - the start of the range of dates that the record covers, which will be the
    same as the enddate field when a record occurred on a single date.
  * EndDate - the end of the range of dates that the record covers, which will be the same
    as the startdate field when a record occurred on a single date.
  * DateType - see the NBN Gateway Exchange format
    (http://www.nbn.org.uk/Share-Data/Providing-Data/NBN-Data-Exchange-format.aspx) for a
    definition of how date types are defined.
  * SiteKey - optional, a unique ID for the site if available.
  * SiteName - optional, the name of the site provided with the record.
  * GridReference - the grid reference notation for the record. Mandatory unless east and
    north are provided. British National Grid or Irish Grid notation depending on
    projection.
  * East - position of record in east/west direction. Mandatory unless gridreference is
    provided. Either a decimal longitude or easting.
  * North - position of record in north/south direction. Mandatory unless gridreference is
    provided. Either a decimal latitude or northing.
  * Projection - indiciates the projection used for gridreference, east and north fields.
    Can be:

      * OSGB
      * OSI
      * WGS84
      * OSGB36

  * Precision - the spatial precision of the georeference in metres. Typically the size of
    the grid square.
  * Recorder - the recorder name(s).
  * Determiner - optional, the name of the person providing the initial identification.
  * lasteditdate - mandatory, returns the date and time time of last edit. 

An example taxon-observation object is:

.. code-block:: json

  {
    "id":"BRC100",
    "href":"http://example.com/rest/taxon-observations/BRC100",
    "srchref":"http://source-server-at-brc.com/rest/taxon-observations/BRC100",
    "DatasetName":"iRecord::Mammals::Dorset Mammal Group",
    "TaxonVersionKey":"NHMSYS0000530482",
    "TaxonName":"Red Kite",
    "StartDate":"2014-07-12",
    "EndDate":"2014-07-12",
    "DateType":"D",
    "GridReference":"SU956436",
    "Projection":"OSGB",
    "Precision":"8",
    "Recorder":"Joe Brown",
    "lasteditdate":"2014-09-12T13:24:11"
  }