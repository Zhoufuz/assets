# CheatGPT resources

Public static resources for `Zhoufuz/CheatGPT`. No executable remote scripts.

`cheatgpt/v1/manifest.json` lists each resource, its original and packed size, CRC32 and SHA-256. Files are raw LZMA2 streams with a 1 MiB dictionary; the final extension is `.lzma2`. Unpacked extensions identify PNG, MP3, WAV or TTF content.

The client pins a complete Git commit, verifies packed and decoded bytes, and caches decoded resources locally. Existing content-addressed resource files must not be replaced with different bytes.

Contents: 183 Valorant animation atlases (1024×768; four 512×384 frames per atlas), six kill sounds, existing hit sounds and UI icons, and the original full SoftRound CJK font. The 95 previous LZ4 font blocks were reconstructed byte-for-byte and compressed as one font resource to avoid 95 separate HTTP requests.

Source media was supplied for this project. This repository does not claim ownership of third-party artwork, sounds, or fonts. Git revisions and the manifest provide the integrity record.
