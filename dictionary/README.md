# Dictionary

`jmdict.sqlite.gz` is the offline dictionary behind Readable's tap-to-define,
downloaded by the app the first time someone taps a word.

## Source and licence

It is converted from **JMdict_e_examp** (JMdict_e with example sentences), the property of the
[Electronic Dictionary Research and Development Group](https://www.edrdg.org/),
and used in conformance with the Group's
[licence](https://www.edrdg.org/edrdg/licence.html).

This converted file is a derived work and is distributed under the same
licence: **Creative Commons Attribution-ShareAlike 4.0**
(https://creativecommons.org/licenses/by-sa/4.0/). You may use, share and
adapt it under those terms; the EDRDG retains copyright in the original
material.

The example sentences come from the [Tatoeba Project](https://tatoeba.org/),
as selected and linked to JMdict senses by the EDRDG, and are licensed under
**Creative Commons Attribution 2.0 France**
(https://creativecommons.org/licenses/by/2.0/fr/).

## What changed from the original

Converted to SQLite by `tools/build_dictionary.py` in the Readable repository:
senses capped at 6 and glosses at 5 per sense; one example sentence kept per
sense where one exists; usage tags and sense notes kept; cross-references and
restriction notes dropped; part-of-speech and usage tags kept as their short
codes.
No entries were added or reworded.
