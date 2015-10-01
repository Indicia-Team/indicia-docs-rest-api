annotation
----------

The definition of an annotation against a taxon-observation. An annotation is an extra piece of information added after the initial record creation event and may describe a user comment, verification event or redetermination of the record. 

Annotations contain the following fields (fields marked with a * are mandatory):

  * id* - The unique identifier of the annotation
  * href* - link to the annotation’s URI. This can be omitted if the API implementation
    does not support access to a single annotation by ID.
  * TaxonObservation* - contains a child-object, itself containing the id and href for the
    taxon observation being annotated
  * TaxonVersionKey* - the unique identifier of the taxon concept that this annotation was
    made against. This might differ from the original or current taxon concept associated
    with the record. This allows annotations to maintain an audit trail of the changing
    opinions of a record’s identification.
  * Comment - free text
  * StatusCode1 - either A (accepted), U (unconfirmed) or N (not accepted) to
    indicate a status if this annotation is setting the verification state of the record.
  * StatusCode2 - provides additional detail regarding the status code. For
    accepted records, can be 1 (correct) or 2 (considered correct). For unconfirmed
    records, can be 3 (plausible) or 4 (not reviewed). For not accepted records, can be 5
    (unable to verify) or 6 (incorrect).
  * EmailAddress - optionally contains the email address of the person creating the
    annotation. It is recommended that when a user takes an action that results in an
    annotation (such as commenting on or verifying a record), then the system should give
    the user an option to opt in to providing their email address. If provided, then on
    other systems receiving the annotation, the email address must only be made available
    to the recipient of the notification. This allows an external communication thread to
    start to discuss the record. Note that email addresses should not be provided if the
    user creating the annotation has not opted in.
  * Question - t or f to indicate true or false. If true, then this annotation contains a
    question that needs answering.
  * AuthorName* - name of the comment author.
  * DateTime* - ISO 8601 date format for the timestamp of the annotation.

An example annotation object is:

.. code-block:: json

  {
    "id":"BRC452",
    "href":"http://indicia.org.uk/rest/annotations/BRC452",
    "TaxonObservation":{
      "id":"BRC251",
      "href":"http://indicia.org.uk/rest/taxon-observations/BRC251"
    },
    "TaxonVersionKey":"NBNSYS0012345678", 
    "Comment":"Some text commenting on the record",
    "StatusCode1":"A",
    "StatusCode2":"1",
    "EmailAddress":"example@example.com",
    "Question":"f",
    "AuthorName":"John Smith",
    "DateTime":"2014-02-01T09:00:22+05:00" 
  }
