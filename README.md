# NH4X Volca Drum Suite

A free **step sequencer** and **editor panel** for the **Korg volca drum** inside REAPER, plus a few helper actions. Two JSFX plugins, no extra software.

By NH4X. Panel 2.6.1 · Sequencer 1.1.5. Music: https://nh4x.bandcamp.com/

![Volca Drum Panel: randomize a whole kit and watch every part change](VolcaDrumPanel.gif)

![Volca Drum Sequencer in REAPER](sequencer-preview.png)

## Contents

<table align="center">
<tr>
<th align="left">Get started</th>
<th align="left">Use it</th>
<th align="left">Reference</th>
</tr>
<tr>
<td valign="top">

1. [Install ReaPack](#step-1--install-reapack)
2. [Add this repository](#step-2--add-this-repository)
3. [Install the plugins](#step-3--install-the-two-plugins)
4. [Start the listener](#step-4--start-the-listener-once)
5. [Set up the track](#step-5--set-up-the-track)
6. [Set up the volca](#step-6--set-up-the-volca)
7. [Check it works](#check-it-works)

</td>
<td valign="top">

- [What's in it](#whats-in-it)
- [The sequencer](#the-sequencer)
  - [How to use it](#how-to-use-it)
  - [Duck trigger](#duck-trigger)
- [The panel](#the-panel)

</td>
<td valign="top">

- [Good to know](#good-to-know)
- [Other DAWs](#other-daws)
- [Split channel mode](#volca-setup-split-channel-mode)
- [Changes](#changes)
- [License](#license)

</td>
</tr>
</table>

## Install (under 5 minutes, do it once)

<p align="center">
  <a href="https://youtu.be/e6BRPumwCv8"><img src="install/video-thumbnail.png" width="640" alt="Install video on YouTube"></a>
  <br><sub>Prefer video? The whole install in under 5 minutes: https://youtu.be/e6BRPumwCv8</sub>
</p>

> [!IMPORTANT]
> Do the steps in this order. Most "it doesn't work" problems come from step 5 (MIDI out, routing, FX order) or step 6 (volca channels).

Click any screenshot to see it full size.

### Step 1 · Install ReaPack
ReaPack is the free package manager for REAPER. Already have it? Go to step 2.

1. Go to https://reapack.com/ and download ReaPack for your system (Windows: `reaper_reapack-x64.dll`).
2. Find the downloaded file in your **Downloads** folder and **copy** it.
3. In REAPER: **Options > Show REAPER resource path in explorer/finder**. A file window opens.
4. Open the folder **UserPlugins** in there (if it's missing, create it) and **paste** the file.
5. **Close REAPER and start it again.** ReaPack opens its *Manage repositories* window once: that means it works.

<p align="center">
  <a href="install/1-reapack-download.png"><img src="install/1-reapack-download.png" height="200" alt="reapack.com download page with the quick install steps"></a>
  <a href="install/1-resource-path.png"><img src="install/1-resource-path.png" height="200" alt="Options menu: Show REAPER resource path in explorer/finder"></a>
  <br><sub>Download ReaPack · Options > Show REAPER resource path</sub>
</p>
<p align="center">
  <a href="install/1-userplugins.png"><img src="install/1-userplugins.png" width="720" alt="The ReaPack dll pasted into the UserPlugins folder"></a>
  <br><sub>The dll in <code>UserPlugins</code></sub>
</p>

### Step 2 · Add this repository
1. In REAPER: **Extensions > ReaPack > Import repositories...** (or, in the *Manage repositories* window: **Import/export... > Import repositories...**).
2. Paste this line and click **OK**:

```
https://github.com/NH4Xnet/volca-drum-suite/raw/main/index.xml
```

<p align="center">
  <a href="install/2-import-repository.png"><img src="install/2-import-repository.png" width="440" alt="Import repositories dialog with the URL pasted"></a>
</p>

### Step 3 · Install the two plugins
1. **Extensions > ReaPack > Browse packages**.
2. Type **volca** into the filter.
3. Right-click **Volca Drum Sequencer** > **Install**, then right-click **Volca Drum Panel** > **Install**.
4. Confirm with **Apply** (or **OK**).

This also installs the helper actions (they all start with "Volca" in the action list).

<p align="center">
  <a href="install/3-browse-packages.png"><img src="install/3-browse-packages.png" width="540" alt="Browse packages filtered to volca, right-click > Install"></a>
</p>

### Step 4 · Start the listener (once)
The panel and the sequencer need a small background helper to talk to each other (it also saves sound files and reads your regions).

1. **Actions > Show action list**.
2. Search for **volca listener**.
3. Select **Script: Volca listener (start).lua** and click **Run** (or double-click it).
4. A window asks if it may start with REAPER from now on: click **Yes**.
5. A message confirms it. From now on it starts with REAPER by itself. (If you click No, it runs until you close REAPER and asks again next time.)

<p align="center">
  <a href="install/4-listener.png"><img src="install/4-listener.png" width="440" alt="Volca listener: start it automatically with REAPER? Yes"></a>
</p>

### Step 5 · Set up the track
1. **Add a track** (**Track > Insert new track**).
2. **Enable MIDI out to your volca**: **Options > Preferences > Audio > MIDI Outputs**, right-click the port your volca is plugged into > **Enable output**. The **Enable** column shows a dot for that port.
   The **Clock** column must stay **empty**: REAPER must not send MIDI clock to the volca, or the volca's own sequencer starts playing along. (If it shows a dot, right-click the port and switch the clock off.) Click **OK**.
3. **Open the track's routing window** (the track's **Route** button).
4. Under **MIDI Hardware Output** pick your volca's MIDI port and **Send to original channels**. (Not a single channel: the parts listen on channels 1-6.) Close the window.

<p align="center">
  <a href="install/5-midi-output.png"><img src="install/5-midi-output.png" height="230" alt="Preferences > MIDI Outputs: volca port enabled, Clock column empty"></a>
  <a href="install/5-route.png"><img src="install/5-route.png" height="230" alt="Routing window: MIDI Hardware Output = volca port, Send to original channels"></a>
  <br><sub>MIDI output enabled, no clock · Routing: MIDI Hardware Output</sub>
</p>

5. Click the track's **FX** button and type **volca** into the filter.
6. Add **first the Volca Drum Sequencer**, **then the Volca Drum Panel**. The order matters.
7. **Arm the track** (its record button). Then the sequencer also runs smoothly while REAPER is stopped (FREE mode) and hears your MIDI keyboard for tap record.

<p align="center">
  <a href="install/5-add-fx.png"><img src="install/5-add-fx.png" height="230" alt="Add FX filtered to volca: sequencer first"></a>
  <a href="install/6-done.png"><img src="install/6-done.png" height="230" alt="Done: Volca Drum Sequencer and Panel on the track"></a>
  <br><sub>Sequencer first, then panel · Done</sub>
</p>

### Step 6 · Set up the volca
- **Split channel mode**, so part 1-6 listen on MIDI channel 1-6. It's the factory default. How to check it or switch it back: [Volca setup: split channel mode](#volca-setup-split-channel-mode). Korg manual: https://www.korg.com/us/support/download/product/0/809/
- Recommended: the custom firmware **vdcf 1.22** by hj-oja: https://github.com/hj-oja/vdcf
  It adds FILT and CLIP (the purple rows in the panel) and makes velocity work like this: 63 = the panel's LEVEL, lower = ghost note, higher = accent. On the stock firmware everything else works.

**You are done.** To hear the volca through REAPER (if its audio comes back through your audio interface): add a second track, set its input to the volca's input, arm it and turn record monitoring on. Otherwise you hear it from its own output or your mixer.

### Check it works
1. In the panel, press **SEND ALL**. Then press the **play button** in a part header: the volca plays one hit.
2. In the sequencer, click a few steps in lane 1 and press play in REAPER: you hear the pattern.
3. In the panel, click a part title, then **SOUND > SAVE PART**: the display shows the saved name. (If it says *RUN ACTION 'VOLCA LISTENER (START)'*, do step 4.)

## What's in it

| What | Where | What it does |
|---|---|---|
| **Volca Drum Sequencer** | FX browser: JS | 6 lanes × 64 steps for the 6 volca parts. See below. |
| **Volca Drum Panel** | FX browser: JS | Every parameter of all 6 parts + waveguide on one screen, kits, sounds, randomize, morph. See below. |
| Volca listener (start) | Action list | Background helper: sound save / rename / delete, regions = patterns. Step 4. |
| Volca kit (save) / (kit +) / (kit -) / (send all) | Action list | Save the panel as a new kit, next / previous kit, send the whole kit. For keys or a MIDI controller. |
| Volca sound (save) / (load) | Action list | Save / load the focused part as a sound file. For keys or a MIDI controller (the panel's SOUND menu does the same). |
| Volca duck to selected tracks | Action list | Lets the sequencer duck other tracks (sidechain style). See **Duck trigger**. |

## The sequencer

| Feature | What it does |
|---|---|
| **Steps** | Click = on, click again = off, drag = paint / erase. Velocity, slice (ratchets), condition, offset and ramp per step (view tabs and right-click menu). |
| **Lanes** | Each lane has its own length and rate (polymeter), direction, swing, humanize, pitch, mute / solo. |
| **Conditions** | Chance, A:B loops, 1ST, FILL, PRE, NEI (like the vdcf firmware's own sequencer). **FILL** switch + **AUTO FILL** every n bars. |
| **P-locks** | Per step, any panel parameter (P-LOCK tab, PARAM button). The value comes back after the hit. Trigless steps = locks only, no note. |
| **Patterns** | 16 patterns, chain, fill pattern. **Regions = patterns**: name regions "P1 …", "P2 …" and the song switches patterns by itself (needs the listener). |
| **Kit per pattern** | Each pattern can switch the panel to a saved kit. |
| **Feel** | Global swing, CHAOS (one knob that loosens everything), DENSITY (thin out / fill up), EVOLVE (small changes every n bars). |
| **Beat generator** | GEN styles fill the lanes with a starting groove: 28 styles from old EBM, futurepop and rhythm noise to house, breakbeat, DnB, trap, funk, bossa nova and swing. |
| **Sync** | SYNC REAPER = locked to the project (loops, jumps, render). FREE = own play button and tempo. |
| **Tap record** | Play the parts on MIDI channel 1-6 and the hits land on the nearest step. |

Rest the mouse for a second on a control and the readout says what it does. **Ctrl+C / V / A / Z stay with REAPER**, so copy / paste / undo live in the right-click menus. Pattern data is saved with the project; REAPER presets of the sequencer = whole sequencer states.

### How to use it

| Action | How |
|---|---|
| Steps on / off | Click a step. Drag from an empty step = paint, from a lit step = erase |
| Velocity | Mouse wheel on a lit step, or paint it in the **VELOCITY** tab. 63 = the panel's LEVEL, lower = ghost note, higher = accent |
| Select steps | **Ctrl+click** = add, **Ctrl+drag** = box (across lanes too), **Shift+click** = range, **Esc** = none. The STEP tab and the right-click menu then change all selected steps |
| Step values | **VIEW** tabs (VELOCITY, CHANCE, SLICE, OFFSET, PITCH, P-LOCK): drag across lit steps, the height sets the value. **Alt+drag** = back to default |
| Copy / paste / undo | Right-click a step. **Del** deletes the selected steps |
| Lane length / rate | **LEN** / **RATE** in the lane strip (drag, wheel, right-click = list), or drag in the thin strip above a lane. **Shift** = all six lanes |
| Hear a part | Click the part name: it plays once |
| Mute / solo | **M** / **S** in the lane strip. **Shift+click** = clear all |
| Play a part melodically | **PIT** box in the lane strip = base note, then paint semitones in the **PITCH** tab. It switches the panel's **Q** on for that part |
| P-lock | **P-LOCK** tab, pick the parameter in the field with ▼, paint by height. **RANGE** (next to it) paints a random range instead: a new value on every hit. **Alt+drag** removes locks |
| Trigless step | Select steps, **TRIGLESS** button in the STEP tab: the step sends only its locks, no note, and changes a sound that is still ringing |
| Conditions | **CONDITION** field in the STEP tab or the step's right-click menu. Example: snare on 14-16 set to **FILL** = a roll only while **FILL** is on |
| Patterns | Click a pattern slot: while playing it switches at the next bar. Right-click = copy, paste, add to chain, fill pattern, clear / reset |
| Chain | **Shift+click** pattern slots or click **+** in the song row, then **CHAIN** on: each entry plays one bar |
| Song from regions | Name regions **P1 Verse**, **P2 Drop** … (P + 1-16 at the start), turn **REGIONS** on. Needs SYNC REAPER and the listener |
| Kit per pattern | **KIT** tab: **GRAB KIT** stores the panel sound in the current pattern |
| Starting grooves | **BEAT** tab: a whole groove from 28 styles · **GEN** tab: Euclid and randomize for one lane |
| Feel | **FEEL** tab: groove template per lane, **EVOLVE**, **AUTO FILL** · header: **SWING**, **CHAOS**, **DENSITY** |
| Clear / reset | **TOOLS** tab: top row keeps, bottom row removes. **CLEAR** keeps the settings, **RESET** = back to default. **NEW SESSION** empties all 16 patterns (asks first, no undo) |
| Tap record | **REC** button, then play the parts on MIDI channel 1-6. **CAL**: tap 8 beats and it learns your timing |
| Default value | Double-click a value box |

**Choke** (closed hat cuts open hat) is done in the volca itself: **FUNC + CHOKE** (step 8), then steps 1-6 switch it per part. The lowest part number wins.

### Duck trigger
The DUCK buttons (**ROUTE** tab) pick lanes that also send a trigger (C1 on MIDI channel 10). Select the tracks that should duck (bass, pads …) and run **Volca duck to selected tracks**: it adds a MIDI receive from the sequencer track (channel 10 > bus 2). Run it again on a track = receive removed. On the ducking track you need a plugin that ducks on MIDI notes, e.g. ShaperBox 3 (VST3): set its MIDI input to Bus 2 and turn on *Map REAPER MIDI buses to VST3 MIDI buses* in its pin menu.

## The panel

![The panel, Sleeve look](screenshot-sleeve.png)

![The panel, Classic look](screenshot.png)

| Action | How |
|---|---|
| Change a value | Drag or mouse wheel on the bar |
| Default value | Double-click or Alt+click the bar |
| Read a value | Layer rows show real units: dB, ms, Hz + note (`G#1`), sweep in st / ms. Measured on a volca drum, so roughly right; noise pitch, OSC / RND mod and the mix rows stay 0-127 |
| Exact value | Hover the bar, type 0-127 (the CC value), Enter |
| Select (SRC / MOD.T / EG.T) | Click a segment, drag, or mouse wheel. Each row changes only its own part of the Select CC |
| Select a part | Click its title (PART 01 … WAVEGUIDE) |
| Copy / paste a part, sound files | **SOUND** button, or right-click a part title |
| Save / load a kit | REAPER's preset menu at the top of the FX window, or the **Volca kit** actions |
| Send everything | **SEND ALL**. **AUTO SEND** (on by default) does it once after a project load |
| Randomize | In RANDOM pick the target (PART / L1 / L2 / KIT), a kind and the amount, press **ROLL**. **SMART** rolls a sound of that kind (KICK … MICRO) inside its useful ranges; **MIX** on KIT rolls a whole drum kit, on a part one random kind. Low amount stays close to the current sound. **WILD** rolls anything, full range. Locked cells are skipped. **UNDO** takes back the last roll, paste, kit load or morph (press again = redo) |
| Lock a cell / row / part | Right-click the bar / click the row name (right-click = all parts) / Shift+click the part title |
| Morph | **SET A**, change or load a kit, **SET B**, then move the MORPH bar |
| Test hit / pitch quantize | Play button / **Q** in the part header |
| Link layers | **LINK**: a change on one layer goes to the other layer too (also for sequencer p-locks) |
| Look / color | Small square (look: Sleeve or Classic, new instances start in Sleeve) and color swatch (click or wheel) at the top left. Same in the sequencer |

Locks and morph snapshots are saved with the project, not in presets. Sound files live in REAPER's resource folder under `Data/NH4X Volca/VolcaSounds` and are shared by all projects.

**Without the sequencer:** notes 65 / 67 / 69 / 71 / 72 / 74 on any channel play part 1-6, so one piano roll plays all parts. Notes on channel 11-16 go to part 1-6 unchanged, to play a part melodically (best with **Q** on).

## Good to know
- The volca has no MIDI out, so the panel only knows what it sent. If the volca was switched on late, press **SEND ALL**.
- For MIDI controllers: every control is a plugin parameter. Panel: Roll (slider 146) and Undo (147) act as buttons (send 1), Morph = slider 148. Sliders 160-195 = each Select row (SRC / MOD.T / EG.T) per part and layer as its own parameter.
- Use one sequencer + panel pair per REAPER session: they talk through shared memory that all open project tabs share.
- The panel uses CC 119 on MIDI channel 16 to talk to the sequencer and doesn't pass it on.
- Fonts of the Sleeve look: big numbers and titles use the free font **Big Shoulders Display** (Google Fonts) if it's installed, otherwise Bahnschrift Condensed. All other text uses Bahnschrift, which comes with Windows 10 / 11.
- Made and tested on Windows. macOS should work, but fonts will look different (not tested).

## Other DAWs
The **panel** should work in other DAWs through **ysfx** (free, loads JSFX as VST3 / AU / CLAP): https://github.com/JoepVanlier/ysfx/releases. Not tested by me. The **sequencer** and the actions need REAPER.

## Volca setup: split channel mode
The panel and the sequencer send every part on its own MIDI channel: part 1 on channel 1, part 2 on channel 2, up to part 6 on channel 6. That is the volca drum's factory default, so a new volca is already set up. If it was set to one channel for all parts, switch it back:

1. Switch the volca **off**.
2. Hold **REC** and switch it **on**. The 16 step buttons now stand for MIDI channels 1-16.
3. Look at the LEDs under the step buttons:
   - **One LED lit:** all parts listen on that one channel. Press **that step button**: the LED goes out and the volca is back to part 1-6 on channel 1-6.
   - **No LED lit:** it's already in split channel mode.
4. Switch the volca off and on again to play normally.

Source: Korg volca drum Owner's Manual, section *Setting the MIDI channel*: https://www.korg.com/us/support/download/product/0/809/

## Changes
- **Suite 1.3** (panel 2.6.1, sequencer 1.1.5): Sleeve look with two fonts: Big Shoulders Display for big numbers and titles, Bahnschrift SemiCondensed for all other text (easier to read). New instances start in Sleeve with the Sleeve red colors. Panel: each Select row (SRC / MOD.T / EG.T) is also its own parameter (sliders 160-195) for MIDI controllers and automation.
- **Suite 1.2** (panel 2.5, sequencer 1.1.4): panel: SMART roll (pick a kind: KICK, SNARE, CLAP, HAT, METAL, PERC, BASS, MICRO, MIX; rolls stay inside useful ranges, MIX on KIT = a drum kit; WILD = the old full-range roll), SOUND menu grouped by first word, Alt+click = default. Sequencer: right-click value lists (humanize, Euclid hits, GEN amount, intensity, accent, BPM, length strip, p-lock parameter), more Alt+click defaults, CAL right-click is a menu. Fix: Alt+click on a step sets the lane length only in STEPS.
- **Suite 1.1** (panel 2.1.3, sequencer 1.1.1): values in real units, measured on a volca drum: LEVEL in dB, ATTACK / RELEASE in ms, PITCH in Hz + nearest note and cents (sine / saw; Q on shows QPI), rise-fall MOD / RATE as sweep in semitones / ms. Same units on the sequencer's p-lock cells. Sleeve: Q and LINK stay visible when on in the selected part.
- **Suite 1.0.1** (sequencer 1.0.1): Fix: pitch locks only on lanes with PIT on (blocked and not sent on PIT-off lanes, PITCH tab not paintable there).
- **Suite 1.0** (panel 2.0, sequencer 1.0): first release of the sequencer and the helper actions. Repository renamed from volca-drum-panel. Panel: AUTO SEND on project load, sound files (save / load / rename / delete), kit actions and kit names, works with the sequencer (p-locks, kit per pattern, LINK for locks), undo for kit load and morph, fixes.
- Panel 1.5.2: Fix: switching Q off always brings the part back to its PITCH value.
- Panel 1.5.1: Classic look: part titles fit at any window size.
- Panel 1.5: Select split into SRC / MOD.T / EG.T rows. Two looks + 14 color themes, test hit and Q (QPI) per part, tooltips, notes on channel 11-16 play parts melodically. Install via ReaPack.
- Panel 1.0.1: Select is easier to set with the mouse.
- Panel 1.0: first release.

## License
**CC BY-NC-SA 4.0** (Creative Commons Attribution-NonCommercial-ShareAlike 4.0): https://creativecommons.org/licenses/by-nc-sa/4.0/

- **Free** to use, share and change, as long as it's not commercial.
- **Credit** NH4X and link to this repository.
- **Changed versions** you share must use the same license.
- **Your music is yours.** Music you make with these tools can be released and sold however you like. The license only covers the code.
- **Commercial use of the code** (selling it, bundling it in a paid product, building a paid product or service on it) needs a separate license from me. Open an issue on this repository and we'll talk.
