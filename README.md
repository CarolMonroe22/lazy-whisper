<div align="center">

# lazy-whisper 🎙️

**Hold right-click. Talk. Let go. Done.**

Dictate with [Wispr Flow](https://wisprflow.ai) without ever reaching for the keyboard.<br>
One hand on the mouse, the other holding your coffee.

![macOS](https://img.shields.io/badge/macOS-000000?logo=apple&logoColor=white)
![Karabiner-Elements](https://img.shields.io/badge/Karabiner--Elements-rule-5A45FF)
![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Laziness](https://img.shields.io/badge/laziness-extreme-ff69b4)

</div>

---

## The idea

Push-to-talk dictation is magic. Except you still need a hand on the keyboard to hold `fn`.

**lazy-whisper** moves push-to-talk to your mouse's right button:

```
 quick right-click  (< 0.7s) ──► normal context menu, nothing changes
 hold right-click   (≥ 0.7s) ──► 🎙️ Wispr starts listening
                        let go ──► ✨ your words appear
```

No app to install beyond one free, open-source tool. No background daemon of ours. It's **one Karabiner-Elements rule**, about 20 lines of JSON you can read in 10 seconds.

Works with Wispr Flow, or **any dictation app with a hold-to-talk key**.

## ⚡ Install in 3 minutes

**You need:** macOS · an external mouse · [Karabiner-Elements](https://karabiner-elements.pqrs.org) (free)

> 🖱️ Apple's built-in trackpad won't work. Karabiner can't remap its right-click, so you need a real mouse.

### 1 · Install Karabiner-Elements

```bash
brew install --cask karabiner-elements
```

Or download it from [karabiner-elements.pqrs.org](https://karabiner-elements.pqrs.org).

### 2 · Grant the three permissions

Open Karabiner-Elements and follow its guide. **All three matter:**

| System Settings | Turn on |
|---|---|
| Privacy & Security → **Input Monitoring** | Karabiner-Core-Service, Karabiner-EventViewer |
| General → Login Items & Extensions → **Allow in the Background** | Karabiner-Elements Agents v2 + Daemons v2 |
| General → Login Items & Extensions → **Driver Extensions** ⓘ | Karabiner-DriverKit-VirtualHIDDevice |

> 👀 **The Driver Extension is the one everyone misses.** Scroll to the bottom of that page. Without it, nothing happens. Check it with:
> ```bash
> systemextensionsctl list | grep pqrs   # → [activated enabled]
> ```

### 3 · Add the rule

```bash
mkdir -p ~/.config/karabiner/assets/complex_modifications
curl -L -o ~/.config/karabiner/assets/complex_modifications/lazy-whisper.json \
  https://raw.githubusercontent.com/CarolMonroe22/lazy-whisper/main/lazy-whisper.json
```

Karabiner-Elements → **Complex Modifications → Add predefined rule →** "Lazy Whisper" → **Enable**.

### 4 · Let Karabiner see your mouse

Karabiner-Elements → **Devices** → turn on **Modify events** for your mouse. Mice are ignored by default.

### 5 · Tell Wispr about Left Control

Wispr Flow → Settings → Shortcuts → **Push to talk** → add **Left Control**. You can keep `fn` too.

> Why Control and not `fn`? Karabiner simulates Control reliably. A virtual `fn` is hit or miss.

### 🎉 Try it

Open any text box, hold right-click, say something, and let go.

## 🎛️ Make it yours

It's plain JSON, so tweak away:

| Want | Change |
|---|---|
| Faster or slower trigger | both `700` values (ms). `500` feels snappy, `1000` is safer |
| A different dictation app | `"left_control"` → that app's hold-to-talk key ([key names](https://karabiner-elements.pqrs.org/docs/json/complex-modifications-manipulator-definition/)) |
| Middle or side button instead | `"button2"` → `"button3"` (middle), `"button4"` / `"button5"` (side) |

## 🩺 Troubleshooting

| Symptom | Fix |
|---|---|
| Nothing happens | Driver Extension (step 2) + **Modify events** on your mouse (step 4) |
| Right-click menu feels a beat late | Expected: a short click now fires on *release*. Lower the timing if it bugs you |
| Wispr doesn't start listening | Left Control isn't set as push-to-talk in Wispr (step 5) |
| Still stuck | Logs live in `~/.local/share/karabiner/log/` |

## 💜 Credits

Built by [Carol Monroe](https://carolmonroe.com), who didn't want to move her other hand.

Powered by [Karabiner-Elements](https://github.com/pqrs-org/Karabiner-Elements), the brilliant open-source work of Fumihiko Takayama. Not affiliated with Wispr.

PRs welcome: new variants, other dictation apps, better defaults. Keep it lazy.

## License

[MIT](LICENSE). Take it, remix it, be lazy with it.
