# get_cover_art

### THE PROBLEM
Missing cover art for large imported music libraries.  

### EXISTING SOLUTIONS

1. Apple's Music App (and its predecessor iTunes) has a "Get Album Artwork" feature, but it isn't reliable and doesn't actually embed cover art into your audio files.  That means if you move your music library elsewhere, you'll be missing all your album artwork.

2. Metadata utilities like Metadatics are great (and cheap if not free), but they can require a lot of manual interaction to go through each album and select artwork from search results.  This can be forbidding for large libraries of thousands of albums.

### THIS SOLUTION
This Python package will batch-update your entire library without manual interaction for each album.

It uses Apple Music's artwork, which is already standardized and high-quality.  It also embeds the artwork directly into your audio files, so that it's independent of your player.

## Supported formats (so far)
- MP3
- MP4 (.m4a)

## Requirements
- Python 3
- Python packages: [mutagen](https://pypi.org/project/mutagen/)

## Usage
```
python get_cover_art.py <path_to_audio_library>
```

## How it works
1. First, it scans your audio library for supported files.
2. For each file without embedded artwork, looks for a local cover image based on the artist and album metadata.
3. If the cover image doesn't exist locally, attempts to download from Apple Music.
4. ignore_artwork.txt is a cache file to skip repeated attempts to download the same artwork.
5. If artwork is found, it's embedded into the audio file.

### Why do you download from Apple Music and not Google image search?
1. Google's Image Search API requires a dev token (so does Apple Music's API, but not its public web query URL).
2. Google search queries are heavily throttled.
3. Apple Music's cover sizes are standardized and sufficiently large.

## Troubleshooting

### The artwork is embedded now, but Apple's Music App still won't show it.
Try re-importing one of your embedded files.  If the re-imported version shows artwork, you need to reimport your music library.  You can do this without losing your playlists as follows:
1. File->Library->Export Library... and name your exported library file.
2. Visit Music->Preferences...->Files and screenshot your options.  You'll need to restore them later.
3. Quit the app and relaunch while holding down the Option key.
4. Choose "Create Library..." and pick a new location.
5. Visit Music->Preferences...->Files and restore your desired options.
6. File->Library->Import Playlist... and choose your library file from step 1.  (Yes, it's called "Import Playlist..." but you actually use this to import your library.)

Step 6 will take a while.

### The artwork appears in Apple's Music App but not my iOS device.
You'll have to unsync all your music and re-sync it again.  Try it with a single file first.