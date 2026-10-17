<div align="center">

# cURL to yt-dlp Converter

A fast, lightweight, and purely client-side web utility that converts browser `cURL` network requests into ready-to-run [`yt-dlp`](https://github.com/yt-dlp/yt-dlp) commands.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

</div>

---

## 💡 Why This Tool?

When downloading video or audio streams (such as `.m3u8`, `.mpd`, or direct media chunks) protected behind session headers, custom referrers, or anti-bot protections, standard `yt-dlp <URL>` calls often fail with `403 Forbidden` or `401 Unauthorized`.

To bypass this, you typically copy the network request from your browser's Developer Tools as a `cURL` command. However, manually converting dozens of `-H 'Header: Value'` lines, extracting the User-Agent, handling cookies, and formatting them for `yt-dlp` is tedious and error-prone.

**curl2yt-dlp** automates this conversion instantly right inside your browser with zero dependencies.

---

## ✨ Features

- **Instant Parsing**: Automatically converts your command as soon as you paste it.
- **Smart Title Extraction**: Scans the `Referer` URL and media path for video titles or media codes and provides a 1-click chip to populate the output filename.
- **Generic Stream Detection & Auto-Focus**: Detects generic playlist names (`master.m3u8`, `index.m3u8`, `manifest.mpd`) and auto-focuses the title input so you can name your video immediately.
- **Filename Sanitizer & Quick Tags**: Automatically strips filesystem-illegal characters and duplicate extensions, with quick buttons for `+ Today's Date` and `+ [%(resolution)s]`.
- **Fast Concurrent Downloads**: Includes a `-N 8` (`--concurrent-fragments 8`) option to download HLS/DASH fragments in parallel, boosting download speeds by up to 5x–10x.
- **Header Translation & Bloat Sanitization**: Maps essential headers (`-H`) into `--add-header`, while stripping browser clutter (`sec-ch-*`, `sec-fetch-*`, `priority`, `accept-encoding`).
- **Segment Chunk Warning**: Detects if you accidentally copied an individual stream chunk (`.ts` / `.m4s`) instead of the master manifest (`.m3u8` / `.mpd`).
- **Remux to MP4**: `--remux-video mp4` toggle (enabled by default) to ensure video and audio streams are packaged cleanly into a standard MP4 file.
- **User-Agent Extraction**: Identifies `user-agent` and isolates it into `--user-agent "<UA>"`.
- **Optional Cookies**: Choose whether to include or exclude browser cookies (`-b` / `cookie:`) with a simple checkbox toggle.
- **1-Click Reset**: "Clear All" button (or press `Esc`) resets all inputs, output, and warnings, auto-focusing the input box ready for the next video.
- **1-Click Copy**: Copy the generated terminal command with one click.
- **100% Client-Side & Private**: Runs entirely in the browser. No requests, headers, or sensitive cookie data are ever transmitted to any external server.

---

## 🚀 How to Use

1. **Copy cURL from Browser**:
   - Open Developer Tools in your browser (`F12` or `Cmd + Option + I`).
   - Go to the **Network** tab.
   - Filter for media requests (e.g., `.m3u8`, playlist, or video manifest).
   - Right-click the request &rarr; **Copy** &rarr; **Copy as cURL** (bash).

2. **Convert**:
   - Paste the copied cURL command into the input box.
   - *(Optional)* Check **Include Cookies** if authentication cookies are required.
   - *(Optional)* Provide a custom filename in the **Custom Output Filename** field.

3. **Run**:
   - Click **Copy Command** (or select the output box).
   - Paste and run the command in your terminal:
     ```bash
     yt-dlp --add-header '...' --user-agent "..." -o '%(title)s.%(ext)s' 'https://...'
     ```

---

## 🛠️ Running Locally

Because this is a standalone static webpage, you don't need to build or install any dependencies.

### Option 1: Direct File Open
Simply double-click [`index.html`](index.html) or open it in any web browser.

### Option 2: Local HTTP Server
Run a quick local web server using Python or Node.js:

```bash
# Using Python 3
python3 -m http.server 8080

# Or using npx
npx serve .
```
Then navigate to `http://localhost:8080`.

---

## ⚙️ Tech Stack

- **HTML5 & Vanilla JavaScript** (ES6+)
- **[Tailwind CSS](https://tailwindcss.com/)** (via CDN)

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
