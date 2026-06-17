# Course Downloader

Download YouTube playlists and videos to Google Drive.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/WhoisMonesh/Colab-Course-Downloader/blob/main/Colab-Course-Downloader.ipynb)

---

## Quick Start

1. **Open in Colab** (click badge above)
2. **Mount Drive** when prompted
3. **Paste the YouTube URL** in the `COURSE_URL` field in section 3
4. **Run all cells**

---

## Supported Platform

| Platform | Auth Required | Method |
|---|---|---|
| **YouTube** (public playlists/videos) | No | Just paste the URL |

---

## Features

| Feature | Description |
|---|---|
| **YouTube Playlists** | Download entire playlists or single videos |
| **Organized Folders** | Saves as `PlaylistName/01 - Title.mp4` |
| **Per-video Progress** | Shows index (3/42), download speed, and percentage |
| **720p Default** | Balanced quality and speed |
| **Audio Only** | Toggle `AUDIO_ONLY = True` for MP3 extraction |
| **Limit Videos** | `MAX_VIDEOS` caps how many to download |
| **Embedded Metadata** | Title, chapters, and descriptions embedded into each video |
| **Sync-safe** | Downloads locally first, then moves to Drive |
| **Keep-Alive** | JavaScript prevents Colab timeout |
| **Auto-Zip** | Zips multiple files with live progress |

---

## Where to Put the URL

In section **3. Configuration**:

```python
COURSE_URL = 'https://youtube.com/playlist?list=PL...'
# or
COURSE_URL = 'https://youtube.com/watch?v=...'
```

---

## Authentication

YouTube content is public — no authentication required.

---

## All Configuration Options

| Variable | Default | Description |
|---|---|---|
| `SAVE_PATH` | `/content/downloads/CourseDownloader/` | Local temp directory |
| `DRIVE_PATH` | `/content/drive/My Drive/CourseDownloader/` | Final Drive destination |
| `COURSE_URL` | `''` | YouTube playlist or video URL |
| `FORMAT` | `'bestvideo[height<=720]+bestaudio/best[height<=720]'` | Video format |
| `AUDIO_ONLY` | `False` | Set `True` for MP3 audio |
| `MAX_VIDEOS` | `0` | Max videos to download (`0` = all) |
| `KEEP_ALIVE` | `True` | Prevent Colab timeout |

---

## Technical Details

- Uses [yt-dlp](https://github.com/yt-dlp/yt-dlp) for reliable YouTube downloads
- Output template: `%(playlist_title)s/%(playlist_index)02d - %(title)s.%(ext)s`
- Downloads to `/content/downloads/` first, then `shutil.move` to Drive (avoids FUSE sync conflicts)
- Live progress via `IPython.display` HTML with `display_id`
- JavaScript keep-alive prevents Colab session timeout
- Auto-zips multiple files with progress bar
- Embedded metadata via yt-dlp's `embedmetadata` and `embedchapters`

---

## Fair Use & Legal Notice

This tool downloads YouTube content for **personal, offline use only**.

**You agree to:**
- Only download content you have legal access to
- Comply with YouTube's Terms of Service
- Respect content creator copyrights

**You may NOT use this tool to:**
- Download content you do not have legal access to
- Redistribute, re-upload, or share downloaded content
- Monetize downloaded content in any form

**Disclaimer:** The authors are not responsible for how you use this software. You assume all legal responsibility for the content you download. This tool is provided for educational purposes only.

---

## License

MIT
