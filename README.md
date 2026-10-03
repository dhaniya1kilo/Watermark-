# Watermark Cover (Android)

Covers a chosen word (a watermark) in a video, frame by frame, with your own text on a
rounded box. Works on images too. Everything runs **offline on the phone**.

## How it works

For every frame of the video:
1. The frame is decoded.
2. On-device OCR (Google ML Kit, model bundled in the APK) searches the frame for your word.
3. A rounded box in your background color is drawn over every place the word was found,
   with your text centered on it in your text color.
4. The frame is encoded into a new H.264 MP4. The original audio is copied unchanged.

Because it searches each frame separately, a watermark that moves around (e.g. jumps
from top to bottom) is followed.

## Using the app

1. **Pick video or image**
2. **Watermark word** – the word to find, e.g. `TikTok` or `@username` (several words work too)
3. **Your text**, **text color**, **background color** (tap a swatch or type `#RRGGBB`;
   `#AARRGGBB` gives a see-through box)
4. Sliders: corner roundness, padding around the word, text size
5. **Preview** – scans one frame and shows the result. If the word isn't found it shows
   what text the app *can* read, so you can type it the same way.
6. **Start** – progress shows frame count and how many frames were covered.
   Keep the app open (the screen stays on while it works).

Output goes to `Movies/WatermarkCover` (videos) or `Pictures/WatermarkCover` (images).

Options:
- *Tolerate small OCR mistakes* – matches even if 1–2 letters are misread.
- *Keep the box if the word is missed* – holds the last position for ~12 frames
  so the box doesn't flicker when OCR misses a blurry frame.
- *Hindi / Devanagari* – switches to the Devanagari OCR model.

Speed: each frame is OCR'd, so expect roughly 3–10 frames per second depending on phone
and resolution (a 30 s, 30 fps clip ≈ 900 frames ≈ 2–5 minutes).

## Building the APK

Requires Android 9+ on the phone.

### Option A – GitHub (no PC software needed)
1. Create a new GitHub repository and upload all files from this folder
   (keep the folder structure, including the hidden `.github` folder).
2. Open the **Actions** tab. The "Build APK" workflow runs automatically
   (or press *Run workflow*).
3. When it finishes (~5 min), open the run and download **WatermarkCover-apk**.
   Unzip it and install `app-debug.apk` on your phone (allow "install unknown apps").

### Option B – Android Studio
Open this folder in Android Studio, wait for Gradle sync, then
*Build → Build App Bundle(s)/APK(s) → Build APK(s)*.
Or from a terminal with the Android SDK installed: `./gradlew assembleDebug`.
The APK is at `app/build/outputs/apk/debug/app-debug.apk`.
