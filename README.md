# CheatGPT assets

Public static resources for `Zhoufuz/CheatGPT`; no executable remote scripts.

## Find resources

- `cheatgpt/v1/manifest.json`: complete file inventory, sizes, CRC32, SHA-256 and active/legacy status.
- `cheatgpt/v1/kill-effect/catalog.json`: kill-effect collection index.
- `cheatgpt/v1/kill-effect/valorant/collections/<collection>/manifest.json`: six stages, 30 FPS frame rectangles, durations and paired sound descriptors.
- `cheatgpt/v1/kill-effect/battlefield1/`: supplied Battlefield skull and kill sound.
- `cheatgpt/v1/fonts/`, `hitsounds/`, `icons/`: shared GUI resources.

## Valorant collections

| Collection | Directory | Media |
|---|---|---|
| 2021 Vandal | `collections/2021-vandal/` | Manifest references existing immutable `valorant-atlas/` atlases and `valorant/` sounds; binaries are not duplicated. |
| Recon | `collections/recon/` | Six transparent atlases and six original segmented kill sounds. |
| Rogue | `collections/rogue/` | Six transparent atlases and six original segmented kill sounds. |
| Singularity | `collections/singularity/` | Six transparent atlases and six original segmented kill sounds. |

The three combined source videos were supplied in `VL.zip`. Source hashes and 30 FPS cut boundaries are recorded per collection. Clips retain original timing, with each stage's audio cut on the same timeline. A centered crop removes the top-left watermark; the gray matte is removed before a single resize to the 512 x 384 logical canvas. Atlas packing preserves all visible pixels and alpha. This is extracted video artwork, not newly drawn artwork.

## Encoding and compatibility

Every resource is a raw LZMA2 stream with a 1 MiB dictionary. PNGs use LZMA2 uncompressed blocks because PNG already compresses its image data; this avoids expensive redundant Lua decoding. Audio/fonts use compressed LZMA2 blocks. Both packed and decoded sizes/checksums are verified by the client, which pins a full Git commit and caches decoded files locally.

Each stage uses one immutable atlas during playback. While Valorant Kill Effect is enabled, the client preloads all six atlas/sound pairs for each collection with at most two concurrent registration jobs. Existing decoded cache files are validated and reused; only missing or invalid files are downloaded. Per-collection registered URIs and sound objects remain reusable across selection changes and respawns.

GPU preparation is bounded: the next applicable kill stage for every collection plus the current foreground (or selected idle lookahead), at most five atlas views for the four collections. This avoids keeping all 24 full atlases resident. Selecting Collection Style does not stop or replay the current banner; the next kill captures the new selection and immediately uses its warm view and sound when ready. Cold or evicted resources can still require engine decoding. Kill counts persist through collection changes, reset on death, and counts above six use stage six.

Legacy multi-page Valorant files remain at their original content-addressed paths. They are marked `legacy` in the inventory, not deleted or moved, so earlier pinned clients remain reproducible. Do not overwrite hashed resource files with different bytes. Add new files and update manifests instead.

Source media was supplied for this project. This repository does not claim ownership of third-party artwork, sounds or fonts.
