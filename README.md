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
| 3 | RAISE    | Tap/hold the **right-outer** thumb key       |
| 2 | ADJUST   | Tap/hold the **left-inner** thumb key        |

> **Smart layer keys:** the left-inner thumb (**ADJUST**) and right-outer thumb (**RAISE**)
> are dual-action: **tap = toggle the layer on/off (it stays on)**, **hold = momentary
> (only while held)**. A quick tap of RAISE locks you into numbers/arrows; tap again to
> go back.

## Base layer (Colemak)

```
,-----------------------------------------.                ,-----------------------------------------.
|  `   |  Q  |  W  |  F  |  P  |  G  |                      |  J  |  L  |  U  |  Y  |  ;  |  -   |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| TAB  |  A  |  R  |  S  |  T  |  D  |                      |  H  |  N  |  E  |  I  |  O  |  '   |
| /SFT |     |     |     |     |     |                      |     |     |     |     |     | /SFT |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|  [   |  Z  |  X  |  C  |  V  |  B  |                      |  K  |  M  |  ,  |  .  |  /  |  ]   |
| /GUI |     |     |     |     |     |                      |     |     |     |     |     | /R+S |
`-----------------------------------'                      `------------------------------------'
                   | ADJ | SPC | DEL |                      | ENT | BSPC| RSE |
                   |     | /ALT| /CTL|                      | /CTL|     |     |
                   `-----------------'                      `-----------------'
```

QWERTY (layer 1) is identical except the letters are in QWERTY order.

### Dual-function keys on the base layer

Many keys do one thing when **tapped** and another when **held** (mod-taps).
The tap action prints; the hold action acts as a modifier or layer.

| Key (position)      | Tap       | Hold              |
|---------------------|-----------|-------------------|
| Top-left **`**      | `` ` ``   | —                 |
| Top-right **-**     | `-`       | —                 |
| Mid-left **TAB**    | Tab       | Left Shift        |
| Mid-right **'**     | `'`       | Right Shift       |
| Bottom-left **[**   | `[`       | **Left GUI (Super)** |
| Bottom-right **]**  | `]`       | **RAISE + Left Shift** |
| Left thumb (inner)  | toggle ADJUST | momentary ADJUST |
| Left thumb (middle) **SPC** | Space | Left Alt (tap-preferred) |
| Left thumb (outer) **DEL**  | Delete | Left Ctrl     |
| Right thumb (inner) **ENT** | Enter | **Right Ctrl** |
| Right thumb (middle) **BSPC**| Backspace | —         |
| Right thumb (outer) | toggle RAISE | momentary RAISE |

> Hold timing is 150 ms (200 ms for Space). Tap faster than that to get the tap
> action; hold longer to get the modifier/layer.
>
> **Tap-then-hold repeats** (like the Iris): tap a dual-function key, then immediately
> press and hold it again — it repeats the *tapped* key instead of triggering the
> modifier/layer. Works on `=`, `]`, Enter, Delete, and Space. **Tab/Shift and `'`/RShift
> do not** — quick-tap is disabled on the Shift keys so rapid Shift presses (e.g. two
> capitals in a row) can never slip out as a stray Tab.
>
> The **`'`/RShift** key is *tap-preferred*: any tap types `'` (so contractions like
> `don't` and `it's` always work), and it only becomes Right Shift if you deliberately
> hold it past 200 ms — interrupting keys never force the Shift.
>
> **Space** is *tap-preferred*: it only becomes Alt if you actually hold it past 200 ms,
> so fast "space then letter" rolls always type a space (never Alt+letter). Esc and GUI
> now live on the RAISE layer (top corners), not the base layer.

## Numbers, arrows & media — the RAISE layer

Hold (or tap to toggle) the **right-outer** thumb key. The top row is the number row
(like the old Iris), the right hand has an inverted-T arrow cluster + nav, and the
left hand has media/volume. Esc and GUI sit on the top corners:

```
,-----------------------------------------.                ,-----------------------------------------.
| ESC  |  1  |  2  |  3  |  4  |  5  |                      |  6  |  7  |  8  |  9  |  0  | GUI  |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|  =   | <<  | >|| | >>  |     |     |                      | PGUP| HOME|  UP | END |  \  |      |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
|      | MUTE| VL- | VL+ |     |     |                      | PGDN| LEFT| DWN | RGT |     |      |
`-----------------------------------'                      `------------------------------------'
```

- **Numbers:** 1 2 3 4 5 / 6 7 8 9 0 across the top row (Esc left corner, GUI right corner).
- **Inverted-T arrows:** UP on the top-right row, LEFT/DOWN/RIGHT below it.
- **Navigation:** HOME/END flank UP; PAGE UP/DOWN on the outer column; `\` next to END.
- **Media:** prev / play-pause / next on the left home row.
- **Volume:** mute / vol- / vol+ on the left bottom row.

### Symbols

There's no separate symbols layer. Two ways to type them:

- **One key:** hold the bottom-right **]** key — it engages RAISE **and** Left Shift
  together, so the number row types `!@#$%^&*()` while held (and Shift+arrows selects).
- **Manual:** **RAISE + Shift + number** → e.g. RAISE makes `4`, Shift makes it `$`.

(`!@#$%^&*()` are just shifted digits; `_ + { } | :` etc. come from shifting the
other RAISE/base keys. The RAISE `=` key also holds Left Shift.)

### Word movement (Ctrl + arrows)

Hold the **left-thumb DEL/CTRL** key (gives Left Ctrl) **and** the **right-outer RAISE
thumb** (activates arrows) at the same time, then press the inverted-T arrows.
Ctrl+Left / Ctrl+Right jump by word. Add physical **Shift** for selection
(Ctrl+Shift+arrow).

## ADJUST layer (settings)

Tap/hold the **left-inner thumb** to reach ADJUST — Bluetooth, RGB, function keys,
and layout switching:

```
,-----------------------------------------.                ,-----------------------------------------.
| F12  |  F1 |  F2 |  F3 |  F4 |  F5 |                      |  F6 |  F7 |  F8 |  F9 | F10 | F11  |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| OUT  | BT0 | BT1 | BT2 | BT3 | BT4 |                      | RGB | HUE+| SAT+| BRT+| BOOT|      |
|      |     |     |     |     |     |                      | TOG |     |     |     |     |      |
|------+-----+-----+-----+-----+-----|                      |-----+-----+-----+-----+-----+------|
| CLMK | QWRT| CLR |     |     |     |                      | EFF | HUE-| SAT-| BRT-|     |      |
`-----------------------------------'                      `------------------------------------'
```

- **F1–F12:** F1–F10 across the top row, F11 on the top-right corner, F12 on the top-left.
- **Bluetooth:** `BT0`–`BT4` select profiles; **CLR** clears the current pairing;
  **OUT** toggles the output endpoint (USB ⇄ BLE).
- **Layout switch:** **CLMK** → Colemak, **QWRT** → QWERTY.
- **RGB:** **TOG** on/off, **EFF** cycle effect, **HUE/SAT/BRT ±** adjust color.
- **BOOT:** enter the bootloader for flashing (second row, right side).

### A note on Bluetooth pairing

1. Tap/hold the **left-inner thumb** to enter ADJUST.
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
