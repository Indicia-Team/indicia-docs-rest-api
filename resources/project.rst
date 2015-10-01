project
-------

The metadata describing a set of records on the server which are being made available to a
client. A project might, for example, be the bird records from iRecord. For a simplicity
of implementation, each project is unique to the calling client (so clients cannot call
projects set up for other clients and there is no need for a many-many relationship). 

Projects contain the following fields (fields marked with a * are mandatory):

  * id* - the unique identifier of the project. This must be provided with requests for 
    taxon-observations and annotations from within this project.
  * href* - provides a link back to the resource API endpoint describing the individual 
    project.
  * Title* - project title.
  * Description* - a description of the project.

An example project object is:

.. code-block:: json

  {
    "id":"BTO12",
    "href":"http://www.bto.org/rest/projects/BTO12",
    "Title":"BTO Odonata",
    "Description":"Odonata records for verification on iRecord"
  }

