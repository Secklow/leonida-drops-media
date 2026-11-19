# leonida-drops-media

Original graphics for **Leonida Drops**, a GTA 6 fan page.

This repository is a public, durable host for stills used by Buffer. Buffer needs a direct, permanent HTTPS file URL (not a local path, share page, or expiring link). Use the raw GitHub URL:

`https://raw.githubusercontent.com/Secklow/leonida-drops-media/main/<path>`

Example:

https://raw.githubusercontent.com/Secklow/leonida-drops-media/main/feed/2026-11-18-0900-unlock.png

After every commit that adds or changes a graphic, wait for the Decode media Action to finish, then confirm the URL returns the image (`curl -sI` should show `content-type: image/png` or the matching media type) before scheduling the Buffer post.

## Layout

- `src/` — transient base64 uploads (the GitHub connector used here cannot push binary files directly). The Action deletes them after decoding; they never stay in the repo.
- `feed/` — decoded 1080×1350 Instagram feed PNGs, written by the `decode-media` GitHub Action
- `.github/workflows/decode-media.yml` — decodes `src/*.b64` into `feed/`, removes the `.b64` files, and commits both in one commit

## How to add a new graphic

1. Make an original 1080×1350 PNG in the brand style (see `make.py` / `make_feed.py` in the working folder). No official Rockstar or platform artwork.
2. `base64 -w0 graphic.png > src/graphic.png.b64`
3. Commit the `.b64` file to the `main` branch (the connector can push this text file).
4. Wait for the Action to commit `feed/graphic.png` (the same commit removes the `.b64`). Pin that commit SHA in the URL.
5. Verify `https://cdn.jsdelivr.net/gh/Secklow/leonida-drops-media@<sha>/feed/graphic.png` returns 200 with the right content type (`image/png` or `video/mp4`). Keep the repo under jsDelivr's 50 MB package limit.
6. Pass that URL to Buffer as the post asset.

## Rules

Leonida Drops is a fan page, not affiliated with Rockstar Games, Take-Two Interactive, PlayStation, or Xbox. Only original typographic or design work belongs here. Do not add official Rockstar, PlayStation, Xbox, or third-party artwork.
