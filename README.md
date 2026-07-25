# Dilisa Lyrics Data

Synchronized lyrics database for Brazilian music, served via GitHub Pages / jsDelivr CDN.

## Structure

```
dilisa-lyrics-data/
├── manifest.json          # Track index with metadata (object keyed by Spotify ID)
├── {track_id}.lrc         # LRC files (Spotify track ID + .lrc)
└── ...
```

## Manifest Format

```json
{
  "version": "1.0.0",
  "generated": "2025-07-25T03:00:00.000Z",
  "songs": {
    "6rqhFgbbKwnb9MLmUQDhG6": {
      "id": "6rqhFgbbKwnb9MLmUQDhG6",
      "title": "Despacito",
      "artists": ["Luis Fonsi", "Daddy Yankee"],
      "album": "Vida",
      "durationMs": 281000,
      "lrcPath": "6rqhFgbbKwnb9MLmUQDhG6.lrc",
      "synced": true,
      "syncType": "line",
      "sourceUrl": "https://github.com/dilisa-lyrics/dilisa-lyrics-data"
    }
  }
}
```

- **songs**: Object keyed by Spotify track ID
- **lrcPath**: Relative path to the LRC file (same directory)
- **synced**: Whether lyrics have timing info
- **syncType**: `"line"` (line-level timestamps) or `"word"` (word-level `<time>word` format)

## LRC Format

Standard LRC format with line-level timestamps:
```
[ti:Despacito]
[ar:Luis Fonsi ft. Daddy Yankee]
[al:Vida]
[length:04:41.00]
[by:Dilisa Lyrics]
[re:https://github.com/dilisa-lyrics/dilisa-lyrics-data]
[ve:v1.0.0]
[00:00.00]Despacito
[00:02.50]¿Sí, sabes que ya llevo un rato mirándote?
[00:05.80]Tengo que bailar contigo hoy
```

Word-level format (optional, for karaoke-style highlighting):
```
[00:00.00]<1000>Despacito <2500>¿Sí,
```

## Usage

The Dilisa Lyrics app fetches:
1. `manifest.json` → finds track by Spotify ID
2. Loads `{track_id}.lrc` → parses timestamps

Via jsDelivr CDN:
```
https://cdn.jsdelivr.net/gh/dilisa-lyrics/dilisa-lyrics-data@main/manifest.json
https://cdn.jsdelivr.net/gh/dilisa-lyrics/dilisa-lyrics-data@main/{track_id}.lrc
```

## Deployment

Push to `main` branch → GitHub Pages + jsDelivr serve automatically at:
```
https://dilisa-lyrics.github.io/dilisa-lyrics-data/manifest.json
```