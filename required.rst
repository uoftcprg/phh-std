Required Fields
===============

The required fields, tabulated below along with their native TOML types, represent a handful of fields that the annotator must define to digitalize a poker hand and therefore form a valid PHH file. The required fields are either used during the initial state construction or the subsequent state progression.

================ ======================= ==================================
Field            Name                    TOML Native Type
================ ======================= ==================================
Variant code     ``variant``             String
Antes            ``antes``               Array of integers or floats
Blinds/Straddles ``blinds_or_straddles`` Array of integers or floats
Bring-in         ``bring_in``            Integer or float
Small bet        ``small_bet``           Integer or float
Big bet          ``big_bet``             Integer or float
Min bet          ``min_bet``             Integer or float
Starting stacks  ``starting_stacks``     Array of integers, floats, or null
Actions          ``actions``             Array of strings
================ ======================= ==================================

As of now, 11 variants are supported, each of which is written in an abbreviated form, as tabulated in Table below.

========= ==========================================================
Code      Name
========= ==========================================================
``FT``    Fixed-limit Texas hold 'em
``NT``    No-limit Texas hold 'em
``NS``    No-limit short-deck hold 'em
``PO``    Pot-limit Omaha hold 'em
``FO/8``  Fixed-limit Omaha hold 'em high/low-split eight or better
``F7S``   Fixed-limit seven card stud
``F7S/8`` Fixed-limit seven card stud high/low-split eight or better
``FR``    Fixed-limit razz
``N2L1D`` No-limit deuce-to-seven lowball single draw
``F2L3D`` Fixed-limit deuce-to-seven lowball triple draw
``FB``    Fixed-limit badugi
========= ==========================================================

These variants include all 9 played in the `2023 WSOP Event #43: $50,000 PPC -- Day 5 <https://www.pokernews.com/news/2023/06/brian-rast-wins-ppc-for-third-time-43877.htm>`_, in addition to 2 others like short-deck and badugi in which the poker community has shown growing interest. These were chosen as they adequately represent the diverse nature of poker variants and demonstrate the flexibility of the specification laid out in this paper which is powerful enough to accommodate all variants in the `2023 WSOP Tournament Rules <_static/2023-WSOP-Tournament-Rules.pdf>`_. Those not mentioned here can simply be integrated by introducing new variant codes to be associated with, and they will be introduced on a need-by-need basis based on community feedback in the future version of the specification. Please create an issue or a pull request if you have any suggestions.

The actual composition of the required fields varies, depending on the played variant. The required field statuses for each variant are described below.

========= ===== =================== ======== ========= ======= ======= =============== =======
Variant   Antes Blinds or Straddles Bring-in Small bet Big bet Min bet Starting stacks Actions
========= ===== =================== ======== ========= ======= ======= =============== =======
``FT``    yes   yes                 no       yes       yes     no      yes             yes
``NT``    yes   yes                 no       no        no      yes     yes             yes
``NS``    yes   yes                 no       no        no      yes     yes             yes
``PO``    yes   yes                 no       no        no      yes     yes             yes
``FO/8``  yes   yes                 no       yes       yes     no      yes             yes
``F7S``   yes   no                  yes      yes       yes     no      yes             yes
``F7S/8`` yes   no                  yes      yes       yes     no      yes             yes
``FR``    yes   no                  yes      yes       yes     no      yes             yes
``N2L1D`` yes   yes                 no       no        no      yes     yes             yes
``F2L3D`` yes   yes                 no       yes       yes     no      yes             yes
``FB``    yes   yes                 no       yes       yes     no      yes             yes
========= ===== =================== ======== ========= ======= ======= =============== =======

Example definitions in PHH format are shown below.

.. code-block:: toml

   # Zero antes.
   antes = [0, 0, 0, 0, 0]
   
   # Antes of 1.
   antes = [1, 1]
   
   # Big blind ante (heads-up)
   antes = [0.0, 3.0]
   
   # Big blind ante
   antes = [0.0, 3.0, 0.0]
   
   # Button ante
   antes = [0, 0, 0, 10]
   
   # Small and big blind (heads-up)
   blinds_or_straddles = [1, 2]
   
   # Small and big blind
   blinds_or_straddles = [1, 2, 0, 0, 0, 0]
   
   # Under-the-gun (UTG) straddle
   blinds_or_straddles = [1, 2, 4, 0]
   
   # UTG and UTG+1 straddle
   blinds_or_straddles = [1, 2, 4, 8, 0, 0]
   
   # Button straddle
   blinds_or_straddles = [1, 2, 0, 0, 0, 4]

.. code-block:: toml

   bring_in = 1
   small_bet = 2
   big_bet = 4

Note that the antes, blinds, and straddles are reverse-assigned for heads-up situations.

State-Construction Fields
-------------------------

The fields in this section concern itself with the topic of the initial state construction.

Variant Code
^^^^^^^^^^^^

The ``variant`` field, which has a string value, defines what variant the hand is in and therefore determines the composition of the required fields that must be specified. The field value is a code unique to each variant, which are tabulated above, along with the corresponding field requirements.

Antes
^^^^^

The value of the ``antes`` field, representing the antes, must be an array of non-negative integers or floats of length equal to the number of players. In general, there are two types of antes: uniform antes and non-uniform antes. In the case of uniform antes, all the array elements are identical, meaning the antes are the same for each player. No antes (zero antes) must be represented as an array of zero integers or floats while non-zero uniform antes can be represented as an array of constant positive TOML native numerical values. Non-uniform ante formats such as big-blind antes and button antes must be represented as an array with non-zero values in the indices corresponding to the anted players.

Note that the antes for each player are reversed in heads-up games by rule.

Blinds or Straddles
^^^^^^^^^^^^^^^^^^^

The ``blinds_or_straddles`` field, representing all forced bets except the bring-in, must only be specified in button games as an array of non-negative integers or floats of length equal to the number of players. Most button games have two blinds: a small blind and a big blind. These are simply described by an array with two positive values in the first two indices while all other elements are zero. Optionally, various straddle regimes ranging from under-the-gun straddle, double straddle, button straddle, et cetera, can be introduced by setting the elements in the relevant indices with non-zero values. Note that, in heads-up situations, the effective blind amounts are the reversed version of the array field value.

Note that the forced bets are reversed in heads-up games by rule. The ``blinds_or_straddles`` are types of forced bets only relevant in button games while the ``bring_in`` is a type of forced bet only used in stud game variants.

Bring-In
^^^^^^^^

The ``bring_in`` field is of a positive integer or float value and is primarily used in stud poker variants to represent the bring-in forced bet. The usage of bring-ins is mutually exclusive with blinds or straddles. In other words, both must never be defined together.

Small Bet
^^^^^^^^^

The ``small_bet`` field, a positive integer or a float, denotes the minimum bet in the first few betting rounds of fixed-limit games. It is not a feature of pot-limit or no-limit games.

Big Bet
^^^^^^^

The ``big_bet`` field, a positive integer or a float, similar to its smaller counterpart, denotes the minimum bet in the last few betting rounds of fixed-limit games. Again, this field is not featured in unfixed-limit games.

The ``small_bet`` and ``big_bet`` fields denote the minimum bets in the first and last few betting rounds in fixed-limit games. In no-limit or pot-limit games, these two values are, by rule, identical and therefore combined into a single ``min_bet`` field.

Min Bet
^^^^^^^

The ``min_bet`` field, a positive integer or a float, denotes the minimum bet in all of the betting rounds of no-limit or pot-limit games. This field must never be specified in fixed-limit games.

Starting Stacks
^^^^^^^^^^^^^^^

The ``starting_stacks`` field denotes the starting stacks of each player and is an array of positive integers or floats of length equal to the number of players. All stack sizes must strictly be non-zero. Unknown stack values can be denoted as ``null``.

State Progression
-----------------

The one and only field that represents the progression of a poker state is the ``actions`` field. This field is an array of string action representations, following our action notation described below. It describes how the state mutates throughout the hand as the actors -- the dealer and the players -- act.

Actions
^^^^^^^

The ``actions`` field is an array of string action notations that describe what each actor did in their turn. For the dealer (an actor), their action notations denote what cards were dealt to each player or to the board. More specifically:

- Dealing board cards or
- Dealing hole cards.

For each player, their action notations may describe them:

- Posting a bring-in;
- Completing;
- Betting;
- Raising or raising to;
- Checking;
- Calling;
- Folding;
- Standing pat;
- Discarding;
- Showing their hole cards; or
- Mucking their hole cards.

The notations in the ``actions`` field must be sorted in the order of the action. Its first element, if the array is not empty, must be the first action taken, which, in all mainstream poker variants, is the hole card dealing action by the dealer. The actions may represent a complete history of the hand or a partial history that does not reach the terminal state (the hand being over).

Action notations in the PHH File Format are shown below.

================================ ==================================================================
Action                           Grammar 
================================ ==================================================================
Dealing community cards          ``d db card(s)[ # Commentary]``
Dealing down/up cards            ``d dh pn card(s)[ # Commentary]``
Bringing in                      ``pN pb[ # Commentary]``
Completing/Betting/Raising to    ``pN cbr amount[ # Commentary]``
Checking/Calling                 ``pN cc[ # Commentary]``
Folding                          ``pN f[ # Commentary]``
Standing pat/Discarding          ``pN sd[ card(s)][ # Commentary]``
Showing/Mucking their hole cards ``pN sm[ card(s)][ # Commentary]``
No-ops                           ``[# Commentary]``
================================ ==================================================================

Each action notation aims to concisely describe the actor, the performed action, and arguments if any. The notation may also optionally include a verbal commentary. In addition, a notation may be composed entirely of a standalone commentary or be an empty string. In general, the action notation satisfies the following grammar: ``[[Actor Action[ Arguments...]][ # Commentary]]`` where contents that may be omitted are enclosed in square brackets. The words are separated by single or multiple consecutive whitespace characters, and the notation itself may contain leading or trailing whitespaces.

Note that commentaries and TOML comments are two distinct mechanisms in the PHH format. They are both followed by a single hash symbol. However, TOML comments are ignored by the parser, while the commentary information is considered a part of the action notation by the parsing system. The annotator should use commentaries to give extra contextual information about the hand that cannot be determined by the parser such as a summary of the metagame between some of the players, exposed hole cards, and interruptions, just to name a few, whereas the TOML comments should serve as a guide to the reader who is directly reading the file without the help of a software parser. For instance, the information provided by TOML comments may include the names of the betting round or the actor.

In poker, there are two types of actors: the dealer (also referred to as nature in stochastic games) and the players. The dealer is represented with a single character string ``d`` while N'th player is represented with a string ``pN`` where N is a 1-indexed player index. The actor information is often omitted in many other game history file format specifications due to redundancy. In most 2-player board games, keeping track of the actor is quite simple. However, in poker, there are often more than 2 actors that rotate around the table who, depending on the situation, are skipped. Even the actor who opens the first betting street (often referred to as pre-flop or third street) differs depending on the forced bet configurations or up cards. It is therefore difficult for human readers, let alone a machine to handle the logic of inferring the actor for each action.

Board Dealing
^^^^^^^^^^^^^

In board dealing actions, the dealer deals the community cards to the board at the beginning of each applicable street. The notation of the board dealing action must include a single argument of a valid card notation representing the newly dealt community cards.

Hole Dealing
^^^^^^^^^^^^

The hole dealing action represents the action of dealing hole cards to a particular player and must accept two arguments, the player being dealt and the newly dealt hole cards (in card notation) some or all of which may be unknown. The hole dealing must be made starting from the first active player to the last active player still in the hand.

Standing Pat/Discarding
^^^^^^^^^^^^^^^^^^^^^^^

The standing pat and discarding actions are grouped together due to their similarity. Standing pat is a special case of discarding where a player does not discard any hole cards. This notation accepts an optional argument denoting the cards that are being discarded. An omission of this argument denotes that the player in turn is standing pat while the inclusion denotes that the player discarding. All discarded cards must be part of the player's hole cards. Therefore, the card notation in the argument may contain unknown cards if and only if some of the player's hole cards are unknown.

Bring-in Posting
^^^^^^^^^^^^^^^^

This action denotes the posting of the bring-in forced bet.

Folding
^^^^^^^

This action denotes the folding action.

Checking/Calling
^^^^^^^^^^^^^^^^

This action represents checking or calling which entails matching or attempting to match the largest bet. When the amount required to match is zero, the player is said to check. Otherwise (in the case of a non-zero amount), the player is said to call.

Completion/Betting/Raising to
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This action represents completion, betting, or raising to a positive integral or real amount, supplied as an argument. This positive amount must be between the valid ranges set by the betting structure of the variant. When this action is performed as an alternative to or in the face of a bring-in, the player is said to complete. Alternatively, when nobody else bet, the player is said to be betting. Otherwise, the player is said to be making a raise.

Showing/Mucking Hole Cards
^^^^^^^^^^^^^^^^^^^^^^^^^^

The showdown action is performed at the end of the hand or after all players go all-in. It represents showing of the hole cards to try to win the pot or after an all-in, or mucking of the hole cards. This action accepts an optional argument of cards which, if supplied, must all be known. The omission of this field represents mucking while the inclusion represents showing.

No-operations
^^^^^^^^^^^^^

No-ops are represented with an empty string, a string composed entirely of whitespace characters or a standalone commentary like ``# Burn card 6s is exposed``.

Card Notation
-------------

======= =========
Rank    Character
======= =========
Ace     A        
Deuce   2        
Trey    3        
Four    4        
Five    5        
Six     6        
Seven   7        
Eight   8        
Nine    9        
Ten     T        
Jack    J        
Queen   Q        
King    K        
Unknown ?        
======= =========

======= =========
Suit    Character
======= =========
Club    c        
Diamond d        
Heart   h        
Spade   s        
Unknown ?        
======= =========

A card in the PHH format can either be known or unknown. Each known card must be represented with two characters. The first character represents the rank of the card while the second character represents the suit, as tabulated in the two tables above. An unknown card must be represented with two question mark characters: ``??``. Multiple cards must be represented by concatenating individual single-card representations without any separators or delimiters. For showdown actions only, if the hole cards being shown have already been specified during the corresponding player's hole card dealing action, the cards can be written as a single dash character: ``-``.

Certain variants like short-deck hold 'em use a non-standard deck where low ranks from deuces to fives do not exist. When a card that does not exist for a particular variant being played is specified, the parser should treat this as a violation of the specification.
