GET /taxon-observations
-----------------------

Retrieve a list of records as a JSON array.

By default the request returns 1 day of records if no end date is specified.

If there are no records, then an empty array should be returned.

Implementations of this API might choose to reject requests for date ranges wider than 1
week, but this restriction can be omitted where the API is being put to wider use.

Deleted records can be included in batches of updates. A deleted record will at the
minimum include the unique identifier for the record plus a flag “Deleted=t”.

Request fields
^^^^^^^^^^^^^^
Fields marked with a * are mandatory.

  * proj_id* - ID of the project whose records are being requested.
  * edited_date_from* - mandatory, retrieves records entered or edited since this date. 
    Format yyyy-mm-dd.
  * edited_date_to - format yyyy-mm-dd
  * page_size - number of records to return in the page.
  * page - index of the page to return, default 1.

Note that this date format confirms to ISO 8601.

Response status codes
^^^^^^^^^^^^^^^^^^^^^

  * 200 - Success
  * 400 - Bad request (Invalid parameters)
  * 401 - unauthorized
  
Response
^^^^^^^^

A successful request receives a list of projects in JSON format, using the :doc:`GET 
response template<index>` and the :doc:`taxon-observation resource 
format<../resources/taxon-observation>`.