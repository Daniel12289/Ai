# ELren AI - PWA Package

## What's Included

This package contains your ELren AI app with full PWA (Progressive Web App) support.

## Setup Instructions

### 1. Create PNG Icons (CRITICAL - prevents Chrome badge!)

Create an `icons/` folder in the same directory as these files.

Generate two PNG files with **SOLID/OPAQUE background** (#070714):
- `icons/icon-192.png` - 192x192 pixels
- `icons/icon-512.png` - 512x512 pixels

> ⚠️ **IMPORTANT:** Use PNG with SOLID background color. Do NOT use transparent PNG or SVG. Chrome adds a white badge overlay to transparent icons. Solid PNGs render clean on the home screen.

You can generate these using:
- Figma, Photoshop, or any image editor
- Online tools like https://pwa-asset-generator.nicepkg.cn/
- Or use this placeholder command (requires ImageMagick):
  ```bash
  mkdir icons
  convert -size 192x192 xc:'#070714' -pointsize 80 -fill '#8b5cf6' -gravity center -annotate +0+0 '🤖' icons/icon-192.png
  convert -size 512x512 xc:'#070714' -pointsize 220 -fill '#8b5cf6' -gravity center -annotate +0+0 '🤖' icons/icon-512.png
  ```

### 2. Deploy

Upload all files to your web server or hosting platform:
- `index.html` (your main app - PWA enhanced)
- `manifest.json`
- `sw.js`
- `icons/icon-192.png`
- `icons/icon-512.png`

### 3. Test PWA

Open the site in Chrome/Edge on desktop or Android:
1. Open DevTools → Application → Manifest (verify it loads)
2. Open DevTools → Application → Service Workers (verify it registers)
3. Look for the install icon in the address bar (desktop) or "Add to Home Screen" prompt (mobile)

### 4. Install

- **Android Chrome:** Menu → "Add to Home Screen"
- **iOS Safari:** Share → "Add to Home Screen"
- **Desktop Chrome:** Address bar install icon → "Install"

The app will install with a clean icon — no Chrome badge/white background overlay.

---

## File Structure

```
/
├── index.html          # Main app with PWA manifest + install logic
├── manifest.json       # PWA manifest (PNG icons referenced)
├── sw.js               # Service Worker for offline support
├── README.md           # This file
└── icons/              # You create this folder
    ├── icon-192.png    # 192x192 solid PNG
    └── icon-512.png    # 512x512 solid PNG
```

## PWA Features Added to Your App

- **Manifest.json** linked in `<head>` with PNG icon references
- **Apple Touch Icon** meta tag for iOS home screen
- **Theme color** meta tags for status bar theming
- **Service Worker** registration for offline capability
- **Install Banner** UI matching your app theme (purple gradient)
- **beforeinstallprompt** capture and custom handling
- **appinstalled** event listener to hide banner after install
- **Standalone mode detection** - hides banner if already installed

## Why PNG Instead of SVG or Transparent PNG?

Chrome automatically adds a white background "badge" to SVG or transparent PNG icons when installing PWAs on Android. Using a **solid-background PNG** prevents this and gives you full control over the final icon appearance on the home screen.

According to Google Chrome documentation: "On newer Android devices, PWA icons that don't follow the maskable icon format are given a white background." Using opaque PNGs avoids this issue entirely.
