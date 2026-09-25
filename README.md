# T-Display Ticker

A small battery-powered text display based on the LilyGO T-Display-S3. You set up text presets on your phone or laptop, send them to the board over Bluetooth, and after that it runs on its own.

I wanted something like a mini LED sign that I could change from my phone without installing an app, so the remote is just a web page that talks to the board through Web Bluetooth.

## Features

- Web page remote with a live preview of the screen
- Animations: static, scroll, blink, typewriter, bounce and rainbow
- Adjustable text color, background color, font (sans, serif, mono), size, speed and brightness
- Supports Latin and Cyrillic text
- Stores up to 16 presets in flash, so they survive power-off
- Low-power design for running on a battery: Bluetooth is only on when you need it, the CPU sleeps between frames, and there's a deep-sleep "off" mode, an auto-off timer and low-battery shutdown

## Buttons

| Button | Short press | Hold |
|---|---|---|
| KEY | Next preset | Turn off (press again to turn on) |
| BOOT | Bluetooth on/off | Show battery and device info |

When Bluetooth is on, a small BT badge appears in the corner: blue while waiting and green when connected. If nothing connects within 2 minutes, Bluetooth turns itself off.

## Setup

**Firmware**

1. Install VS Code with the PlatformIO extension.
2. Open the project folder, plug in the board and press Upload.

If the upload can't find the board, hold BOOT, press RST, let go of BOOT and try again.

**Web app**

The remote is `index.html` in the root of this repo. It's hosted with GitHub Pages here:
[antonkalitsov.github.io/lilygo-t-display-s3](https://antonkalitsov.github.io/lilygo-t-display-s3/)

Web Bluetooth only works over HTTPS, which GitHub Pages provides. On a laptop you can also just open the file directly in Chrome or Edge.

Browser support:
- Android: Chrome
- Windows, macOS, Linux: Chrome or Edge
- iPhone/iPad: Safari doesn't support Web Bluetooth, but the free Bluefy browser does

**Connecting**

Press BOOT on the board, click Connect on the page and pick the `TDisplay-XXXX` device. From there you can preview a preset on the board while editing it, upload all your presets, or read back what's currently saved on the board.

## Battery

Any 3.7 V LiPo with the right JST connector works, and it charges through USB-C. Battery life mostly depends on the screen brightness. If you plan to leave it in a drawer for a long time, a small switch on the battery wire is the safest way to keep it from draining.

## Project layout

```
platformio.ini        build config
src/main.cpp          firmware (display, animations, Bluetooth, power)
src/lgfx_config.h     display pin setup
src/fonts/            fonts with Latin + Cyrillic characters
tools/make_fonts.py   script that generates the fonts
index.html            the Bluetooth remote (served by GitHub Pages)
heart32.png           favicon for the web page
```

## Libraries

- [LovyanGFX](https://github.com/lovyan03/LovyanGFX) for the display
- [NimBLE-Arduino](https://github.com/h2zero/NimBLE-Arduino) for Bluetooth
- [ArduinoJson](https://arduinojson.org/)
- Fonts converted from [Liberation Fonts](https://github.com/liberationfonts/liberation-fonts) (SIL Open Font License)

Board documentation: [Xinyuan-LilyGO/T-Display-S3](https://github.com/Xinyuan-LilyGO/T-Display-S3)

## License

MIT
