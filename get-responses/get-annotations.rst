GET /annotations
----------------

Retrieve a list of annotations as a JSON array.

Use query parameters in the URL to filter – e.g. edited_date_from, edited_date_to to
define the date range for edits to include. If there are no results then an empty array is
returned.

Request fields
^^^^^^^^^^^^^^

Fields marked with a * are mandatory.

  * proj_id* - the ID of the project whose annotations are being requested.
  * edited_date_from* - format yyyy-mm-dd or ISO 8601 yyyy-mm-ddThh:mm:ss. Limits to 
    records created or updated on or after this date.
  * edited_date_to - format yyyy-mm-dd or ISO 8601 yyyy-mm-ddThh:mm:ss. Limits to 
    records created or updated on or before this date.
  * page_size - number of records to return in the page.
  * page - index of the page to return, default 1.

Note that the 2 date filter fields relate to the edit date of the annotation record itself
and are independent of the taxon-observation’s edit date.

Response status codes
^^^^^^^^^^^^^^^^^^^^^

  * 200 - Success
  * 400 - Bad request (Invalid parameters)
  * 401 - unauthorized
  
Response
^^^^^^^^

A successful request receives a list of annotations in JSON format, using the :doc:`GET 
response template<index>` and the :doc:`annotation resource 
format<../resources/annotation>`.