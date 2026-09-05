# ContextTTS Gold Set — Prosody Annotation

Static annotation site. Open the GitHub Pages URL, enter an annotator ID, and
work through the trials. Download the CSV at the end and send it back.

- `index.html`  annotator UI + guidelines (no dependencies, no backend)
- `trials.json` context, target line, intent, opaque clip ids
- `audio/`      534 Opus clips (445 synthetic candidates + 89 human references)

Clip filenames are hashed and carry no labels; the mapping from clip to
condition is held privately and is deliberately **not** in this repo.
