GET /projects
-------------

Retrieves a list of projects available to the client.

The server side needs a mechanism for associating records to "projects" and for
associating projects to the accessing client's authorisation. So, iRecord might be able to
access BirdTrack Odonata records but not bird records, therefore BirdTrack will need to be
able to identify the Odonata records with a unique project ID and to recognise that
iRecord can access this project.

.. note:: 

  In iRecord, it is likely that projects will be managed using the existing filters
  system, giving great flexibility over the records exposed. This is a detail of
  implementation which does not affect the transfer specification.
  
Request fields
^^^^^^^^^^^^^^

  * page_size - number of records to return in the page.
  * page - index of the page to return, default 1.

Response status codes
^^^^^^^^^^^^^^^^^^^^^

  200 - Success
  401 - unauthorized

Response
^^^^^^^^

A successful request receives a list of projects in JSON format, using the :doc:`GET 
response template<index>` and the :doc:`project resource format<../resources/project>`.