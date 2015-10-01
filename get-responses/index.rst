GET responses
=============

Responses to HTTP GET requests are either a single object (one of _project_,
_taxon-observation_ or _annotation_ as described above) or a list/array of objects. When
returning a list of objects, the each individual response includes a single page of
objects and it may be necessary to make multiple calls to page through the dataset.
Therefore the structure  also includes metadata to simple support pagination by providing
links to the current, next and previous page. The following template is used:

.. code-block:: json

  {
    “data”:[
      { project, taxon-observation or annotation object },
      { project, taxon-observation or annotation object },
      { project, taxon-observation or annotation object },
      etc
    ],
    “paging”:{
      “self”:”uri for current page in set”,
      “previous”:”uri for previous page in set”,
      “next”:”uri for next page in set”,
    }
  }

The next and previous page links are only provided when there is a next or previous page 
available in the dataset.

Resource API end-points
-----------------------

The following list of end-points are exposed by an implementation of the REST API:

.. toctree::
   :maxdepth: 1

   get-projects
   get-taxon-observations
   get-annotations