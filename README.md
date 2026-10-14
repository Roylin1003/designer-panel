*A collaborative project by roylin1003 and Claude.*

# designer-panel

**Turn any `CONFIG` object into live sliders — tune your web game while it runs, then paste the changes back.**
One file, one function: `initDesignerPanel(CONFIG)`. Every number becomes a knob (number box + slider), every boolean a checkbox. Change one and the game reacts on the next frame.

Zero dependencies. No build step.

It holds the tuning knobs for dozens of games in the **[Protonia](https://roynexus.com)** game lab — try it in the playable demo here first.

## Try it

```bash
python -m http.server 8000
# open http://localhost:8000/demo.html — catch the falling stars, press F2 (or tap ⚙) and drag the sliders
```

On localhost the panel is on by default. On a public host, add `?design=1`.

## Use

```html
<script src="config.js"></script>        <!-- const CONFIG = { player: { speed: 4 }, ... } -->
<script src="designer-panel.js"></script>
<script>
  initDesignerPanel(CONFIG, {
    labels:   { player: 'Player', speed: 'Move speed' },   // optional names next to the keys
    ranges:   { 'player.speed': [0, 10, 0.1] },             // optional slider range
    onChange: () => resize(),                               // after every change
    theme:    { bg: 'rgba(10,8,6,.97)', accent: '#E8C36A' } // match your game's colors
  });
</script>
```

The one rule: **read `CONFIG.x.y` every time you use it.** Copy it into a `const` at start-up and the knob is disconnected.

## What you get

- **Net diff, ready to paste.** The bottom box shows only what differs from the file values, as valid JS: `CONFIG.star.gravity = 0.08;   // 原本 0.04` ("原本" = "was"). Copy it into `config.js`, or into a chat with whoever edits the file.
- **Reset** one knob (↺) or all.
- **Filter** by key path or label.
- **Players don't get it.** Local: on. Public: off unless `?design=1`. `?design=0` shows what players see. No memory in localStorage, so one visit can't leave it switched on.
- **Measuring guides** laid over the whole screen: red lines (percent of the window), gold boxes (x, y, width, height), text samples (size, color, font). Click a reading to copy it.
- **Touch:** a draggable ⚙ handle for phones without F2.

The panel element is returned, so a game can `appendChild` its own extra sections.

Comments in `designer-panel.js` and the panel's interface text are in Traditional Chinese. Option details are in the header comment.

## About this project

Directed by Yen-Ting R. Lin. The code was written mostly by AI (Anthropic Claude) under his direction, then tested and reviewed by hand.

## License

Code: [MIT](LICENSE). See [CREDITS](CREDITS.md).
