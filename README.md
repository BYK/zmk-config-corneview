# Corne v2 (ZMK) — keymap

A ZMK keymap for a Corne v2 (`nice_nano_v2` + nice_view), ported from a QMK Iris
layout. It keeps the Colemak/QWERTY split and the mod-tap muscle memory from the
original Iris, with numbers and navigation on a single RAISE layer.

## Hardware

This repo builds the **same keymap** for two keyboards:

| Keyboard | Controller | Feedback | Keymap file |
|----------|-----------|----------|-------------|
| **Corne v2** | nice_nano_v2 + `corne` shield | nice_view display | `config/corne.keymap` |
| **Corne Min** | `corne_min_left/right` boards (MechboardsLTD) + `rgbled_adapter` | RGB LED indicator (battery/BT) + ZMK Studio | `config/corne_min.keymap` |

Both share the same 42-key layout, so the keymaps are identical apart from
hardware-specific bits (the Corne Min has no WS2812 underglow and no nice_view, and
uses an RGB indicator LED instead). Built via GitHub Actions — see
[Building & flashing](#building--flashing).

## Layers at a glance

| # | Layer    | How to reach it                              |
|---|----------|----------------------------------------------|
| 0 | COLEMAK  | Default at boot                              |
| 1 | QWERTY   | ADJUST → tap **QWRT**                        |
| 2 | ADJUST   | Tap/hold the **left inner thumb**            |
| 3 | RAISE    | Tap/hold the **right outer thumb**           |

> **Smart layer keys:** the ADJUST and RAISE thumb keys are dual-action:
> **tap = toggle the layer on/off (it stays on)**, **hold = momentary (only while held)**.
> A quick tap of RAISE locks you into numbers/arrows; tap again to go back. Holding it
> gives that layer only while your thumb is down.

## Base layer (Colemak)

```
,-----------------------------------------.                ,-----------------------------------------.
| TAB  |  Q  |  W  |  F  |  P  |  G  |                      |  J  |  L  |  U  |  Y  |  ;  | ESC  |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| BSPC |  A  |  R  |  S  |  T  |  D  |                      |  H  |  N  |  E  |  I  |  O  |  '   |
| /SFT |     |     |     |     |     |                      |     |     |     |     |     | /SFT |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|  [   |  Z  |  X  |  C  |  V  |  B  |                      |  K  |  M  |  ,  |  .  |  /  |  ]   |
| /C+S |     |     |     |     |     |                      |     |     |     |     |     | /C+A |
`-----------------------------------'                      `------------------------------------'
                   | ADJ | SPC | DEL |                      | ENT | GUI | RSE |
                   |     | /ALT| /CTL|                      | /CTL|     |     |
                   `-----------------'                      `-----------------'
```

QWERTY (layer 1) is identical except the letters are in QWERTY order.

### Dual-function keys on the base layer

Many keys do one thing when **tapped** and another when **held** (mod-taps).
The tap action prints; the hold action acts as a modifier or layer.

| Key (position)      | Tap       | Hold              |
|---------------------|-----------|-------------------|
| Top-left **TAB**    | Tab       | —                 |
| Top-right **ESC**   | Esc       | —                 |
| Mid-left **BSPC**   | Backspace | Left Shift        |
| Mid-right **'**     | `'`       | Right Shift       |
| Bottom-left **[**   | `[`       | **Ctrl + Shift**  |
| Bottom-right **]**  | `]`       | **Ctrl + Alt**    |
| Left thumb (inner)  | toggle ADJUST | momentary ADJUST |
| Left thumb (middle) **SPC** | Space | Left Alt      |
| Left thumb (outer) **DEL**  | Delete | Left Ctrl     |
| Right thumb (inner) **ENT** | Enter | **Right Ctrl** |
| Right thumb (middle) **GUI**| GUI / Super | —        |
| Right thumb (outer) | toggle RAISE | momentary RAISE |

> Hold timing is 200 ms. Tap faster than that to get the tap action; hold longer to
> get the modifier/layer.

## Numbers, arrows & media — the RAISE layer

Tap/hold the **right outer thumb**. The top row is the number row
(like the old Iris), the right hand has an inverted-T arrow cluster + nav, and the
left hand has media/volume:

```
,-----------------------------------------.                ,-----------------------------------------.
|  `   |  1  |  2  |  3  |  4  |  5  |                      |  6  |  7  |  8  |  9  |  0  |  -   |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|  =   | <<  | >|| | >>  |     |     |                      | HOME|  UP | END |  \  |     |      |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|      | MUTE| VL- | VL+ |     |     |                      | PGUP| LFT | DWN | RGT | PGDN|      |
`-----------------------------------'                      `------------------------------------'
```

- **Numbers:** `` ` `` 1 2 3 4 5 / 6 7 8 9 0 `-` across the top row.
- **Inverted-T arrows:** UP on the home row, LFT/DWN/RGT below it.
- **Navigation:** HOME/END flank UP; PGUP/PGDN on the outer bottom; `\` next to END.
- **Media:** prev / play-pause / next on the left home row.
- **Volume:** mute / vol- / vol+ on the left bottom row.

### Symbols

There's no separate symbols layer. Type symbols the natural way:
**RAISE + Shift + number** → e.g. RAISE makes `4`, Shift makes it `$`.
(`!@#$%^&*()` are just shifted digits; `_ + { } | :` etc. come from shifting the
other RAISE/base keys.)

### Word movement (Ctrl + arrows)

Hold the **left-thumb DEL/CTRL** key (gives Left Ctrl) **and** the **right-thumb RAISE**
key (activates arrows) at the same time, then press the inverted-T arrows.
Ctrl+Left / Ctrl+Right jump by word. Add physical **Shift** for selection
(Ctrl+Shift+arrow).

## ADJUST layer (settings)

Tap/hold the **left inner thumb** to reach ADJUST — Bluetooth, RGB, function keys,
and layout switching:

```
,-----------------------------------------.                ,-----------------------------------------.
| F12  |  F1 |  F2 |  F3 |  F4 |  F5 |                      |  F6 |  F7 |  F8 |  F9 | F10 | BOOT |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| OUT  | BT0 | BT1 | BT2 | BT3 | BT4 |                      | RGB | HUE+| SAT+| BRT+| F11 |      |
|      |     |     |     |     |     |                      | TOG |     |     |     |     |      |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| CLMK | QWRT| CLR |     |     |     |                      | EFF | HUE-| SAT-| BRT-|     |      |
`-----------------------------------'                      `------------------------------------'
```

- **F1–F12:** F1–F10 on the top row, F11 on the right home row, F12 on the top-left.
- **Bluetooth:** `BT0`–`BT4` select profiles; **CLR** clears the current pairing;
  **OUT** toggles the output endpoint (USB ⇄ BLE).
- **Layout switch:** **CLMK** → Colemak, **QWRT** → QWERTY.
- **RGB:** **TOG** on/off, **EFF** cycle effect, **HUE/SAT/BRT ±** adjust color.
- **BOOT:** enter the bootloader for flashing (top-right).

### A note on Bluetooth pairing

1. Tap/hold the **left inner thumb** to enter ADJUST.
2. Tap a **BT0–BT4** key to pick a profile slot.
3. Pair from your computer/phone. To re-pair a slot, tap **CLR** first, then pair again.

## Things that work differently from the QMK Iris

- **No physical number row** — numbers live on RAISE (see above).
- **No symbols layer** — symbols come from RAISE + Shift + number, as on a normal
  keyboard's number row.
- **Default layer doesn't persist across reboots.** ZMK can't save the active layer to
  flash like QMK's EEPROM did. Colemak is compiled as layer 0, so the keyboard always
  **boots into Colemak**. Switching to QWERTY via ADJUST resets after a power cycle.
- **Bluetooth profiles and RGB settings *do* persist** across reboots automatically.
- **No automatic per-layer RGB colors.** The Corne's addressable underglow has no
  built-in per-layer coloring in ZMK, so RGB is controlled manually from ADJUST.

## Building & flashing

Pushing to GitHub triggers the **Build** GitHub Action, which compiles firmware for
both keyboards. Download the `.uf2` artifacts from the Actions run:

**Corne v2 (nice_view):**
- `corne_left nice_view_adapter nice_view` + `corne_right nice_view_adapter nice_view`

**Corne Min:**
- `corne_min_left_with_studio` — left (central) half, includes ZMK Studio support
- `corne_min_right` — right (peripheral) half

To flash each half:

1. Put the half into bootloader mode — double-tap the reset button, **or** press the
   **BOOT** key on the ADJUST layer.
2. It mounts as a USB drive; copy the matching `.uf2` onto it.
3. Repeat for the other half — **only flash `.uf2`s for the keyboard you own.**

> **Flash both halves** whenever the keymap changes, so they stay in sync.

### Corne Min notes

- The RGB indicator LED blinks battery level and Bluetooth status automatically on
  boot and profile changes. On the ADJUST layer, **BAT** (`&ind_bat`) and **CON**
  (`&ind_con`) show them on demand.
- The Corne Min build has no WS2812 underglow, so the ADJUST layer's RGB color
  controls (present on the nice_view Corne) are omitted here.
- **ZMK Studio:** the `corne_min_left_with_studio` firmware lets you edit the keymap
  live at [zmk.studio](https://zmk.studio/) over USB.
