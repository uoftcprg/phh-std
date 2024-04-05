Motivational Examples
=====================

The PHH format aims to be both human-readable and writable while maintaining easy parsability by relevant software systems. In this format, the hands are described through the definitions of various key/values, along with optional comments throughout the file.

The two examples below show two historical poker hands digitalized into the PHH format. The first involves the first televised million-dollar pot between `Tom Dwan and Phil Ivey <https://www.pokernews.com/news/2018/11/poker-moments-phil-ivey-tom-dwan-million-dollar-pot-32706.htm>`_ in the 2009 Full Tilt Million Dollar Cash Game Season 4 Episode 12.

.. code-block:: toml

   # A big pot between Dwan and Ivey.
   variant = "NT"
   antes = [500, 500, 500]
   blinds_or_straddles = [1000, 2000, 0]
   min_bet = 2000
   starting_stacks = [1125600, 2000000, 553500]
   actions = [
     # Pre-flop
     "d dh p1 Ac2d",  # Ivey
     "d dh p2 ????",  # Antonius
     "d dh p3 7h6h",  # Dwan
     "p3 cbr 7000",  # Dwan
     "p1 cbr 23000",  # Ivey
     "p2 f",  # Antonius
     "p3 cc",  # Dwan
     # Flop
     "d db Jc3d5c",
     "p1 cbr 35000",  # Ivey
     "p3 cc",  # Dwan
     # Turn
     "d db 4h",
     "p1 cbr 90000",  # Ivey
     "p3 cbr 232600",  # Dwan
     "p1 cbr 1067100",  # Ivey
     "p3 cc",  # Dwan
     "p1 sm Ac2d",  # Ivey
     "p3 sm 7h6h",  # Dwan
     # River
     "d db Jh",
   ]
   author = "Juho Kim"
   event = "Million Dollar Cash Game"
   year = 2009
   players = ["Phil Ivey", "Patrik Antonius", "Tom Dwan"]
   currency = "USD"

The second hand (shown below) describes a bad beat from the final table of the `2019 WSOP Event #52: $50,000 PPC on Day 5 <https://www.pokernews.com/news/2019/07/moment-of-the-week-josh-arieh-draws-perfect-vs-bryce-yockey-34717.htm>`_ of the event between `Josh Arieh and Bryce Yockey <https://www.pokernews.com/news/2019/07/moment-of-the-week-josh-arieh-draws-perfect-vs-bryce-yockey-34717.htm>`_.

.. code-block:: toml

   # A bad beat between Yockey and Arieh.
   variant = "F2L3D"
   antes = [0, 0, 0, 0]
   blinds_or_straddles = [75000, 150000, 0, 0]
   small_bet = 150000
   big_bet = 300000
   starting_stacks = [1180000, 4340000, 5910000, 10765000]
   actions = [
     "d dh p1 7h6c4c3d2c",  # Yockey
     "d dh p2 ??????????",  # Hui
     "d dh p3 ??????????",  # Esposito
     "d dh p4 AsQs6s5c3c",  # Arieh
     "p3 f",  # Esposito
     "p4 cbr 300000",  # Arieh
     "p1 cbr 450000",  # Yockey
     "p2 f",  # Hui
     "p4 cc",  # Arieh
     "p1 sd",  # First draw; Yockey
     "p4 sd AsQs",  # Arieh
     "d dh p4 2hQh",  # Arieh
     "p1 cbr 150000",  # Yockey
     "p4 cc",  # Arieh
     "p1 sd",  # Second draw; Yockey
     "p4 sd Qh",  # Arieh
     "d dh p4 4d",  # Arieh
     "p1 cbr 300000",  # Yockey
     "p4 cc",  # Arieh
     "p1 sd",  # Third draw; Yockey
     "p4 sd 6s",  # Arieh
     "d dh p4 7c",  # Arieh
     "p1 cbr 280000",  # Yockey
     "p4 cc",  # Arieh
     "p1 sm 7h6c4c3d2c",  # Showdown; Yockey
     "p4 sm 2h4d7c5c3c",  # Arieh
   ]
   author = "Juho Kim"
   event = "2019 WSOP Event #58"
   city = "Las Vegas"
   region = "Nevada"
   country = "United States of America"
   day = 28
   month = 6
   year = 2019
   players = ["Bryce Yockey", "Phil Hui", "John Esposito", "Josh Arieh"]
