Specification
=============

The PHH format is a derivative of the `Tom's Obvious, Minimal Language (TOML) format <https://toml.io/>`_. This design allows PHH files to take advantage of TOML format's type system and be human-readable and writable while maintaining easy parsability by software systems. This differs from historical game file formats like `PGN <_static/PGN_Reference.txt>`_ or `SGF <https://www.red-bean.com/sgf/>`_ which use in-house formatting.

The PHH format puts restrictions on the naming and types of the key/values, with which the poker games are described. These definitions, named "fields", fall under two classifications. The first involves state construction and progression and must be specified. The second describes various miscellaneous information about the game and may be omitted by the annotator. The full fields are described below.

============================================================== ========================== ================================== ========
Field                                                          Name                       TOML Native Type                   Required
============================================================== ========================== ================================== ========
Variant code                                                   ``variant``                String                             yes
Antes                                                          ``antes``                  Array of integers or floats        yes
Blinds/Straddles                                               ``blinds_or_straddles``    Array of integers or floats        yes
Bring-in                                                       ``bring_in``               Integer or float                   yes
Small bet                                                      ``small_bet``              Integer or float                   yes
Big bet                                                        ``big_bet``                Integer or float                   yes
Min bet                                                        ``min_bet``                Integer or float                   yes
Starting stacks                                                ``starting_stacks``        Array of integers, floats, or null yes
Actions                                                        ``actions``                Array of strings                   yes
Annotator full name or mononym                                 ``author``                 String                             no
Event name                                                     ``event``                  String                             no
Event or organizer URL                                         ``url``                    String                             no
Venue                                                          ``venue``                  String                             no
Venue street-level address                                     ``address``                String                             no
Venue city                                                     ``city``                   String                             no
Venue region, state, or province                               ``region``                 String                             no
Venue postal code                                              ``postal_code``            String                             no
Venue country                                                  ``country``                String                             no
Timestamp at the start of the hand                             ``time``                   Local time                         no
`IANA time zone <https://www.iana.org/time-zones>`_            ``time_zone``              String                             no
Time zone abbreviation                                         ``time_zone_abbreviation`` String                             no
Event day                                                      ``day``                    Integer                            no
Event month                                                    ``month``                  Integer                            no
Event year                                                     ``year``                   Integer                            no
Hand name or number                                            ``hand``                   String or integer                  no
Tournament level                                               ``level``                  Integer                            no
Players' seat numbers                                          ``seats``                  Array of integers                  no
The number of seats                                            ``seat_count``             Integer                            no
Table name or number                                           ``table``                  String or integer                  no
Player full names or mononyms                                  ``players``                Array of strings                   no
Final stacks                                                   ``finishing_stacks``       Array of integers or floats        no
Winnings                                                       ``winnings``               Array of integers or floats        no
`ISO 4127 <https://www.iso.org/standard/64758.html>`_ currency ``currency``               String                             no
Currency symbol                                                ``currency_symbol``        String                             no
Ante uniformity                                                ``ante_trimming_status``   Boolean                            no
Allocated time per action                                      ``time_limit``             Integer or float                   no
Time banks at the beginning of the hand                        ``time_banks``             Array of integers or floats        no
============================================================== ========================== ================================== ========

Objective
---------

An ideal representation of poker hands should not only be concise but also easily readable and writable by human readers. It should also support only describing the bare minimum information necessary to comprehensively describe a hand while facilitating options to give rich details for various use cases beyond simple action tracking. For convenience in parser implementations, the formatting must also be simply structured in a consistent manner. In addition, the format must be powerful enough to describe a wide variety of poker games played in formal settings. Such selections should cover games played in reputable poker tournaments around the world while the inclusion of various eccentric or esoteric variants is not as necessary.

Error Handling
--------------

In the implementation of the PHH parser, the program should report an error when any violation of the specification is encountered. The parser may stop parsing the file, ignore the problematic field or action, or proceed as normal.

Position
--------

The fields that have a value of type array where each element corresponds to a particular player must have their elements ordered identically to the ordering of the players and have lengths equal to the number of players. The ordering of the players is table agnostic, that is, it is purely based on position.

The first player in the PHH format is typically the very first person being dealt the hole card by the dealer while the last player in the PHH format is typically the person being dealt the last hole card. This is assuming a proper dealing order is followed. In general, the ordering of the players must represent a clockwise order.

In typical button games such as no-limit Texas hold 'em or pot-limit Omaha hold 'em, the first player must be in the small blind while the last player must be in position (i.e. has the button). In non-button games like stud, there is no strict notion of position. In such games, the first player should be the one in the dealer's immediate left while the last player should be in the dealer's immediate right.

Rules
-----

As poker is a game with a diverse set of rules that often differ based on regions or events, it is impossible to point to anything as an authoritative documentation of poker rules that must be followed both by the annotator and the parser. The parser implementation should be designed to handle actions that may be potential transgressions in certain poker rule sets, either silently or with a warning.

While annotating the fields, especially the "actions" field, the author should follow the specific set of rules followed by the game being annotated. Where applicable or possible, the author is encouraged to conform to the latest WSOP `Live Action <_static/2023-WSOP-Live-Action-Rules.pdf>`_ and `Tournament Rules <_static/2023-WSOP-Tournament-Rules.pdf>`_ of which the most recently released versions as of the writing of this page are for the 2023 WSOP. If there is any contradiction between the two documents, the tournament rules take precedence, as they impose stricter guidelines on poker playing. When there is an ambiguity in both documents, it is to be considered as an undefined behavior. In such a case, the annotator should adhere to a historically informed custom of poker playing.
