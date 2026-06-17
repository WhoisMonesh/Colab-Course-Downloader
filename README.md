# Course Downloader

Download courses from YouTube, Coursera, and Udemy to Google Drive.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/WhoisMonesh/Colab-Course-Downloader/blob/main/Colab-Course-Downloader.ipynb)

---

## Quick Start

1. **Open in Colab** (click badge above)
2. **Mount Drive** when prompted
3. **Paste your course URL** in the `COURSE_URL` field in section 3
4. For Coursera/Udemy: upload `cookies.txt` when prompted
5. **Run all cells**

---

## Supported Platforms

| Platform | Auth Required | Method |
|---|---|---|
| **YouTube** (public playlists) | No | Just paste the URL |
| **Coursera** (enrolled courses) | Yes | Upload cookies.txt |
| **Udemy** (purchased courses) | Yes | Upload cookies.txt |

---

## Features

| Feature | Description |
|---|---|
| **Multi-platform** | YouTube playlists, Coursera courses, Udemy courses |
| **Organized Folders** | Saves as `CourseName/01 - Title.mp4` |
| **Per-lecture Progress** | Shows index (3/42), download speed, and percentage |
| **720p Default** | Balanced quality and speed for lectures |
| **Audio Only** | Toggle `AUDIO_ONLY = True` for MP3 lectures |
| **Limit Lectures** | `MAX_VIDEOS` caps how many to download |
| **Embedded Metadata** | Title, chapters, and descriptions embedded into each video |
| **Cookies Upload** | Upload `cookies.txt` for authenticated platforms |
| **Sync-safe** | Downloads locally first, then moves to Drive |
| **Keep-Alive** | JavaScript prevents Colab timeout |
| **Auto-Zip** | Zips the entire course with progress |

---

## Where to Put the URL

In section **3. Configuration**:

```python
COURSE_URL = 'https://youtube.com/playlist?list=PL...'
# or
COURSE_URL = 'https://coursera.org/learn/machine-learning'
# or
COURSE_URL = 'https://udemy.com/course/python-bootcamp/'
```

---

## Authentication (Coursera / Udemy)

You need to be enrolled in the course. Two options:

### Upload cookies.txt

1. Install a browser extension like [Get cookies.txt](https://chrome.google.com/webstore/detail/get-cookiestxt/bgaddhkoddajcdgocldbbfleckgcbcid) (Chrome) or [cookies.txt](https://addons.mozilla.org/en-US/firefox/addon/cookies-txt/) (Firefox)
2. Log into Coursera/Udemy in your browser
3. Export cookies using the extension → saves as `cookies.txt`
4. When you run the download cell, upload this file when prompted

---

## All Configuration Options

| Variable | Default | Description |
|---|---|---|
| `SAVE_PATH` | `/content/downloads/CourseDownloader/` | Local temp directory |
| `DRIVE_PATH` | `/content/drive/My Drive/CourseDownloader/` | Final Drive destination |
| `COURSE_URL` | `''` | Course URL (YouTube, Coursera, Udemy) |
| `FORMAT` | `'bestvideo[height<=720]+bestaudio/best[height<=720]'` | Video format |
| `AUDIO_ONLY` | `False` | Set `True` for MP3 audio |
| `MAX_VIDEOS` | `0` | Max lectures to download (`0` = all) |
| `USERNAME` | `''` | Optional login for Coursera/Udemy |
| `PASSWORD` | `''` | Optional password for Coursera/Udemy |
| `KEEP_ALIVE` | `True` | Prevent Colab timeout |

---

## Technical Details

- Uses [yt-dlp](https://github.com/yt-dlp/yt-dlp) which natively supports YouTube, Coursera, Udemy, and 1000+ sites
- Auto-detects platform from URL (`coursera.org`, `udemy.com`, or YouTube)
- Cookies file passed via `cookiefile` option for authenticated access
- Recursive file handling via `os.walk` for proper subdirectory zipping and Drive move
- Output template: `%(playlist_title)s/%(playlist_index)02d - %(title)s.%(ext)s`
- Downloads to `/content/downloads/` first, then `shutil.move` to Drive (avoids FUSE sync conflicts)
- Live progress via `IPython.display` HTML with `display_id`
- JavaScript keep-alive prevents Colab session timeout

---

## Fair Use & Legal Notice

This tool downloads course content for **personal, offline educational use only**.

**You agree to:**
- Only download content you are enrolled in or have legal access to
- Comply with each platform's Terms of Service
- Use downloaded content for personal offline study only
- Respect instructor copyright and course licenses

**You may NOT use this tool to:**
- Download paid/premium content without valid enrollment
- Redistribute, re-upload, or share downloaded course materials
- Monetize downloaded content in any form
- Bypass DRM, paywalls, or access controls
- Violate platform-specific terms (Coursera Honor Code, Udemy ToS, etc.)

**Disclaimer:** The authors are not responsible for how you use this software. You assume all legal responsibility for the content you download. This tool is provided for educational purposes only. Check each platform's Terms of Service before downloading.

---

## License

MIT
