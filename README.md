# ContextTTS Gold Set — Prosody Annotation

Static annotation site. Open the GitHub Pages URL, enter an annotator ID, and
work through the pages. Download the CSV at the end and send it back.

Each page shows one conversation, one target line, and **one** synthetic clip,
and asks a single binary question: **match** or **mismatch**. Five consecutive
pages share the same conversation and target line, one per candidate clip, so
each clip is judged on its own rather than ranked against the others. 45 items
× 5 clips = 225 pages.

- `index.html`  annotator UI + guidelines (no dependencies, no backend)
- `trials.json` context, target line, intent, opaque clip ids
- `audio/`      Opus clips, hash-named. 270 are referenced by the published
                45-item set; the rest are from the full 89-item pool and are
                simply unused (see `../subset_trials.py`).

Every page also has an optional free-text **comment** box, saved per page and
exported in the CSV. **Review** in the top bar shows all 225 pages at a glance
(green match, red mismatch, blank unanswered, a dot where a comment was left)
and jumps to any of them — nothing is ever locked, including after the CSV has
been downloaded.

Every page has a **Copy link** button. The URL carries `#<trial_id>/<clip_id>`
and reopens that exact page, so a specific clip can be linked in Slack. The
link is annotator-independent; whoever opens it enters their own ID first.

Clip filenames are hashed and carry no labels; the mapping from clip to
condition is held privately and is deliberately **not** in this repo.

## Keyboard

`M` match · `X` mismatch · `1`/`2`/`3` confidence low/medium/high ·
`Space` play/pause · `Enter` next · `←` back

## CSV

One row per judgement, i.e. one row per (item, clip). The same conversation and
target therefore appear on five rows — join on `trial_id` or `item_id` to get
back to the item.

`annotator, page, trial_id, item_id, axis, target_text, target_speaker, clip,
clip_index_in_trial, clips_in_trial, verdict, is_match, confidence, broken,
comment, response_ms, presented_order, share_url, exported_at`

A page with a comment but no verdict is still exported, so nothing an annotator
wrote is lost. `verdict` is empty on those rows and the scorer excludes them
from the statistics rather than reading the blank as `mismatch`.

`confidence` is the annotator's confidence in **that page's match/mismatch
call**, not a ranking over clips.

Score the returned files with `../score_annotations.py`, which reports hit rate,
per-family false-alarm rate and d′ rather than forced-choice accuracy.
