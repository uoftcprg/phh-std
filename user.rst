User-defined Fields
===================

Depending on the use case, the required and optional fields may not be sufficient to capture certain desired levels of details. The specification allows annotators to define custom fields with a single underscore prefix in the field names. Parser implementations should simply ignore unknown fields and may issue a warning when such a field is encountered. This is also in part to ensure that the parser is compatible with PHH files conforming to the future version of the specification that may introduce new fields.

Example user-defined fields in PHH format are shown below.

.. code-block:: toml

   _sponsors = ["", "GGPoker", ""]
   _nationalities = [
     "Peru", "Italy", "Japan",
   ]
