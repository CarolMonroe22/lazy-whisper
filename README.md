# lazy-whisper 🎙️

Hold your mouse's right button to dictate with [Wispr Flow](https://wisprflow.ai). Let go and it transcribes. A quick right-click still opens the normal context menu.

Your other hand never has to leave what it's doing. Peak laziness, fully intentional.

```
 quick right-click  (< 0.7s) ──► normal context menu
 hold right-click   (≥ 0.7s) ──► holds Left Control ──► Wispr listens 🎙️
                        release ──► Wispr transcribes
```

It's a single [Karabiner-Elements](https://karabiner-elements.pqrs.org) rule. It works with any dictation app that has a hold-to-talk shortcut, not only Wispr.

## What you need

- macOS
- An **external mouse**. Karabiner can't remap the built-in Apple trackpad's right-click.
- [Karabiner-Elements](https://karabiner-elements.pqrs.org) (free)
- Wispr Flow, or any app with a push-to-talk key

## Setup

### 1. Install Karabiner-Elements

Download it from [karabiner-elements.pqrs.org](https://karabiner-elements.pqrs.org), or:

```bash
brew install --cask karabiner-elements
```

> If you run `brew` from a place with no interactive terminal (like an AI agent), it fails because the installer needs your password. Open the `.pkg` manually instead.

### 2. Grant the permissions

Open Karabiner-Elements and follow its guide. There are three, and all of them matter:

| Where (System Settings) | Turn on |
|---|---|
| Privacy & Security → **Input Monitoring** | Karabiner-Core-Service, Karabiner-EventViewer |
| General → Login Items & Extensions → **Allow in the Background** | Karabiner-Elements Non-Privileged Agents v2, Privileged Daemons v2 |
| General → Login Items & Extensions → **Driver Extensions** (scroll down, click ⓘ) | Karabiner-DriverKit-VirtualHIDDevice |

The driver extension is the one people miss. Without it nothing happens. You can check it in Terminal:

```bash
systemextensionsctl list | grep pqrs
# should say: [activated enabled]
```

### 3. Import the rule

Copy the rule into Karabiner's folder:

```bash
mkdir -p ~/.config/karabiner/assets/complex_modifications
curl -L -o ~/.config/karabiner/assets/complex_modifications/lazy-whisper.json \
  https://raw.githubusercontent.com/CarolMonroe22/lazy-whisper/main/lazy-whisper.json
```

Then in Karabiner-Elements: **Complex Modifications → Add predefined rule →** "Lazy Whisper" → **Enable**.

### 4. Turn on your mouse

In Karabiner-Elements → **Devices**, turn on **Modify events** for your mouse. Karabiner leaves mice alone by default, so the rule does nothing until you do this.

### 5. Set Left Control as push-to-talk in Wispr

Wispr Flow → Settings → Shortcuts → **Push to talk**: add **Left Control** (you can keep `fn` too).

> Why Control and not `fn`? Karabiner simulates Control reliably. Sending `fn` from a virtual keyboard is hit or miss depending on the app.

## Try it

| Do this | You get |
|---|---|
| Quick right-click | normal context menu |
| Hold right-click about 1s, talk, let go | Wispr transcribes |

## Customize

**Timing.** Change both `700` values in the JSON (in milliseconds). Around 500 feels snappier, and around 1000 makes accidental triggers less likely. Keep both numbers equal.

**Different key.** If your dictation app uses another push-to-talk key, change `"left_control"` to that key. Karabiner's key names are in [its docs](https://karabiner-elements.pqrs.org/docs/json/complex-modifications-manipulator-definition/).

**Different button.** Change `"button2"` (right) to `"button3"` (middle) or `"button4"` / `"button5"` (side buttons). With a side button you can drop `to_if_alone` if you never use its original action.

## Troubleshooting

- **Nothing happens.** Check the driver extension (step 2) and **Modify events** on your mouse (step 4).
- **Right-click menu feels slow.** That's expected. The normal right-click fires when you *release* the button, not when you press it. Lower the timing if it bothers you.
- **Wispr doesn't start.** Make sure Left Control is set as push-to-talk in Wispr (step 5).
- **Logs:** `~/.local/share/karabiner/log/`

## Credits

Made by [Carol Monroe](https://carolmonroe.com). Built with [Karabiner-Elements](https://github.com/pqrs-org/Karabiner-Elements) by Fumihiko Takayama. Not affiliated with Wispr.

## License

MIT
