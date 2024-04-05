Related Works
=============

In poker literature, it has historically been the norm to describe poker games verbally as exemplified in the news articles covering the aforementioned hands (`Tom Dwan vs. Phil Ivey <https://www.pokernews.com/news/2018/11/poker-moments-phil-ivey-tom-dwan-million-dollar-pot-32706.htm>`_ and `Josh Arieh vs. Bryce Yockey <https://www.pokernews.com/news/2019/07/moment-of-the-week-josh-arieh-draws-perfect-vs-bryce-yockey-34717.htm>`_). Such a practice, while fit for human readership, presents significant challenges for parsing and computational analysis. While the description could be rich with information like the names of players involved, the backstory of the hand, et cetera, it could also lack nuances and details that may be of interest to the readers such as the exact stack sizes, bet sizes, and mucked hand values. The subjective formatting may introduce bias and inconsistencies unsuitable for scientific use cases.

One of the earliest attempts to introduce a form of structure to hand summaries was the Mike Caro University Poker Chart proposed by Mike Caro in his "`Caro's Book of Poker Tells <https://books.google.ca/books?id=vGjCntCl_ToC>`_". His tabular format where players and betting rounds are represented as a table adds a form of structure to the data that makes it easier for humans to follow. In addition, various mathematical symbols and operations such as for equals, square root, subtraction, exponentiation, and more were used to concisely represent each betting action. Caro's format serves as an innovative breakthrough when it comes to improvements in visual clarity and consistency. Unfortunately, various descriptions of poker such as stakes remain verbal, and are designed primarily for human-to-human communication. In hindsight, it failed to become a standard in the poker community, especially in the age of computer poker where machine interpretability is another vital angle that must be considered when designing such standards.

PokerStars, one of the most popular online poker platforms, saves a log of the game history in their proprietary `PokerStars Hand History format <https://www.pokerstars.com/poker/learn/news/dive-deeper-into-your-poker-play-with-hand-histories-and-reports/>`_. While the logs are designed for human readership and record-keeping, they are in plaintext format and are highly structured and consistent, allowing various poker analytic tools in the industry such as Holdem Manager, Poker Copilot, and PokerSnowie to parse and analyze a player's hand history reliably. The logged details include granular information down to the amounts of antes and blinds being posted by each player. This fine detail unfortunately makes it too verbose to be hand-typed by a human while being too specialized for use in video poker, namely PokerStars. For instance, some digital archiving use cases may require additional or complete descriptions of the game like the final stacks, time control, et cetera with features of the game not available on PokerStars. Not only that, the verbal nature of the format introduces unnecessary verbosity that wastes storage space. This flaw is further exacerbated by its lack of sufficient specification or documentation which introduces substantial difficulties when developing datasets in the PokerStars format. This is evident by the fact that there has not been any notable community effort to digitalize any historical poker hands.

The hand played by `Tom Dwan and Phil Ivey <https://www.pokernews.com/news/2018/11/poker-moments-phil-ivey-tom-dwan-million-dollar-pot-32706.htm>`_, also shown as a motivational example in the PHH file format, converted to the PokerStars hand history format is shown below. Note that unknown information is marked with question marks. Again, the starting stack of Patrik Antonius is unknown.

.. code-block::

   PokerStars Hand #????????????: Hold'em No Limit ($1000.00/$2000.00) - 2009/??/?? ??:??:?? ??? [2009/??/?? ??:??:?? ET]
   Table `?????' ?-max Seat #3 is the button
   Seat 1: PhilIvey ($1125600.00 in chips)
   Seat 2: PatrikAntonius ($2000000.00 in chips)
   Seat 3: Hero ($553500.00 in chips)
   PhilIvey: posts the ante $500.00
   PatrikAntonius: posts the ante $500.00
   Hero: posts the ante $500.00
   PhilIvey: posts small blind $1000.00
   PatrikAntonius: posts big blind $2000.00
   *** HOLE CARDS ***
   Dealt to Hero [7h 6h]
   Hero: raises $5000.00 to $7000.00
   PhilIvey: raises $16000.00 to $23000.00
   PatrikAntonius: folds
   Hero: calls $16000.00
   *** FLOP *** [Jc 3d 5c]
   PhilIvey: bets $35000.00
   Hero: calls $35000.00
   *** TURN *** [Jc 3d 5c] [4h]
   PhilIvey: bets $90000.00
   Hero: raises $142600.00 to $232600.00
   PhilIvey: raises $834500.00 to $1067100.00 and is all-in
   Hero: calls $262400.00
   Uncalled bet ($572100.00) returned to PhilIvey
   *** RIVER *** [Jc 3d 5c 4h] [Jh]
   *** SHOW DOWN ***
   PhilIvey: shows [Ac 2d] (a straight, Ace to Five)
   Hero: shows [7h 6h] (a straight, Three to Seven)
   Hero collected $1109500.00 from pot
   *** SUMMARY ***
   Total pot $1109500.00 | Rake ?
   Board [Jc 3d 5c 4h Jh]

The dataset of hands played by Pluribus, in the supplementary of `Brown and Sandholm <https://doi.org/10.1126/science.aay2400>`_, is formatted in a much more concise way, as shown below. This format includes the bare minimum description of actions to comprehensively represent a no-limit Texas hold 'em hand. However, due to the fact that each action notation does not specify the actor, the hands are difficult to follow by a human reader. In addition, the format is limited to only a single variant: no-limit Texas hold 'em, and makes critical assumptions such as the identical and fixed starting stack sizes of 100 big blinds and the number of players being 6. On top of this, it lacks options to include various metadata outside of the game state descriptions that may be of interest for data referencing purposes.

A sample hand played by Pluribus in the supplementary of `Brown and Sandholm <https://doi.org/10.1126/science.aay2400>`_ is shown below.

.. code-block::

   STATE:7:fr225fffc/cr475c/cr1225c/cc:5hJc|Jd9h|6s5c|Ah7h|2s2d|3hTs/3sJh2h/Tc/Ks:-50|1275|0|-1225|0|0:Gogo|Budd|Eddie|Bill|Pluribus|MrWhite

Standardized recording formats of other prominent board games such as `PGN <_static/PGN_Reference.txt>`_ for chess or `SGF <https://www.red-bean.com/sgf/>`_ for go provide a good direction that can be followed for the game of poker. These formats specify tags or properties that can be omitted depending on the needs of the end user for encoding information not limited to the game state or the list of actions but also numerous extra information designed to give extra context to the game played like the location or the commentary just to name a few. Our PHH format takes inspiration from the aforementioned approaches and adopts them for use in the recording of poker hand history.
