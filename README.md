# Corne v2 (ZMK) — keymap

A ZMK keymap for a Corne v2 (`nice_nano_v2` + nice_view), ported from a QMK Iris
layout. It keeps the Colemak/QWERTY split, the mod-tap muscle memory, and the
numbers/symbols/nav layers from the original Iris.

## Hardware

- **Board:** nice_nano_v2 (both halves)
- **Display:** nice_view
- **Underglow:** WS2812 addressable strip
- Built via GitHub Actions — see [Building & flashing](#building--flashing).

## Layers at a glance

| # | Layer    | How to reach it                        |
|---|----------|----------------------------------------|
| 0 | COLEMAK  | Default at boot                        |
| 1 | QWERTY   | ADJUST → tap **QWRT** (`&to QWERTY`)   |
| 2 | LOWER    | Tap/hold the **left inner thumb**      |
| 3 | RAISE    | Tap/hold the **right inner thumb**, or hold **Tab** |
| 4 | ADJUST   | Hold **LOWER + RAISE** together        |

> **Note on layer keys:** the LOWER and RAISE thumb keys are smart:
> **tap = toggle the layer on/off (it stays on)**, **hold = momentary (only while held)**.
> So a quick tap of LOWER locks you into numbers; tap it again to go back. Holding it
> gives numbers only while your thumb is down.

## Base layer (Colemak)

```
,-----------------------------------------.                ,-----------------------------------------.
| TAB  |  Q  |  W  |  F  |  P  |  G  |                      |  J  |  L  |  U  |  Y  |  ;  | ESC  |
| /RSE |     |     |     |     |     |                      |     |     |     |     |     | /GUI |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| BSPC |  A  |  R  |  S  |  T  |  D  |                      |  H  |  N  |  E  |  I  |  O  |  '   |
| /SFT |     |     |     |     |     |                      |     |     |     |     |     | /LWR |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|  [   |  Z  |  X  |  C  |  V  |  B  |                      |  K  |  M  |  ,  |  .  |  /  |  ]   |
| /C+S |     |     |     |     |     |                      |     |     |     |     |     | /SFT |
`-----------------------------------'                      `------------------------------------'
                   | LWR | SPC | DEL |                      | ENT | RSE | DWN |
                   |     | /ALT| /CTL|                      |     |     | /C+A|
                   `-----------------'                      `-----------------'
```

QWERTY (layer 1) is identical except the letters are in QWERTY order.

### Dual-function keys on the base layer

Many keys do one thing when **tapped** and another when **held** (mod-taps).
The tap action prints; the hold action acts as a modifier or layer.

| Key (position)      | Tap    | Hold              |
|---------------------|--------|-------------------|
| Top-left **TAB**    | Tab    | RAISE layer       |
| Top-right **ESC**   | Esc    | GUI / Super (Win) |
| Mid-left **BSPC**   | Backspace | Left Shift     |
| Mid-right **'**     | `'`    | LOWER layer       |
| Bottom-left **[**   | `[`    | **Ctrl + Shift**  |
| Bottom-right **]**  | `]`    | Right Shift       |
| Left thumb (inner)  | toggle LOWER | momentary LOWER |
| Left thumb (middle) **SPC** | Space | Left Alt   |
| Left thumb (outer) **DEL**  | Delete | Left Ctrl |
| Right thumb (inner) **ENT** | Enter | —          |
| Right thumb (middle)| toggle RAISE | momentary RAISE |
| Right thumb (outer) **DWN** | Down  | Ctrl + Alt |

> Hold timing is 200 ms. Tap faster than that to get the tap action; hold longer to
> get the modifier/layer.

## Numbers — the LOWER layer

Hold (or tap to lock) the **left inner thumb**. The top row becomes the number row,
exactly like the old Iris:

```
,-----------------------------------------.                ,-----------------------------------------.
|  `   |  1  |  2  |  3  |  4  |  5  |                      |  6  |  7  |  8  |  9  |  0  |  -   |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|  =   |     |     |     |     |     |                      | HOME| PGDN| PGUP| END |     |  \   |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|      |     | <<  | >|| | >>  |     |                      | LFT | DWN |  UP | RGT |     |      |
`-----------------------------------'                      `------------------------------------'
```

- **Top row:** `` ` `` 1 2 3 4 5 / 6 7 8 9 0 `-`
- **`=`** and **`\`** sit on the home row outer columns.
- **Media:** previous / play-pause / next track on the left home row.
- **Navigation:** Home/PgDn/PgUp/End on the right home row; arrow keys on the bottom row.

## Symbols — the RAISE layer

Hold **Tab** (or tap/hold the **right inner thumb**). The top row gives shifted
number-row symbols; the right side gives brackets and operators:

```
,-----------------------------------------.                ,-----------------------------------------.
| TAB  |  !  |  @  |  #  |  $  |  %  |                      |  ^  |  &  |  *  |  (  |  )  | BSPC |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| CTRL |     |     |     |     |     |                      |  -  |  =  |  [  |  ]  |  \  |  `   |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| SHFT | MUTE| VL- | VL+ |     |     |                      |  _  |  +  |  {  |  }  | "|" |  ~   |
`-----------------------------------'                      `------------------------------------'
```

- **Top row:** `! @ # $ %` / `^ & * ( )`
- **Operators & brackets:** `- = [ ] \` and shifted `_ + { } | ~` on the right.
- **Volume:** Mute / Vol- / Vol+ on the bottom-left.

## ADJUST layer (settings)

Hold **LOWER + RAISE at the same time** to reach ADJUST. This is where Bluetooth,
RGB, function keys, and layout switching live:

```
,-----------------------------------------.                ,-----------------------------------------.
| BOOT |  F1 |  F2 |  F3 |  F4 |  F5 |                      |  F6 |  F7 |  F8 |  F9 | F10 | F11  |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| USB/ | BT0 | BT1 | BT2 | BT3 | BT4 |                      | RGB | HUE+| SAT+| BRT+| F12 | BOOT |
| BLE  |     |     |     |     |     |                      | TOG |     |     |     |     |      |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| CLMK | QWRT| CLR |     |     |     |                      | EFF | HUE-| SAT-| BRT-|     |      |
`-----------------------------------'                      `------------------------------------'
```

- **F1–F12:** function keys across the top + two on the right.
- **Bluetooth:** `BT0`–`BT4` select profiles; **CLR** clears the current pairing;
  **USB/BLE** toggles the output endpoint.
- **Layout switch:** **CLMK** → Colemak, **QWRT** → QWERTY.
- **RGB:** **TOG** on/off, **EFF** cycle effect, **HUE/SAT/BRT ±** adjust color.
- **BOOT:** enter the bootloader for flashing.

### A note on Bluetooth pairing

1. Hold **LOWER + RAISE** to enter ADJUST.
2. Tap a **BT0–BT4** key to pick a profile slot.
3. Pair from your computer/phone. To re-pair a slot, tap **CLR** first, then pair again.

## Things that work differently from the QMK Iris

- **No physical number row** — numbers live on LOWER (see above).
- **Default layer doesn't persist across reboots.** ZMK can't save the active layer to
  flash like QMK's EEPROM did. Colemak is compiled as layer 0, so the keyboard always
  **boots into Colemak**. If you switch to QWERTY via ADJUST, it resets to Colemak after
  a power cycle.
- **Bluetooth profiles and RGB settings *do* persist** across reboots automatically.
- **No automatic per-layer RGB colors.** The Corne's addressable underglow has no
  built-in per-layer coloring in ZMK, so RGB is controlled manually from ADJUST.

## Building & flashing

Pushing to GitHub triggers the **Build** GitHub Action, which compiles firmware for
both halves (with nice_view). Download the `.uf2` artifacts from the Actions run.

To flash each half:

1. Put the half into bootloader mode — double-tap the reset button, **or** press the
   **BOOT** key on the ADJUST layer.
2. It mounts as a USB drive; copy the matching `.uf2` onto it.
3. Repeat for the other half.

> **Flash both halves** whenever the keymap changes, so they stay in sync.
