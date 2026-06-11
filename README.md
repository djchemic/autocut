# Autocut — Install

## What's in this package

- `autocut.py` — launcher + state machine + HTTP/SSE server
- `dashboard.html` — browser UI (served at http://localhost)
- `atem-levels.js` — Node helper that talks to the ATEM
- `install.sh` — one-shot build script (produces `Autocut.app`)
- `package.sh` — bundles `.app` + Node binary into a distributable zip
- `favicon.png` — the AC by @djchemic icon

## First install

Drop all files into one folder, e.g. `~/Downloads/Files`, then:

```
cd ~/Downloads/Files
bash install.sh
```

The script installs `python@3.12`, `node`, `pyinstaller`, `zeroconf`, and
`atem-connection` (via npm), then builds `Autocut.app` and opens it.
First run takes 1-2 minutes; subsequent rebuilds are faster.

## Rebuild after changes

Same command. The script wipes the iconset and Launch Services cache so
icon and dashboard changes always take effect:

```
bash install.sh
```

If the Mac app icon doesn't refresh in Finder, the script flushes
`lsregister` and restarts Dock + Finder automatically — you'll see them
flash for a moment.

## Distribute to another Mac (Apple Silicon)

After `install.sh` builds the app:

```
bash package.sh
```

Produces `Autocut-Mac-AppleSilicon.zip` (~80 MB). Recipient unzips, drags
`Autocut.app` to `/Applications`, right-clicks → **Open** the first time
to bypass Gatekeeper. Or strip the quarantine attribute:

```
xattr -dr com.apple.quarantine /Applications/Autocut.app
```

## Config & recovery

Settings live at:

```
~/Library/Application Support/Autocut/config.json
```

A `.bak` is written on every save. If a rebuild ever scrambles your
config:

```
cd ~/Library/Application\ Support/Autocut
cp config.json.bak config.json
```
## Routing to Atem Mini Pro Iso/or other models
- use the Mic1 and Mic2 input at the back
- For Mic1 i choosed host and for Mic2 guest(s)
- I have routed from RodeCaster Pro II 3.5mm jacks via "Custom mix"
- Rodecaster Pro II lets you select which channel goes where by "Routing"
- Dont forget to set Atem Mini inputs to Line not to microphone input.


## Default working values

- Mic 1 input: 1301, gate -37 dB, attack 500 ms, release 450 ms
- Mic 2 input: 1302, gate -37.5 dB, attack 400 ms, release 450 ms
- Both Gate: -41 dB, Both Release: 1900 ms
- Both Overlap: 2800 ms, Min Hold: 600 ms
- Cam mapping: BOTH=1, SOLO_1=2, SOLO_2=3

## Recovery to v1.1.1 baseline

If a later change breaks something, `autocut-v1.1.1-source.zip`
(shipped separately) is the saved working snapshot — unzip over your
files and rebuild.
