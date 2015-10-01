API Versioning
==============

The default version for all calls is the latest available API version on that system.
Requests for a specific API version can be made by inserting the API version name into the
URL segments, placing it before the resource name. For example::

  http://example.com/rest/v1.0/projects

is equivalent to::
 
  http://example.com/rest/projects
  
when the API is at version 1.0.

The API should normally be used without specifying the version and the option to use the
version is only recommended in specific circumstances, e.g. during development. This
approach ensures that resource URIs are effectively permalinks that will not change over
time. For more information on the reasoning here, see
http://stackoverflow.com/questions/389169/best-practices-for-api-versioning. 