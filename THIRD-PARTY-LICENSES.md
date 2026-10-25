# Third-Party Licenses

## Google Fonts

Line Boil Generator uses the following fonts from Google Fonts, all licensed under the **SIL Open Font License 1.1**:

### Fonts Used

- **Archivo** (Sans-Serif)
  - Weights: 600, 700, 800
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Archivo

- **Asap** (Sans-Serif)
  - Weights: 400, 500, 600, 700
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Asap

- **Azeret Mono** (Monospace)
  - Weights: 400, 500, 600
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Azeret+Mono

- **Bangers** (Display)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Bangers

- **Permanent Marker** (Display)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Permanent+Marker

- **Caveat** (Handwriting)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Caveat

- **Fredoka** (Sans-Serif)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Fredoka

- **Bungee** (Display)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Bungee

- **Alfa Slab One** (Display)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Alfa+Slab+One

- **Playfair Display** (Serif)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Playfair+Display

- **Special Elite** (Display)
  - License: SIL Open Font License 1.1
  - URL: https://fonts.google.com/specimen/Special+Elite

### SIL Open Font License 1.1 Summary

The SIL Open Font License allows you to:
- Use the fonts freely in your projects (personal or commercial)
- Bundle the fonts with your application
- Modify the fonts (with proper attribution)

**Full License Text**: https://opensource.org/licenses/OFL-1.1

---

## System Fonts

The application also supports the following system fonts, which are not bundled and are assumed to be pre-installed on the user's device:

- **Georgia** (Serif) – standard on Windows, macOS, and most Linux systems
- **Impact** (Sans-Serif) – standard on Windows and macOS

These fonts are not included in this distribution and are assumed to be available under the system's own licensing.

---

## Custom Code

All code in Line Boil Generator is original, including:

- **GIF Encoder**: Hand-written implementation with LZW compression, median-cut palette, and transparency support
- **APNG Builder**: Custom implementation with frame-control chunks and delta optimization
- **ISO-BMFF Muxer**: Custom H.264 MP4 container writer (works with WebCodecs API)
- **ZIP Writer**: Store-only ZIP format with CRC32 and central directory
- **Distortion Engine**: Value-noise based procedural generation
- **Canvas Compositing**: Custom layer blending and rasterization
- **User Interface**: Vanilla JavaScript/HTML/CSS with no frameworks

No third-party libraries are used at runtime.

---

## Font Loading

Google Fonts are loaded on-demand from `https://fonts.googleapis.com` and `https://fonts.gstatic.com`. If you host this application offline, you can preload the fonts or modify the HTML `<link>` tag to serve from a local copy instead.

**Note**: Font files remain the property of their original designers and are provided by Google Fonts under the SIL Open Font License 1.1.
