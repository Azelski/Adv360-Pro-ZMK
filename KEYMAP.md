# Dev Hyprland Keymap

This profile is built for QWERTY, Polish Programmer layout, terminal/dev work,
Neovim-style navigation, RDP/Citrix stability, and Hyprland control without
using Super as the local window-manager modifier.

## Layer Model

```text
BASE          default QWERTY, no home-row tap-hold mods
NAV           hold left thumb, fast H/J/K/L navigation
SYM           hold right thumb, programming symbols and code macros
UTIL          hold NAV + SYM together, physical Mod, or right lower edge
LOCAL         hold old CapsLock key, sends F13-F24 for Hyprland
```

Home-row mods are intentionally not used. Navigation is a direct `&mo NAV`
momentary layer, so it does not depend on hold/tap timing.

## Thumb Keys

```text
Left thumb cluster:
  LCtrl, LAlt, NAV, Space, LShift, RAlt

Right thumb cluster:
  LGUI, Delete, SYM, RAlt, Enter, Backspace

Right lower edge:
  UTIL
```

`RAlt` is available on both sides for Polish diacritics through the OS Polish
Programmer layout.

CapsLock is on physical `mod4`. The old CapsLock output position now holds
`LOCAL`, and the right lower edge now holds `UTIL`.

Clique/ZMK Studio unlock is a single press on physical `mod3`.

## NAV

Hold `NAV` with the left thumb:

```text
U I O P     Insert Home PageDown PageUp End
H J K L     Left   Down Up       Right
N M , . /   CtrlLeft CtrlRight Backspace Delete Enter
;           Escape
```

## SYM

Hold `SYM` with the right thumb:

```text
Top row macros:
  |>  =>  ->  ::  ?.  ??

Q W E R T     !  @  #  $  %
Y U I O P     ^  &  *  |  ~

A S D F G     (  {  [  <  _
H J K L ;     =  >  ]  }  )

Z X C V B     '  "  `  \  -
N M , . /     +  :  ;  ?  /
```

## UTIL

Hold `NAV + SYM` together, the physical Kinesis `Mod` key, or the right lower
edge:

```text
Top row       F1-F12
Esc           Clique/ZMK Studio unlock
Q-W-E-R-T     Bluetooth profiles 0-4
A-S-D-F       sticky GUI / Alt / Ctrl / Shift
G             Bluetooth clear
Z-X-C-V       Pause / PrintScreen / Ctrl+Alt+End / Ctrl+Alt+Pause
Right hand    full numpad numbers:
              U-I-O     7 8 9
              H-J-K     4 5 6
              N-M-,     1 2 3
              bottom    0 0 .
Bottom left   Bluetooth clear all, RGB toggle, backlight down/up
Center top    bootloader
```

## LOCAL

Hold `LOCAL` on the old CapsLock output key; the keyboard sends private F keys
for Hyprland:

```text
H J K L     F13 F14 F15 F16
U I O P     F17 F18 F19 F20
N M , .     F21 F22 F23 F24
```

Suggested Hyprland convention:

```ini
bind = , F13, movefocus, l
bind = , F14, movefocus, d
bind = , F15, movefocus, u
bind = , F16, movefocus, r

bind = , F17, workspace, e-1
bind = , F18, workspace, e+1
bind = , F19, fullscreen
bind = , F20, killactive

bind = , F21, exec, grimblast copy area
bind = , F22, exec, cliphist list | wofi --dmenu | cliphist decode | wl-copy
bind = , F23, exec, loginctl lock-session
bind = , F24, submap, passthrough

submap = passthrough
bind = , F24, submap, reset
submap = reset
```
