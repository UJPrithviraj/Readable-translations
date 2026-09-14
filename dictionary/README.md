# Dictionary

`jmdict.sqlite.gz` is the offline dictionary behind Readable's tap-to-define,
downloaded by the app the first time someone taps a word.

## Source and licence

It is converted from **JMdict_e**, the property of the
[Electronic Dictionary Research and Development Group](https://www.edrdg.org/),
and used in conformance with the Group's
[licence](https://www.edrdg.org/edrdg/licence.html).

This converted file is a derived work and is distributed under the same
licence: **Creative Commons Attribution-ShareAlike 4.0**
(https://creativecommons.org/licenses/by-sa/4.0/). You may use, share and
adapt it under those terms; the EDRDG retains copyright in the original
material.

## What changed from the original

Converted to SQLite by `tools/build_dictionary.py` in the Readable repository:
senses capped at 6 and glosses at 5 per sense; cross-references, examples and
restriction notes dropped; part-of-speech tags kept as their short codes.
No entries were added or reworded.
