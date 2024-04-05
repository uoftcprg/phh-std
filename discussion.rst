Discussion
==========

The PHH format has the potential to serve as a transformational solution to various computational poker applications involving the storage of poker hands.

AI Agents
---------

The use of the PHH format can greatly benefit AI research, especially those that use reinforcement learning and ensemble learning techniques. The comprehensive hand histories allow for detailed analyses and can be used for training purposes. As previously mentioned, previous AI agents were greatly limited in scope due to the initial state assumptions they made about the game. Development of this file format serves as the crucial first step to set up the development of the poker AI agents that overcome these limitations. Furthermore, using a standardized format to share hand histories played by AI agents can also enhance transparency and enable other researchers to easily validate their findings.

Online Casinos
--------------

Online casinos that offer poker games can store hands played on their platforms in the PHH file format for archival purposes that can track player history and facilitate easier internal auditing processes. In the industry, logs of the game actions or table data at each snapshot are typically stored. This makes it difficult to carry out statistical analyses or automate certain tasks that may be of interest to these firms. An area of particular interest in online poker is cheating detection. A more highly structured data format for hand histories can facilitate the development of new tools or methods to discern unusual behaviors and identify tell-tale signs of bots. The same data (or maybe another version with the sensitive information like other players' hole cards censored out) can be provided to the players involved in the hand upon request. As an alternative to using persistent files, the developers can map each field into database table columns to store them in a queryable database.

Poker Tools
-----------

The PHH format can become a standard for sharing hands between poker players. One interesting avenue of research is in the creation of an open poker hand database akin to various chess databases which would enable poker enthusiasts to reference different hands. The platform can also serve datasets of poker hands for researchers in the field of computational poker for usage in statistical analyses and AI development.

Crowdsourcing and opening of such a database to the public can open up new avenues of poker strategy research. There are largely two schools of poker playing (and developing imperfect information game AI agents): exploitative and unexploitative plays. The first school -- the exploitative approach -- advocates for modeling opponents' behaviors and adjusting one's strategy to take advantage of imbalance in the opponent's range. The second school advocates for adopting a perfectly balanced strategy that cannot be exploited -- Nash Equilibrium. Professional players generally advocate for a mix of both, while academics have mostly focused on the second school of calculating Nash equilibrium strategies (`Gilpin and Sandholm <https://aaai.org/papers/01684-ISD05-008-optimal-rhode-island-hold-em-poker/>`_, `Cepheus <https://doi.org/10.1145/3131284>`_, `DeepStack <https://doi.org/10.1126/science.aam6960>`_, `Libratus <https://doi.org/10.1126/science.aao1733>`_, and `Pluribus <https://doi.org/10.1126/science.aay2400>`_). Commonly mentioned issues with resolving of Nash equilibrium are that there may exist multiple Nash equilibriums and that it is not well defined in games of more than 2 players due to possibilities of collusion or cooperation among players. A large database of hand histories can provide data to model an average poker player from which exploitative AI agents can be developed with a more well-defined goal of taking maximum advantage of imbalances in commonly employed human poker strategies by diverging from Nash equilibrium.
