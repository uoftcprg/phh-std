Benchmarking
============

Using the average number of newlines, words, and bytes used to represent a hand, we compare the conciseness of the following three formats: the PHH format, the PokerStars hand history format, and the format used in the supplementary of `Brown and Sandholm <https://doi.org/10.1126/science.aay2400>`_ in the table below. 

========== ================= ============== ==============
Format     # newlines / hand # words / hand # bytes / hand
========== ================= ============== ==============
PHH        9.000             101.634        544.570
PokerStars 34.359            160.519        884.711
Pluribus   1.000             1.000          125.141
========== ================= ============== ==============

The dataset of hands explored in this analysis is the 10,000 hands played by the poker AI agent Pluribus, all of which were of the no-limit Texas hold 'em variant. The PokerStars hand history version of the dataset was provided by `Wang <https://github.com/VitamintK/pluribus-hand-parser>`_ and is used for this comparison. All files exclusively use the ASCII character set.

As expected, the Pluribus's original format is the most concise of all three representations. This format is followed by the PHH file format, which is noticeably more concise than the PokerStars format, primarily thanks to its non-verbal nature in the recording method.

Note that the benchmarks of this sort for other hands included in `our dataset contribution <https://github.com/uoftcprg/phh-dataset>`_ is impossible due to the fact that the Pluribus format only supports no-limit Texas hold 'em in specific initial configurations and no documentation is available on recording hands of different variants and configurations in PokerStars notation. In addition, the concepts used in some of the histories like big blind antes are only recently emerging and therefore not supported on PokerStars.

The performance of our open-source PHH parser implementation, written in Python, is tabulated below.

====== ====================
Format Throughput (hands/s)
====== ====================
PHH    6801.31
====== ====================

The hands in `our dataset contribution <https://github.com/uoftcprg/phh-dataset>`_ were used to calculate the throughput and the parser process was run on a single CPU of Intel Core i5-4690. All the file contents were loaded into memory prior to being parsed. We utilize Python's built-in TOML file reader to parse the file and perform checks to validate the data. On average, it takes 0.147 milliseconds to parse a single hand. Note that no widely established open-source hand history parser for other file formats is available to compare with.
