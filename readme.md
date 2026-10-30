# Restyle themes

Custom CSS themes for the Restyle Chrome extension.

## Themes

| Name             | Sites            | Notes                                    |
| ---------------- | ---------------- | ---------------------------------------- |
| Wikipedia-OneSee | wikipedia.org    | Neutral dark theme, `#1c1c1c` background |
| Gmail-OneSee     | mail.google.com  | Neutral dark theme, `#1c1c1c` background |
| Amazon-OneSee    | amazon.com       | Neutral dark theme, `#1c1c1c` background |
| SketchUp-OneSee  | app.sketchup.com | Neutral dark theme, `#1c1c1c` background |

## How it works

The extension reads [themes.json](themes.json) from this repo and downloads each stylesheet listed in it.
Point the extension's settings at the repo's GitHub URL (for example `https://github.com/<you>/restyle-themes`).
The repo has to be public.

## Adding a theme

1. Add a stylesheet under `themes/`, e.g. `themes/youtube-dark.css`.
2. Add an entry to `themes.json`:

   ```json
   {
     "name": "YouTube-Dark",
     "description": "Dark theme for YouTube",
     "matches": ["*://*.youtube.com/*"],
     "css": "themes/youtube-dark.css"
   }
   ```

3. Push, then press **Sync** in the extension (it also re-syncs every 6 hours).

Field notes:

- `name` must be unique. It's also how the extension remembers whether you turned a theme off.
- `matches` takes [Chrome match patterns](https://developer.chrome.com/docs/extensions/develop/concepts/match-patterns),
  or a bare domain such as `"youtube.com"` (that domain plus all its subdomains).
- `css` is a path relative to `themes.json`.

## Writing themes

The stylesheet is added at the end of the page, so it wins ties with the site's own CSS, but sites
often use inline styles or very specific selectors. Use `!important` freely.

If the site uses CSS variables for its colors (Wikipedia does), overriding those on `:root` gets you
most of the way. [wikipedia-onesee.css](themes/wikipedia-onesee.css) is a worked example.
