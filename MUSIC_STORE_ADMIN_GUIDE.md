# Music Store Setup for BrickRace App

## Quick Start

The BrickRace app now syncs music from the Firebase database. Follow these steps to get music into the store:

### 1. Upload Music Files

1. Open `index.html` in BrickRaceMusicStore
2. Sign in with Firebase credentials
3. Select your category (e.g., "audio" or "lyrics")
4. Upload `.mp3`, `.m4a`, `.wav`, or `.aac` files
5. Files automatically upload to Dropbox + Firebase

### 2. Upload Lyrics Files

1. Create `.lrc` files with timestamps:
   ```
   [00:00.00] Song Title
   [00:12.34] First verse line
   [00:18.90] Another verse line
   [01:15.00] Chorus section
   ```
2. Upload to "lyrics" category
3. **Match the filename** to the audio file (e.g., `mysong.mp3` → `mysong.lrc`)

### 3. Verify in App

- Open BrickRace on Android device
- Open Music Hub (drawer menu)
- Under "BrickRace music store" section:
  - Audio files show "Play" button
  - Lyric files show "Download" button
  - Songs with matching lyrics auto-pair on playback

## Firebase Structure

Your uploaded files appear here:

```
Firebase Realtime Database
└── ads
    ├── audio
    │   ├── {key1}
    │   │   ├── fileName: "song1.mp3"
    │   │   ├── shareLink: "https://dropbox..."
    │   │   └── uploadedAt: "2025-01-15T10:30:00Z"
    │   └── {key2} (more songs)
    └── lyrics
        ├── {key1}
        │   ├── fileName: "song1.lrc"
        │   ├── shareLink: "https://dropbox..."
        │   └── uploadedAt: "2025-01-15T10:30:00Z"
        └── {key2} (more lyrics)
```

## Tips

✅ **Naming**: Keep audio and lyrics filenames consistent
- ✓ `song.mp3` + `song.lrc`
- ✗ `song.mp3` + `song_lyrics.lrc` (won't auto-pair)

✅ **Formats**:
- Audio: MP3, M4A, WAV, AAC, OGG
- Lyrics: LRC format with `[MM:SS.ms]` timestamps

✅ **File Size**: Keep under 50MB per file (Dropbox/Firebase limits)

✅ **Categories**: The app recognizes:
- `audio` → Audio files
- `lyrics` → Lyric files
- Other categories are ignored

❌ **Avoid**: Uploading duplicate filenames (will overwrite)

## Troubleshooting

### Files not appearing in app
- Wait 30 seconds for Firebase sync
- Refresh app or reopen Music Hub
- Check Firebase console: `ads` should show your categories and files

### Lyric files not syncing with audio
- Verify `.lrc` filename matches audio filename exactly
- Check lyric format: `[MM:SS.ms] text` (no extra spaces)
- Download the `.lrc` file manually from Music Hub to verify content

### Download links not working
- Verify Dropbox tokens are valid in auth.html
- Check internet connection
- Try uploading a new file

## Supported File Types

| Type | Extension | Example |
|------|-----------|---------|
| Audio | `.mp3` | song.mp3 |
| Audio | `.m4a` | song.m4a |
| Audio | `.wav` | song.wav |
| Audio | `.aac` | song.aac |
| Audio | `.ogg` | song.ogg |
| Lyrics | `.lrc` | song.lrc |

## Lyric File Format

Standard LRC format with millisecond precision:

```
[00:00.00] Song Title - Artist Name
[00:12.34] Here comes the sun
[00:18.90] And I say it's alright
[00:25.00] Verse two starts here
[01:15.50] Bridge section
[02:30.00] Final chorus
[03:45.99] Song end
```

The app syncs the **exact lyric line** matching the current playback time.

## Testing Locally

1. Upload test audio + lyrics with same filename
2. Open Music Hub on device
3. Click "Play" on the store track
4. Start a game
5. Lyric overlay should appear at top of screen
6. Lyrics should update as music plays

## Support

- **Firebase issues**: Check [Firebase Console](https://console.firebase.google.com)
- **Dropbox issues**: Verify token in `auth.html` and check [Dropbox App Console](https://www.dropbox.com/developers/apps)
- **App crashes**: Check Logcat in Android Studio for error messages
