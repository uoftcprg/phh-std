============================================
Poker Hand History File Format Specification
============================================

This project defines the poker hand history (PHH) file format, designed to standardize the recording of poker hands across different game variants. Despite poker's widespread popularity in the mainstream culture as a mind sport and its prominence in the field of artificial intelligence (AI) research as a benchmark for imperfect information AI agents, it lacks a consistent format that humans can use to document poker hands across different variants that can also easily be parsed by machines. To address this gap in the literature, we propose the PHH format which provides a concise human-readable machine-friendly representation of hand history that comprehensively captures various details of the hand, ranging from initial game parameters and actions to contextual parameters including but not limited to the venue, players, and time control information.

Example hand histories in the PHH format are provided in `our dataset contribution <https://github.com/uoftcprg/phh-dataset>`_, also hosted on `Zenodo <https://zenodo.org/doi/10.5281/zenodo.10796885>`_. The source code of the parser is available on GitHub as part of our `PokerKit <https://github.com/uoftcprg/pokerkit>`_ project, about which we previously published an accompanying publication on the `IEEE Transactions on Games <https://doi.org/10.1109/TG.2023.3325637>`_.

Contributing
------------

Contributions are welcome! Please read our Contributing Guide for more information.

License
-------

The PHH file format specification is distributed under the MIT license.

Citing
------

If you use the PHH file format in your research, please cite the following:

.. code-block:: bibtex

   @INPROCEEDINGS{10645611,
     author={Kim, Juho},
     booktitle={2024 IEEE Conference on Games (CoG)}, 
     title={Recording and Describing Poker Hands}, 
     year={2024},
     volume={},
     number={},
     pages={1-8},
     keywords={Graphics;Machine learning algorithms;Games;Manuals;Software systems;Distance measurement;Recording;Card games;Games of chance;Game design;Multi-agent systems;Poker;Rule based systems;Scripting;Strategy games},
     doi={10.1109/CoG60054.2024.10645611}}
