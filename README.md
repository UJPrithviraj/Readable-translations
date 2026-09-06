# Readable — shared translations

English translations of Japanese song lyrics, keyed to [LRCLIB](https://lrclib.net)
record ids and served as static files over a CDN.

Used by [Readable](https://github.com/UJPrithviraj/Readable), an Android app that
shows Japanese lyrics with rōmaji and English, line-synced to whatever is playing.

## Why this exists

Translating a song is a one-time job, and the result is identical for everyone
who ever plays it. Done per user, everyone needs their own API key and most
people end up with poor machine output instead. Done once and shared, nobody
needs a key at all.

This is static files rather than a service on purpose. There is nothing to run
and nothing to pay for, reads cost nothing at any scale, and if this project is
abandoned the data is still here and still forkable.

## Layout

    translations/<last two digits of id>/<lrclib id>.json

Sharded so no directory grows to tens of thousands of files. The path is
computable from the id alone — there is no index to keep in step.

## Format

```json
{
  "schema": 1,
  "lrclib_id": 34747189,
  "source_hash": "<sha-256 of the source lines>",
  "line_count": 55,
  "translator": "groq-openai/gpt-oss-120b",
  "pipeline": 6,
  "lines": ["", "English for line 2", "..."],
  "created": "2026-09-06"
}
```

`lines` is positional and must be exactly `line_count` long, including blanks
for instrumental gaps. English is matched to the lyric sheet **by index**.

### source_hash is the important field

LRCLIB records are community-edited. If a record gains, loses or reorders a line
after a translation was published, that translation would sit one position out
for the rest of the song — and it reads as a *sync* bug, sending anyone
debugging it in completely the wrong direction.

So each entry records a fingerprint of the source it was made against, and the
client discards the entry when the source no longer matches. A stale entry
becomes a cache miss instead of a broken song.

## Contributing

Open a pull request adding or updating files. Please make sure:

- `lines` has exactly `line_count` entries, blanks included.
- No Japanese remains in any English line. Text passed through untranslated is
  the commonest defect and it is easy to check for.
- `source_hash` was computed against the current LRCLIB record.
- The translation came from a capable model. Small on-device output is the
  quality problem this repository exists to solve, so it is not accepted.

`tools/publish_translations.py` in the app repository validates all of the above
and stages files into this layout.

## Scope and takedowns

These are machine translations, not transcriptions: the Japanese source text is
not stored here, only derived English. If you hold rights to a work and want an
entry removed, open an issue and it will be deleted.
