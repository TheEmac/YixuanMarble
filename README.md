# Yixuan Marble

A userscript for [Wplace.live](https://wplace.live) that overlays templates on the canvas and tracks your painting progress. It is a fork of [Skirk Marble](https://github.com/Seris0/Wplace-SkirkMarble) by Seris0, which is itself based on Blue Marble by SwingTheVine.

This README lists what Yixuan Marble adds or changes compared with Skirk Marble. Everything Skirk Marble already does (templates, color filter, enhanced crosshairs, mini tracker, search, import/export, and so on) still works the same way unless noted below.

## Install

Install a userscript manager such as Tampermonkey or Violentmonkey, then open:

```
https://raw.githubusercontent.com/TheEmac/YixuanMarble/master/yixuan-marble.user.js
```

The script has `@updateURL` and `@downloadURL` set to that address, so your userscript manager picks up new versions automatically.

## New features

### Color Filter

- **Enable Unlocked Only** button. Turns on only the colors your account has unlocked in Wplace's color picker and turns off the rest. It opens the picker in the background to read which colors are locked, then puts the picker back the way it was. You can hide the button with the **Enable Unlocked Btn** option in the display settings.
- **Enable all / Disable all Enhanced** button now reads the current state. It shows "Enable all Enhanced" when nothing is enhanced and "Disable all Enhanced" when something is, instead of always doing the same thing.
- **Unused Colors at Bottom** setting. Colors that the template doesn't use always go to the bottom of the Color Filter list, so the colors you need stay at the top.

### Enhanced crosshairs

- **Enhance Selected Color** toggle. When it is on, picking a color in Wplace's palette enhances only that color, so you only see crosshairs for the color you're painting with.
- **Crosshair Color Mode** setting, with three options:
  - **Fixed**: always use the crosshair color you chose (the original behavior).
  - **Auto (contrast when similar)**: switch to a contrasting color only where the crosshair would blend into the painted pixel underneath.
  - **Invert**: always use the inverse of the painted pixel underneath.
- **Highlight Above Error Map** toggle (on by default). Draws the enhanced crosshairs for wrong pixels on top of the error map, so they don't get hidden behind it.
- **Instant tile refresh**. Changing enhanced colors, disabled colors or crosshair settings redraws the map right away. Before, you had to wait for Wplace's own refresh, which takes about 6 to 15 seconds.

### Error map

- The Error Map button cycles through three modes instead of two:
  1. Off.
  2. **Error Map**: green for correct pixels, red for wrong ones.
  3. **Error Map + Color Hint**: wrong pixels show the color they should be, so you can eyedrop the color straight off the map and paint over the pixel.

### Wrong pixels list

- The list now has two tabs:
  - **Wrong Pixels**: pixels that are painted the wrong color.
  - **Not Placed**: template pixels that haven't been painted yet.
- Each tab shows how many pixels it has. The script remembers the last tab you used, and opens the other tab when the remembered one is empty.

### User info panel

- **Full Charge timer** shows weeks and days for long waits (for example `1w 2d 3h 4m 5s`). It also shows the exact date and time your charges will be full.
- The panel remembers whether you minimized it and stays that way after a page reload.

## Fixes

- **Shop bundles tab** no longer blanks your username or shows `NaN` for droplets and next level. The script used to read any site response whose address ended in `me` as your profile. It now ignores responses that don't contain user data.
- **Phantom remaining pixels**: progress counts no longer show pixels left to paint when the template is actually done. The cause was color keys being stored in a slightly different format than the template palette.
- **Brave browser gaps**: Brave slightly randomizes canvas colors to block fingerprinting, which made enhanced mode skip some pixels. Colors are now matched against the template palette's own keys, so those pixels are no longer missed.
- **💧 in the Color Filter list view is no longer clickable.** In Skirk Marble it selected the color by simulating a click on Wplace's palette button, which sets one of Wplace's anti-cheat flags (`UntrustedPalette`). It's now just a premium-color badge, like the 💧 on the grid cards.
- **Unlocked color detection** for Enable Unlocked Only now reads the color picker correctly.

## Performance

- Debug and performance logging is off unless you turn on debug logging. Before, it ran on every tile.
- The template color palette is cached, so it doesn't need to be rebuilt every time a tile loads.

## Other changes

- Renamed to Yixuan Marble, with a new icon and credits in the panel ("Made by Yixuan | Original by Seris0").
- Hosted on GitHub with auto-update support.

## Credits

- **Seris0**: [Skirk Marble](https://github.com/Seris0/Wplace-SkirkMarble)
- **SwingTheVine**: Blue Marble
- The "Blue Marble" image is from NASA and released under CC0 1.0.

## License

[MPL-2.0](https://www.mozilla.org/en-US/MPL/2.0/)
