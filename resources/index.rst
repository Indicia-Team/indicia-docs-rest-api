API resources
=============

The RESTful API defines a set of resources available at the following URLs and request
types. Since it is effectively a uni-directional read only specification, we are using GET
for all requests. Resource names are lower case and use hyphens as a word separator, to
meet with current best-practice for URI naming.

Because a server might not want to expose all its records to a client, the API includes
the notion of projects that a client can access. A project is effectively a filter on the
underlying records; the mechanism of how this filter may be defined internally is up to
each system. For example, in Indicia a project would use the reporting saved filters
system to allow a flexible definition of the list of records available.

Resource object definitions
---------------------------

The API returns resource objects (in JSON format), either individually, or in lists
depending on the API call made. The following list of object types are defined for the API.

.. toctree::
   :maxdepth: 2

  projects
  taxon-observations
  annotations