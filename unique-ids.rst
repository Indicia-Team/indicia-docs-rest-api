Unique record identifiers
=========================

Each participating system will be given a unique user ID - a code that unqiuely identifies
the system to other participants. The system identifiers can be mutually agreed since a
relatively small number of participating systems will exist, for example "BRC" or "BTO"
would be suitable candidates.

Presumably each participating system will use a standard relational database model with a
primary key for all database tables. As this primary key is likely to be a locally
generated sequential integer, the IDs will not be unique across all databases.

Therefore each participating system will need to prefix it’s user_id to its record IDs to
make a globally unique ID, so record ID 100 on iRecord might be expressed as BRC100 for
example. Limiting these to 3 alphabetical characters makes parsing of IDs easier. The
resultant record identifiers only need to be unique within each resource type and not
globally across all resource types.