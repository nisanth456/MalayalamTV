# Malayalam TV – Android IPTV app

Plays all Malayalam TV channels from the iptv-org playlist
`https://iptv-org.github.io/iptv/languages/mal.m3u` on Android phones, tablets and
Android TV / TV boxes.

## Features
* Loads the M3U playlist from the internet; keeps a saved copy so the app opens offline-fast.
* Channel grid with logos, **search**, **category filter** (News, Entertainment, Movies, Music, …)
  and **favourites** (long-press a channel; pick "★ Favourites" in the category list).
* Full-screen player (Media3 / ExoPlayer): HLS (.m3u8), DASH and direct streams;
  honours per-channel `User-Agent` / `Referer` from the playlist.
* TV remote: **D-pad Up/Down or Channel +/-** = previous/next channel, **OK** = controls.
  Shows in the Android TV launcher (leanback).
* Offline / geo-blocked channel → message with **Retry** and **Next channel**.
* Settings button (⚙) → change the playlist URL (any M3U, e.g. `https://iptv-org.github.io/iptv/countries/in.m3u`).

## Build the APK

### Option A – Android Studio (on your PC)
1. Install Android Studio (Koala or newer).
2. *File → Open* → select this folder `ANDROID-APK`.
3. Let Gradle sync (first time downloads Gradle 8.7, Android plugin and libraries).
4. *Build → Build App Bundle(s) / APK(s) → Build APK(s)*.
5. APK: `app\build\outputs\apk\debug\app-debug.apk`
   (or `Build → Generate Signed Bundle / APK` for your own signed release).

### Option B – GitHub (no Android Studio needed)
1. Create a GitHub repository and upload this folder. Put `github-workflow/build-apk.yml`
   at `.github/workflows/build-apk.yml` in the repo (GitHub web: *Add file → Create new file*,
   name `.github/workflows/build-apk.yml`, paste the content).
2. Open the **Actions** tab → *Build APK* runs automatically.
3. Download the artifact **MalayalamTV-apk** → contains `app-debug.apk` and `app-release.apk`.

## Install on phone / TV
* Phone: copy the APK → open it → allow *Install unknown apps*.
* Android TV: copy to USB or use "Send Files to TV" / "Downloader" app → open the APK.

## Project
```
app/src/main/java/com/ivl/malayalamtv/
  MainActivity.kt        channel grid, search, categories, favourites, playlist URL
  PlayerActivity.kt      ExoPlayer full-screen, channel up/down, error handling
  M3uParser.kt           #EXTINF / #EXTVLCOPT parser
  PlaylistRepository.kt  download + offline cache + favourites
  ImageLoader.kt         logo loader with memory cache
  ChannelAdapter.kt, Channel.kt, ChannelStore.kt
```
minSdk 21 (Android 5.0), targetSdk 34, Kotlin 1.9.24, AGP 8.5.2, Media3 1.4.1.

## Note
The streams are public links collected by iptv-org; the app only plays them.
Channels can be offline or blocked outside India at any time – that is the stream, not the app.
