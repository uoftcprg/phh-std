Tooling
=======

This page lists the libraries that support the PHH file format. If an entry is missing in this page, please create an issue or a pull request.

PokerKit
--------

An example code snippet loading a PHH file in `PokerKit <https://doi.org/10.1109/TG.2023.3325637>`_ is shown below.

.. code-block:: python

   from pokerkit import *
   
   # Hand loading
   
   with open("...", "rb") as file:
       hh = HandHistory.load(file)
   
   # Iterate through each action step
   
   for state in hh:
       ...
   
An example code snippet dumping a PHH file in `PokerKit <https://doi.org/10.1109/TG.2023.3325637>`_ is shown below. This hand, played between `Viktor Blom and Patrik Antonius <https://www.cardschat.com/news/10-largest-online-poker-pots-93487/>`_, holds the record for the largest online poker pot ever played.

.. code-block:: python

   from pokerkit import *
   A = Automation
   # Game state construction
   game = PotLimitOmahaHoldem(
       (
           A.ANTE_POSTING,
           A.BET_COLLECTION,
           A.BLIND_OR_STRADDLE_POSTING,
           A.CARD_BURNING,
           A.HOLE_CARDS_SHOWING_OR_MUCKING,
           A.HAND_KILLING,
           A.CHIPS_PUSHING,
           A.CHIPS_PULLING,
       ),
       True,
       0,
       (500, 1000),
       1000,
   )
   state = game((1259450.25, 678473.5), 2)
   # State progression; Pre-flop
   state.deal_hole("Ah3sKsKh")  # Antonius
   state.deal_hole("6d9s7d8h")  # Blom
   # Blom
   state.complete_bet_or_raise_to(3000)
   # Antonius
   state.complete_bet_or_raise_to(9000)
   # Blom
   state.complete_bet_or_raise_to(27000)
   # Antonius
   state.complete_bet_or_raise_to(81000)
   state.check_or_call()  # Blom
   # Flop
   state.deal_board("4s5c2h")
   # Antonius
   state.complete_bet_or_raise_to(91000)
   # Blom
   state.complete_bet_or_raise_to(435000)
   # Antonius
   state.complete_bet_or_raise_to(779000)
   state.check_or_call()  # Blom
   # Turn & River
   state.deal_board("5h")
   state.deal_board("9c")
   # Creating hand history
   hh = HandHistory.from_game_state(
       game, state,
   )
   hh.players = ["Patrik Antonius", "Viktor Blom"]
   # Dump hand
   with open("...", "wb") as file:
       hh.dump(file)
