REST API Introduction
=====================

This document describes a RESTful API implemented in Indicia and BirdTrack allowing 
the sharing of records between systems. It can be implemented within other online 
recording systems wishing to participate in record sharing.

.. todo::

  Appropriate reflection of BSBI and BTO as partners in this development.

BirdTrack and Indicia both collect records from a wide range of taxonomic groups. Although
BirdTrack is in its nature primarily a system for recording birds, it has been extended
to allow recording of other taxonomic groups such as Odonata, which are frequently 
included on lists produced by bird recorders. However, the expert verifiers who are 
engaged with the BTO BirdTrack system do not have the expertise to verify these data and
furthermore, these records would be of great interest to recording schemes such as the 
British Dragonfly Society who are using Indicia and iRecord. Similarly, iRecord is used by
recorders to enter records from a wide range of taxonomic groups including birds. However
as many bird expert verifiers are already engaged with BirdTrack it would not make sense
to encourage them to use iRecord, especially given the fact that the majority of expert 
verifiers give their time voluntarily. Therefore a mechanism for synchronising records
from one online recording system to another and to synchronise verification decisions back
again is required.

.. note::

  The RESTful API described here provides the part of the mechanism which exposes records
  to outside systems; it does not define how those systems should go about pulling the 
  records from another system's API into their database.

In general, the master copy of any record remains in the source system, but other systems
will be able to annotate records in the context of verification messages and outcomes.
At the minimum, implementations of the REST API provide the following: 

  * A list of sets of records which are available to the other participating system 
    (projects). 
  * A list of records entered onto the system since a given date for each project so that
    they can be synchronised into other systems. 
  * A list of annotations of records as a result of expert verification. This allows 
    verification outcomes to be exported back to the source of the record. Annotations can
    be added to a record either by the system performing NBN Record Cleaner style 
    automated checks, by user comments, or by expert verifiers. 
    
Synchronisation requires that the API is implemented by all participating systems. The 
following steps describe an example configuration for synchronisation between iRecord and
BirdTrack: 

  * BirdTrack declares a project created called “BirdTrack Odonata” which filters 
    BirdTrack records to only the dragonfly and damselfy records. 
  * BirdTrack is configured to allow iRecord to access it’s API and to allow iRecord
    to access the BirdTrack Odonata project.
  * iRecord declares a project created called “iRecord Birds” which filters iRecord 
    records to only the bird records. 
  * iRecord is configured to allow BirdTrack to access it’s API and to allow 
    BirdTrack to access the iRecord Birds project. 
  * A process is written as part of the BirdTrack system to run periodically
    (e.g. nightly). This process calls the iRecord RESTful API to retrieve entered or
    changed records in the iRecord Birds project since the last time the process was run.
    The records are imported into BirdTrack. 
  * A process is written as part of the iRecord system to run periodically (nightly?).
		This process calls the BirdTrack RESTful API to retrieve entered or changed records in
		the BirdTrack Odonata project since the last time the process was run. The records are
		imported into iRecord.
  * The BirdTrack Odonata records are made available to expert verifiers on iRecord. 
    Verification outcomes are stored in the iRecord database as annotations in the 
    ``occurrence_comments`` table.
  * The iRecord Birds records is made available to expert verifiers on BirdTrack. 
    Verification outcomes are stored in the BirdTrack database as annotations.
  * The periodic process on BirdTrack requests any verification responses for the
    BirdTrack Odonata project from the annotations on iRecord and pulls them back into
    BirdTrack. BirdTrack then notifies recorders as it sees fit.
  * The periodic process on iRecord will request any verification responses for the
    iRecord Birds project from the annotations on BirdTrack and pulls them back into 
    iRecord.
  * iRecord then notifies recorders as it sees fit.

The API receives requests via URLs and returns JSON format responses. Although other 
formats (NBN exchange, CSV, XML etc) could be considered, the existing NBN REST API also 
returns JSON so this will limit the number of technologies users of these APIs need to 
learn.