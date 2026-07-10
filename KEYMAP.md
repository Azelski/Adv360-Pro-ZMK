# Dev Hyprland Keymap

This profile keeps standard QWERTY geometry and is optimized for the Polish
Programmer layout, terminal development, Neovim/tmux, Citrix, and Hyprland.
It deliberately avoids home-row mods and timing-sensitive typing behaviors.

## Layer Model

```text
BASE          standard QWERTY plus dedicated thumb modifiers
NAV           hold the left center thumb key
SYM           hold the right center thumb key
UTIL          hold NAV + SYM, mod2, mod3, or mod8
LOCAL         hold mod7; sends F13-F24 to Hyprland
```

The direct UTIL keys internally hold NAV and SYM. This is required because ZMK
conditional layers cannot also be activated directly with `&mo`.

## Base And Mod Keys

The number row follows the standard Advantage/QWERTY order:

```text
= 1 2 3 4 5     6 7 8 9 0 -
```

```text
mod1    Clique/ZMK Studio unlock
mod2    UTIL (right side)
mod3    UTIL (left side, convenient for the numpad and F7-F12)
mod4    Caps Lock
mod5    Caps Word
mod6    repeat the last key
mod7    LOCAL
mod8    UTIL
```

```text
Left thumb cluster:   LCtrl, LAlt, NAV, Space, LShift, RAlt
Right thumb cluster:  LGUI, RCtrl, SYM, RAlt, Enter, Backspace
```

The second Ctrl makes common GUI and CLI chords cross-hand: use right-thumb
Ctrl for C/V/X/Z/A/S/R/W/B, and left-thumb Ctrl for H/J/K/L. Delete remains on
`NAV+.`. Caps Word is preferable for constants, environment variables, and SQL
keywords because it turns itself off at punctuation.

For Polish letters, keep the OS layout set to `pl` / Polish (Programmers). Use
right-thumb RAlt for the left-hand letters A/C/E/S/X/Z and left-thumb RAlt for
the right-hand letters L/N/O. Firmware Unicode or Alt-code macros are avoided
because they are not portable through Citrix.

## NAV

Hold NAV with the left thumb:

```text
Y U I O P     Insert Home PageDown PageUp End
H J K L       Left   Down Up       Right
N M           CtrlLeft CtrlRight
, . /         Backspace Delete Enter
;             Escape
```

The base H/J/K/L keys remain available for Neovim and tmux. NAV emits real
cursor/editing keys for shells, prompts, Citrix, and GUI applications.

## SYM

Hold SYM with the right thumb:

```text
Top row macros:  |>  =>  ->  ::  ?.  ??

Tab             |       cross-hand pipe for F# and shells
Q W E R T       !  @  #  $  %
Y U I O P       ^  &  *  |  ~
A S D F G       (  {  [  <  _
H J K L ;       =  >  ]  }  )
Z X C V B       '  "  `  \  -
N M , . /       +  :  ;  ?  /
```

The sequence macros use 40 ms tap and wait times so BLE and Citrix do not group
or reorder their HID events. Editor-aware pairing stays in Neovim/IDE plugins;
firmware pairing macros would duplicate closing characters in those tools.

## UTIL

Hold either direct UTIL key, or hold NAV + SYM together:

```text
Top row         F1-F12
Q W E R T       Bluetooth profiles 0-4
A S D F         sticky GUI / Alt / Ctrl / Shift
G               clear the selected Bluetooth profile
Z               Pause
X               PrintScreen
C               Ctrl+Alt+End (RDP or Citrix UseCtrlAltEnd=True)
V               Ctrl+Alt+Enter (Citrix remote Ctrl+Alt+Delete default)
B               toggle USB/BLE output
mod5 / mod6     prefer USB / prefer BLE output
Esc             Clique/ZMK Studio unlock
```

The right hand contains an aligned keypad and media controls:

```text
Y               Num Lock
U I O           7 8 9
J K L           4 5 6
N M , .         0 1 2 3
P / Backslash   / *
; / Quote       - +
Slash / RShift  decimal / Enter
H               mute
left-well Right play/pause
{ / }           previous / next track
Left / Right    volume down / volume up
```

Select USB for the lowest-latency Citrix connection. Select BLE explicitly when
USB is connected only for charging; ZMK otherwise prefers USB automatically.

## LOCAL

Hold mod7 and use the right hand. These private F keys are handled locally by
Hyprland, including while Citrix requests shortcut inhibition:

```text
H J K L         F13-F16: focus left/down/up/right
Shift+H/J/K/L   move the active window
Ctrl+H/J/K/L    resize the active window

U / I           F17/F18: previous/next non-empty workspace
Shift+U / I     move the active window to the previous/next workspace
O               F19: maximize; Ctrl+O: true fullscreen
P               F20: toggle floating; Shift+P: close the active window

N               F21: region screenshot
M               F22: application launcher
,               F23: lock screen
.               F24: enter/leave the Hyprland passthrough submap
```

Passthrough temporarily disables the other keyboard shortcuts so Citrix can
receive Alt, Super, and other system chords. LOCAL+`.` always exits it.

## MX Master 4

The mouse complements the keyboard instead of duplicating its navigation layer:

```text
Haptic Sense panel    application launcher
Gesture button drag   move the local Hyprland window
Wheel click           normal middle click
Back / Forward        native application navigation
Thumb wheel           native horizontal scrolling
Top button            native SmartShift toggle
```

The two custom mouse controls remain local with Citrix focused and while the
keyboard passthrough submap is active. Native horizontal scrolling is retained
for code, SQL results, spreadsheets, Outlook, and Citrix applications.

## Citrix And Clique

For a Windows VDA, use Citrix Automatic (or Unicode) input with Sync Once or
Dynamic Sync so the local `pl` layout maps to Windows Polish (Programmers). If
using Scancode with No Sync, configure Polish (Programmers) inside the VDA too.

Clique/ZMK Studio stores a runtime keymap. After flashing this firmware, choose
Restore Stock Settings in Studio once; otherwise the stored layout can override
`config/adv360.keymap`. That DTS file is the firmware source of truth.

## Learning Order

1. Build accuracy on BASE and alternate hands for Ctrl/RAlt chords.
2. Add NAV until the mouse is unnecessary for text and prompt navigation.
3. Add SYM one language at a time, starting with pipe, brackets, and arrows.
4. Add LOCAL only after the typing layers are automatic.

Change at most one high-frequency binding at a time and keep it for at least a
week. Consistent repetition will improve speed more than adding more macros or
timing-sensitive layers.
