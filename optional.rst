Optional Fields
===============

The optional fields may be left unspecified by the annotator. The complete list of optional fields and their TOML native types are tabulated below.

============================================================== ======================== ===========================
Field                                                          Name                     TOML Native Type
============================================================== ======================== ===========================
Annotator full name or mononym                                 ``author``               String
Event name                                                     ``event``                String
Event or organizer URL                                         ``url``                  String
Venue street-level address                                     ``address``              String
Venue city                                                     ``city``                 String
Venue region, state, or province                               ``region``               String
Venue postal code                                              ``postal_code``          String
Venue country                                                  ``country``              String
Timestamp at the start of the hand                             ``time``                 Local time
`IANA time zone <https://www.iana.org/time-zones>`_            ``time_zone``            String
Event day                                                      ``day``                  Integer
Event month                                                    ``month``                Integer
Event year                                                     ``year``                 Integer
Hand number                                                    ``hand``                 Integer
Tournament level                                               ``level``                Integer
Players' seat numbers                                          ``seats``                Array of integers
The number of seats                                            ``seat_count``           Integer
Table number                                                   ``table``                Integer
Player full names or mononyms                                  ``players``              Array of strings
Final stacks                                                   ``finishing_stacks``     Array of integers or floats
`ISO 4127 <https://www.iso.org/standard/64758.html>`_ currency ``currency``             String
Ante uniformity                                                ``ante_trimming_status`` Boolean
Allocated time per action                                      ``time_limit``           Integer or float
Time banks at the beginning of the hand                        ``time_banks``           Array of integers or floats
============================================================== ======================== ===========================

Author
^^^^^^

The ``author`` field describes the annotator and is of TOML native string type. The value should represent a properly capitalized full name of the annotator as in ``"First_name[ Middle_name(s)...] Last_name"`` or a mononym ``"Name"`` depending on their preferences.

Venue-Related Fields
--------------------

The following fields describe the venue in which the hand was played.

Event
^^^^^

The ``event`` field represents the full name of the event which should be in English and is of type: string.

URL
^^^

The ``url`` field contains a string URL relevant to the event. This field is particularly important for online poker hands where the venue might not be a physical location. Still, the annotator may choose to specify a relevant URL to the organizer's website or tournament website for physical poker hands, as well. The link should be prefixed with substrings like ``http://`` or ``https://`` to denote the internet communication protocol.

Address
^^^^^^^

The ``address`` field contains a string value that may or may not include the street name, street number, room number, et cetera. The annotator should use English wherever possible.

City
^^^^

The ``city`` field contains the information about the city the hand was played in. The annotator should use full English names for the cities.

Region
^^^^^^

The ``region`` field contains the information about the city the hand was played in. Similarly to the cities, the annotator should use full English names for the regions.

Postal Code
^^^^^^^^^^^

The ``postal_code`` field contains the postal code of the location of the hand.

Country
^^^^^^^

The ``country`` field contains the name of the country of the hand location. Again, the annotator should use full English names for the countries.

Time
^^^^

The ``time`` field should contain the approximate time the hand began as a TOML native local time without the timezone information.

If the ``time_zone`` field is defined, the time is assumed to be of that time zone. Otherwise, if every one of the following three fields -- ``city,`` ``region,`` and ``country`` -- are defined, it is assumed that the time is in the local time zone of the location of the hand. If the two previous conditions are not satisfied, the time is assumed to be in Coordinated Universal Time (UTC).

Time Zone
^^^^^^^^^

The ``time_zone`` field contains a value of type string and must represent an IANA time zone in the latest version of the `IANA time zone <https://www.iana.org/time-zones>`_ database available like ``America/Toronto``.

Day
^^^

The ``day`` field should contain the day the hand took place in, and is of the integer type.

Month
^^^^^

The ``month`` field should contain the month the hand took place in, and has an integral value where 1 represents January, 2 represents February, and so on.

Year
^^^^

The ``year`` field should contain the year the hand took place in, and must be an integer.

Counter-Related Fields
----------------------

Hand
^^^^

The ``hand`` field denotes the hand number which should be an integer. Typically, these count from ``1``.

Level
^^^^^

The ``level`` field denotes the blind or ante level, which is relevant in a poker tournament. This field must contain an integer value. Typically, these count from ``1``.

Seating-Related Fields
----------------------

Seats
^^^^^

The ``seats`` field denotes the seat numbers of the players. Typically, the seat numbers are counted from ``1``. The value of this field must be an array of integers, of length N where N is the number of players.

Number of Seats
^^^^^^^^^^^^^^^

The ``seat_count`` field denotes the number of seats and must have an integer value. Note that it is possible for there to be more seats than the players.

Table
^^^^^

The ``table`` field denotes the table number the hand is played in, as an integer value. Typically, these are counted from ``1``.

Miscellaneous Fields
--------------------

Players
^^^^^^^

The ``players`` field contains player names as an array of strings. The names should be written as a full name (``"First_name[ Middle_name(s)...] Last_name"``) or as a mononym (``"Name"``) depending on which is used or preferable. If the name of the player is unavailable perhaps due to anonymity, an empty string should be used.

Finishing Stacks
^^^^^^^^^^^^^^^^

The ``finishing_stacks`` field denotes the final stacks as an array of non-negative integers or floats. It may also be specified for a non-terminal hand history file, which can be interpreted as the stack values after all the action notations are applied.

The description of finishing stacks is helpful as the parser may not be aware of the granularity of the currency the chips are in or the rake applied in the end. For example, dollars can be broken down to cents whereas Japanese Yen must be of an integral value. On top of this, in a physical setting where chips are used, depending on the denominations, odd chip situations may arise where the player out of position is given the extra odd chip that cannot be broken further. It is, of course, infeasible to describe all the different chip values each player has in a poker hand history format. These inaccuracies are inherent drawbacks of using purely numerical representations to describe the stack values. It is worth noting that the inconsistencies caused by such circumstances only lead to extremely minor ambiguities in the final stack sizes that should not significantly impact the expected value calculations.

Currency
^^^^^^^^

The ``currency`` field denotes what currency the chips are in. The value must be of string and be one of three letter currency values in the `ISO 4127 <https://www.iso.org/standard/64758.html>`_ standard.

Ante Trimming Status
^^^^^^^^^^^^^^^^^^^^

The ``ante_trimming_status`` denotes how to handle the special cases where a player or players are so short-stacked that they cannot even pay the full ante as a Boolean value that defaults to ``false``. If ``true,`` the player can only win depending on how much the player contributed. Otherwise, the player can win all the antes even if they did not pay the full ante. This field was introduced due to the ambiguities in the 2023 WSOP `Live Action <_static/2023-WSOP-Live-Action-Rules.pdf>`_ and `Tournament Rules <_static/2023-WSOP-Tournament-Rules.pdf>`_. Note that, in certain ante configurations such as big blind antes, unequal contribution in the antes is expected, and therefore this value should be kept as ``false`` for non-uniform antes. In the vast majority of real-life poker hands, the players can at least pay the full antes. Therefore, this field is only relevant in extremely rare circumstances.

Time-Control Fields
-------------------

Time Limit
^^^^^^^^^^

The ``time_limit`` represents the shot clock time and is of type: integer or float. It represents the time the user has to make a decision at every turn. If there is none, the annotator can omit this field or set it as ``inf`` for infinity.

Time Banks
^^^^^^^^^^

The ``time_banks`` field denotes the time banks of each player at the beginning of the hand, as an array of integers or floats of length equal to the number of players. Just like in stack values, representing time banks as a simple numerical value loses the detail of the granularity of the time cards a player may have. Still, integral values are used thanks to their simplicity and consistency.
