Field formats
=============

Dates in requests and responses are formatted to ISO 8601. The following possibilities are
accepted:

============= =========================================================================
Format        Notes
============= =========================================================================
Date          ``yyyy-mm-dd``, e.g. 2014-12-25
Date and time   * ``yyyy-mm-ddThh:mm:ss``, e.g. 2014-12-25T16:25:27 (without timestamp)
                * ``yyyy-mm-ddThh mm:ss+hh:mm``, e.g. 2014-12-25T16:25:27+02:00 (with 
                  timestamp)
============= =========================================================================