# OLDs Cyber

A dark cyberpunk theme for [Omarchy](https://omarchy.org). Black ground,
magenta accent, periwinkle bar and borders.

![OLDs Cyber](backgrounds/olds-cyber-1-4k@.jpg)

## Palette

| Role | Hex |
| --- | --- |
| Background | `#000000` |
| Surface / panel | `#1e1e2a` |
| Muted text | `#4a4a5a` |
| Foreground | `#e8e8f0` |
| Accent (magenta) | `#E43995` |
| Bar and borders (purple) | `#6c7fe0` |
| Secondary (cyan) | `#4ad9e0` |

The magenta is the anchor: it marks selection, hover, focus, active
indicators and the window border gradient. The purple carries structure,
the bar icons and every surface border, so the two never compete.

## Install

```
omarchy theme install https://github.com/USERNAME/omarchy-olds-cyber
```

Then pick **OLDs Cyber** from the theme menu, or:

```
omarchy theme set "OLDs Cyber"
```

## What it covers

Hyprland borders and hyprlock, the Omarchy shell (bar, menus, popups,
notifications, launcher, polkit and lock), btop, GTK 3 and 4, Qt via qt6ct,
mako, walker, swayosd, superfile, cava, chromium and Zen.

Terminal colours come from `colors.toml`. The `alacritty.toml`,
`ghostty.conf` and `kitty.conf` files are included for local use but are
stripped by Omarchy when a theme is installed from a git repo, which is
expected and loses nothing.

### Shell section overrides

Rather than shipping a whole `shell.toml`, this theme ships three section
overrides so it keeps inheriting upstream template improvements:

- `shell.bar.toml` sets the bar's idle icon colour and the attention colour
  used by recording, muted mic, do-not-disturb and pending updates.
- `shell.hyprland.toml` sets the two shared border tokens, which every
  surface references.
- `shell.controls.toml` sets the normal, hover, focus and selected states.

## Optional extras

These are **not** part of the theme. Omarchy themes carry colour files, not
QML, so the following need edits to cloned plugins. Each survives theme
switches and needs redoing after a plugin re-clone.

### Magenta calendar hero

Clone the clock, then edit `Panel.qml`:

```
omarchy-plugin-clone omarchy.clock
```

In `~/.config/omarchy/plugins/<user>.clock/Panel.qml`, the hero date and its
glyph use `root.contentForeground`. Change both to `Color.accent`:

```qml
color: heroMouse.containsMouse
  ? Qt.lighter(Color.accent, 1.25)
  : Color.accent
```

For the ring around today, replace

```qml
border.color: Style.normalBorderFor(root.contentForeground, Color.accent)
```

with `border.color: Color.accent`.

### Magenta weather hero

```
omarchy-plugin-clone omarchy.weather
```

In `<user>.weather/Panel.qml`, set `color: Color.accent` on the condition
glyph (`id: heroIcon`), the temperature (`id: tempBig`), its unit, and the
map-marker and location lines if you want those too.

> The map-marker glyph is a Nerd Font private-use character. Edit that colour
> line in place rather than retyping the glyph line, or the icon is lost.

### A note on cloned plugins

Cloning forks a plugin, so upstream fixes no longer reach it. That matters
more for the weather plugin, which talks to an external API, than for the
clock.

Apply changes with `omarchy-restart-shell`, not `omarchy theme set`.

## Credits

Wallpaper generated from the theme palette. Everything here is original.

## License

MIT. See [LICENSE](LICENSE).
