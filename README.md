# YouTube to Anki

An Anki addon that generates a full-fledged deck with audio and pictures from a YouTube link using subtitles with the click of a button. This eliminates the need for having to download a video, or the accompanying subtitles, re-timing them, and dealing with TSV files to import. For those of you familiar with Subs2SRS, consider this to be the YouTube version.

This addon offers several features:

- Supports all languages
- Fallback to automatically generated subs if man-made captions could not be found
- Set a limit to how many cards are generated
- Choose the dimensions of the pictures
- Fast card generation

## Installation

1. In `Tools > Addons`, click `Get addon` and use the code `964531817`
2. Restart Anki for changes to take place

If you are a Linux or Mac user, make sure to install `ffmpeg` using your package manager.

## Usage

1. Enter the YouTube link for the video
2. Set an output folder for the audio and screenshots to go (can also be used for condensed audio)
3. Choose the appropriate note type and fields for the card data
4. Specify the subtitle language (default: English)
5. Hit generate. After a bit, refresh your decks, and you should see a deck named after the title of the video

## Quality of the subtitles

TL;DR: In order to get the best learning experience, work with the YouTube's
videos that have high-quality manually generated subtitles (e.g., TED talks).
Enable option "Optimize subtitles" to get sentence-based Anki cards: one card
per sentence.

The YouTube to Anki (Y2A) extension uses subtitle ranges to cut the corresponding
audio fragments out of the downloaded video. If the subtitles are well-crafted
by the creators of a YouTube video, the resulting Anki cards will 90%+ perfectly
match the audio from the MP3 files generated by the extension.

YouTube's videos can have automatically and manually generated subtitles.

When a video has manually generated subtitles, it is likely to have:

- Capitalized sentences and correct punctuation.
- Subtitle ranges matching the actual sentences as they are spoken on a video.

For the manually generated subtitles, the Y2A extension provides an optimization
which merges the subtitle texts so that the full sentences are formed, one
sentence per one Anki card. The optimization relies on the punctuation found
in the subtitles, e.g. ".", ",", "?" in order to decide when a sentence should
end. The option is enabled with the "Optimize subtitles" flag.

Examples of good YouTube videos that can be used for testing this extension:

- [The strongest predictor for success | Angela Lee Duckworth](https://www.youtube.com/watch?v=GfF2e0vyGM4&list=PLsJDRmMjwANLfCZxb25npMoR3aWFIpSRA&index=2&t=42s)
- [Elon Musk: A future worth getting excited about | TED | Tesla Texas Gigafactory interview](https://www.youtube.com/watch?v=YRvf00NooN8&t=265s)

When a video has automatically generated subtitles, it is most often that the
extension cannot produce good Anki cards: the subtitle text will have neither
capitalized letters nor punctuation, and therefore the Anki cards will not be
sentence-based.

## Development

Before moving on, be sure you have `python` and `poetry` setup.

1. Clone the repository

```
git clone https://github.com/kamui-fin/yt-to-anki.git
cd yt-to-anki
```

2. Install dependencies

```
poetry install
```

3. Install pre-commit hooks

```
poetry run pre-commit install
```

4. If you are on windows, you need to create a top-level directory called `ffmpeg` with [`ffmpeg.exe`](https://github.com/BtbN/FFmpeg-Builds/releases) inside
5. Bundle everything (or update the bundle)

```
poetry run invoke package-dev
```

6. Create a symlink of `dist/` inside of your Anki data's `addons21/` folder

```
ln -s ./dist ~/.local/share/Anki2/addons21/yt-to-anki
```

7. Now you can use the `dev` command for simultaneously running anki with the updated bundle

```
poetry run invoke dev
```

## Contributing

All contributions are gladly welcomed! Feel free to open an issue or create a pull request if you have any new changes/ideas in mind.
