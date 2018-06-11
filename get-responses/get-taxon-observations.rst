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

Fields marked with a * are mandatory so must be included in the request.

  * proj_id* - ID of the project whose records are being requested.
  * edited_date_from* - format yyyy-mm-dd or ISO 8601 yyyy-mm-ddThh:mm:ss. Limits to
    records created or updated on or after this date.
  * edited_date_to - format yyyy-mm-dd or ISO 8601 yyyy-mm-ddThh:mm:ss. Limits to
    records created or updated on or before this date.
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

A successful request receives a list of taxon-observations in JSON format, using the
:doc:`GET response template<index>` and the :doc:`taxon-observation resource
format<../resources/taxon-observation>`.

.. note::

  The server is responsible for ensuring that the default sort order of any taxon
  observations returned is stable and not affected by edits happening whilst the client
  pages through the dataset. For example, a sort by creation timestamp or record ID (if
  sequentially generated) would be appropriate.