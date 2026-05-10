# birdfeed

`birdfeed` converts NPR/PRSS-delivered MP2 audio files that arrive inside WAV containers so they are usable on macOS.

PRSS delivers MP2 audio in .wav containers. With QuickTime no longer supporting MP2, these faux .wav files have become a pain to work with on macOS. `birdfeed` uses FFmpeg to rewrite the audio as a standard stereo PCM WAV file, then replaces the original file after a basic duration sanity check passes.

My intention is to make it easier to tag promos and fundraising material when the original source is delivered directly from Content Depot. Unattended automation or insertion into production workflows is at your own risk. No effort has been made to preserve the original PRSS metadata.

This has been useful for me, and as the value proposition of Mac vs. PC continues to evolve, it may prove useful for others as well.

## What It Does

- Converts the first audio stream to 16-bit stereo PCM WAV audio at 44.1 kHz.
- Keeps the original filename.
- Replaces the original file only if the converted file duration is within 1% or 0.25 seconds of the source.
- Processes one or more files in a single command.

## Prerequisites

`birdfeed` is a Bash script for macOS and other Unix-like systems. It requires:

- Bash
- FFmpeg
- FFprobe
- awk

On macOS, the easiest way to install FFmpeg is with Homebrew:

```sh
brew install ffmpeg
```

## Install

Clone the repository:

```sh
git clone https://github.com/YOUR-USERNAME/birdfeed.git
cd birdfeed
```

Make sure the script is executable:

```sh
chmod +x birdfeed
```

Optionally copy it somewhere in your `PATH`:

```sh
cp birdfeed /usr/local/bin/birdfeed
```

If you use Apple Silicon Homebrew and prefer keeping user-installed scripts with Homebrew tools, this may be a better location:

```sh
cp birdfeed /opt/homebrew/bin/birdfeed
```

## Usage

```sh
birdfeed path/to/file.wav
```

You can pass multiple files:

```sh
birdfeed path/to/first.wav path/to/second.wav
```

The script replaces each original file after conversion. If the duration check fails, the original file is left untouched and the temporary converted file is kept next to it for inspection.

## Notes

- Make a backup first if the source files are important.
- The script is intentionally small and readable so it can be inspected or modified easily.
- The output format is currently fixed at 16-bit, 44.1 kHz, stereo PCM WAV.

## License

This project is released under the MIT License. See [LICENSE](LICENSE).
