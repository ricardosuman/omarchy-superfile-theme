# omarchy superfile theme

makes [superfile](https://github.com/yorukot/superfile) follow the current omarchy theme.

omarchy renders every `*.tpl` in `~/.config/omarchy/themed/` into the active theme
directory whenever you switch themes. this is one of those templates, plus a symlink
so superfile finds the result.

## install

```sh
curl -fsSL -o ~/.config/omarchy/themed/superfile.toml.tpl \
  https://raw.githubusercontent.com/ricardosuman/omarchy-superfile-theme/main/superfile.toml.tpl

ln -sf ~/.local/state/omarchy/current/theme/superfile.toml \
  ~/.config/superfile/theme/omarchy.toml
```

then set `theme = "omarchy"` in `~/.config/superfile/config.toml`, and switch themes
once to render the file. until you switch, the symlink points at nothing.

`-f` matters: without it curl writes the 404 body into the template and exits 0.

## notes

- superfile reads the theme at startup, so reopen `spf` after switching themes.
- `code_syntax_highlight` is pinned to `monokai`. the template engine has no
  conditionals, so it can't pick a light style on light themes.
- works with both `colors.toml` dialects (semantic keys and base16 `color0..15`).
  tested against the 22 built-in omarchy themes.
- custom themes must define `accent` in their `colors.toml`. it is the one key
  omarchy's resolver has no fallback for, so without it you get a literal
  `{{ accent }}` in the output.
