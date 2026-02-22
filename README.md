# dltkk.to — Free Video Downloader for 1000+ Sites

**[dltkk.to](https://dltkk.to)** is a free, browser-based video downloader powered by yt-dlp. No ads, no watermark, no signup. Works on iPhone, Android, and desktop.

## Features

- **1000+ platforms** — TikTok, YouTube, Twitter/X, Instagram, Twitch, Vimeo, Facebook and more
- **Multiple formats** — MP4, MP3, FLAC, WAV, AAC, MKV, GIF, thumbnail extraction
- **Batch download** — paste up to 10 URLs at once
- **GIF conversion** — convert any video to optimized looping GIF via ffmpeg
- **Zero ads** — no popups, no fake buttons, no redirects. Ever.
- **No account required** — paste a link and download, that's it
- **Mobile optimized** — works in Safari and Chrome on iPhone and Android

## How It Works

```
User pastes URL → Node.js/Express backend → yt-dlp downloads to /tmp → streams to browser → file deleted
```

Everything routes through `/tmp` (RAM-based on Linux). Nothing touches permanent disk. Files are deleted immediately after streaming completes.

## Tech Stack

- **Backend:** Node.js + Express
- **Downloader:** yt-dlp
- **Audio/Video processing:** ffmpeg
- **Frontend:** Plain HTML/CSS/JS — no frameworks, no build step
- **Rate limiting:** 3 requests per IP per minute

## Platform-Specific Notes

| Platform | Notes |
|----------|-------|
| TikTok | Requires `--impersonate chrome-131` |
| Instagram | Requires `Referer: https://www.instagram.com/` header |
| YouTube | 10 minute limit, merges video+audio via ffmpeg |
| Reddit | Blocked at datacenter IP level — no workaround currently |
| Twitter/X | Works via guest token |

## Key Technical Decisions

**Why /tmp instead of a downloads folder:**
yt-dlp can pipe to stdout with `-o -` but this breaks silently on any format requiring ffmpeg merging (most YouTube downloads). Routing through `/tmp` is RAM-based so no disk writes, and cleanup is instant after streaming.

**Why `res.on('close')` not `req.on('close')`:**
`req` fires the close event the moment the POST body is fully read — which is almost instant. This was killing yt-dlp immediately after spawning. `res.on('close')` fires only when the browser connection actually drops.

**GIF conversion:**
```bash
ffmpeg -y -i input.mp4 -vf "fps=10,scale=480:-1:flags=lanczos" -loop 0 output.gif
```
Lanczos scaling gives the best quality at small file sizes.

## Guides & Documentation

### TikTok
- [How to Download TikTok Without Watermark](https://dltkk.to/blog/download-tiktok-without-watermark.html)
- [TikTok Downloader for iPhone](https://dltkk.to/blog/tiktok-downloader-iphone.html)
- [TikTok Downloader for Android](https://dltkk.to/blog/tiktok-downloader-android.html)
- [TikTok to MP3 — Extract Audio Free](https://dltkk.to/blog/tiktok-mp3-downloader.html)
- [TikTok Downloader Not Working? Fix It](https://dltkk.to/blog/tiktok-downloader-not-working-fix.html)
- [Best TikTok Downloader 2026](https://dltkk.to/blog/best-tiktok-downloader.html)
- [TikTok Bulk Downloader](https://dltkk.to/blog/tiktok-bulk-downloader.html)
- [Download TikTok on PC](https://dltkk.to/blog/download-tiktok-on-pc.html)
- [TikTok Downloader for Chrome](https://dltkk.to/blog/tiktok-downloader-chrome.html)
- [Download TikTok Without Login](https://dltkk.to/blog/download-tiktok-without-login.html)
- [Save TikTok to Google Drive](https://dltkk.to/blog/save-tiktok-google-drive.html)
- [Download TikTok Trending Sounds](https://dltkk.to/blog/download-tiktok-trending-sounds.html)
- [TikTok Slideshow Downloader](https://dltkk.to/blog/tiktok-slideshow-downloader.html)
- [TikTok Caption Downloader](https://dltkk.to/blog/tiktok-caption-downloader.html)
- [TikTok on MacBook](https://dltkk.to/blog/tiktok-macbook.html)
- [TikTok on Windows 11](https://dltkk.to/blog/tiktok-windows-11.html)
- [Save TikTok Videos iPhone 15](https://dltkk.to/blog/save-tiktok-videos-iphone-15.html)
- [TikTok Dance Video Downloader](https://dltkk.to/blog/tiktok-dance-video-downloader.html)
- [TikTok Art Tutorial Downloader](https://dltkk.to/blog/tiktok-art-tutorial-downloader.html)
- [TikTok Educational Content Saver](https://dltkk.to/blog/tiktok-educational-content-saver.html)
- [Download TikTok Workout Videos](https://dltkk.to/blog/download-tiktok-workout-videos.html)
- [Download TikTok Life Hacks](https://dltkk.to/blog/download-tiktok-life-hacks.html)
- [Download TikTok Pet Videos](https://dltkk.to/blog/download-tiktok-pet-videos.html)
- [Save TikTok Recipe Videos](https://dltkk.to/blog/save-tiktok-recipe-videos.html)
- [Download TikTok Comedy Skits](https://dltkk.to/blog/download-tiktok-comedy-skits.html)
- [Download Private TikTok](https://dltkk.to/blog/download-private-tiktok.html)
- [TikTok Video Saver](https://dltkk.to/blog/tiktok-video-saver.html)

### YouTube
- [How to Convert YouTube to MP3](https://dltkk.to/blog/how-to-convert-youtube-to-mp3.html)
- [YouTube to MP4 Converter](https://dltkk.to/blog/youtube-to-mp4-converter.html)
- [YouTube Shorts Downloader](https://dltkk.to/blog/youtube-shorts-downloader.html)
- [YouTube Music Downloader](https://dltkk.to/blog/youtube-music-downloader.html)
- [YouTube Playlist Downloader](https://dltkk.to/blog/youtube-playlist-downloader.html)
- [YouTube Thumbnail Downloader](https://dltkk.to/blog/youtube-thumbnail-downloader.html)
- [YouTube to GIF Converter](https://dltkk.to/blog/youtube-to-gif-converter.html)
- [YouTube to MP3 320kbps](https://dltkk.to/blog/youtube-downloader-mp3-320kbps.html)
- [YouTube Shorts to Instagram Reels](https://dltkk.to/blog/youtube-shorts-to-reels.html)
- [YouTube Playlist to MP3](https://dltkk.to/blog/youtube-playlist-mp3.html)
- [YouTube Music Playlist Downloader](https://dltkk.to/blog/youtube-music-playlist-downloader.html)
- [YouTube Channel Downloader](https://dltkk.to/blog/youtube-channel-downloader.html)
- [YouTube Live Stream Downloader](https://dltkk.to/blog/youtube-live-stream-downloader.html)
- [YouTube Podcast Downloader](https://dltkk.to/blog/youtube-podcast-episode-downloader.html)
- [YouTube Documentary Downloader](https://dltkk.to/blog/youtube-documentary-downloader.html)
- [YouTube Gaming Video Downloader](https://dltkk.to/blog/youtube-gaming-video-downloader.html)
- [YouTube Vlog Downloader](https://dltkk.to/blog/youtube-vlog-downloader.html)
- [YouTube Downloader for Firefox](https://dltkk.to/blog/youtube-firefox-downloader.html)
- [Download YouTube in Safari](https://dltkk.to/blog/download-youtube-videos-safari.html)
- [Download YouTube Videos Free](https://dltkk.to/blog/download-youtube-videos-free.html)
- [Download YouTube in 4K](https://dltkk.to/blog/download-youtube-video-4k-quality.html)
- [Download YouTube Tutorials Offline](https://dltkk.to/blog/download-youtube-tutorial-offline.html)
- [Download Age Restricted YouTube](https://dltkk.to/blog/download-youtube-age-restricted.html)
- [Convert YouTube to MP4](https://dltkk.to/blog/convert-youtube-to-mp4.html)
- [Best YouTube Converters 2026](https://dltkk.to/blog/best-youtube-converters.html)

### Instagram
- [Instagram Reels Downloader](https://dltkk.to/blog/instagram-reels-downloader.html)
- [Instagram Story Downloader](https://dltkk.to/blog/instagram-story-downloader.html)
- [Instagram Video Downloader](https://dltkk.to/blog/instagram-video-downloader.html)
- [Download Instagram Photos](https://dltkk.to/blog/download-instagram-photos.html)
- [Instagram Carousel Downloader](https://dltkk.to/blog/instagram-carousel-downloader.html)
- [Instagram Highlight Downloader](https://dltkk.to/blog/instagram-highlight-downloader.html)
- [Instagram Profile Picture HD](https://dltkk.to/blog/instagram-profile-picture-hd.html)
- [Instagram Downloader Online](https://dltkk.to/blog/instagram-downloader-online.html)
- [Save Instagram Reels to Photos](https://dltkk.to/blog/save-instagram-reels-to-photos.html)
- [Instagram IGTV Downloader](https://dltkk.to/blog/instagram-igtv-downloader.html)
- [Instagram DM Video Download](https://dltkk.to/blog/instagram-dm-download.html)
- [Download Private Instagram](https://dltkk.to/blog/download-private-instagram.html)
- [Instagram Fitness Content Saver](https://dltkk.to/blog/instagram-fitness-content-saver.html)
- [Instagram Food Content Downloader](https://dltkk.to/blog/instagram-food-content-downloader.html)
- [Instagram Motivational Content](https://dltkk.to/blog/instagram-motivational-content-saver.html)
- [Save Instagram Travel Content](https://dltkk.to/blog/save-instagram-travel-content.html)
- [Instagram Fashion Content](https://dltkk.to/blog/download-instagram-fashion-content.html)
- [Instagram Business Content](https://dltkk.to/blog/download-instagram-business-content.html)

### Alternatives & Comparisons
- [Best Y2Mate Alternative 2026](https://dltkk.to/blog/y2mate-alternative.html)
- [Best SaveFrom Alternative](https://dltkk.to/blog/savefrom-alternative.html)
- [dltkk vs SnapTik](https://dltkk.to/blog/dltkk-vs-snaptik.html)
- [dltkk vs SSSTik](https://dltkk.to/blog/dltkk-vs-ssstiktok.html)

## Try It

**[https://dltkk.to](https://dltkk.to)** — free, no signup, works on any device.

---

*Built with Node.js, Express, yt-dlp, and ffmpeg.*
