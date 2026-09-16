# The Great GIFs Museum

A wall of random GIFs, pulled live from six different corners of the internet.
No text, no chrome, no navigation — just tiles, endless scroll, and a reset button.

**[Live demo →](https://fanxy13.github.io/The-Great-Gifs-Museum/)**

## What it does

- Loads 20 GIFs at a time, five per row, and keeps going as you scroll.
- Pulls from six independent sources and deals them out round-robin, so two
  neighbouring tiles never come from the same place.
- Click a tile for the full, uncropped GIF. The red button downloads it.
- The reset button wipes the wall and starts over with a fresh random draw.

## Sources

| Source | What you get |
| --- | --- |
| Reddit | Meme and reaction GIFs, including Giphy- and Imgur-hosted ones |
| Bluesky | GIFs posted as link embeds — mostly Tenor and Giphy |
| Wikimedia Commons | Scientific animations, diagrams, historical material |
| Internet Archive | Whatever people uploaded and forgot about |
| GifCities | GeoCities GIFs, rescued from the 90s web |
| Openverse | Openly licensed images from Flickr, museums and others |

None of them need an API key or an account. Sources that stop responding are
dropped silently and retried a minute later, so the wall keeps filling even
when two or three of them are down.

## Run it

Any static host works. There is no build step and no dependency — it is one
HTML file.

```bash
git clone https://github.com/Fanxy13/The-Great-Gifs-Museum.git
cd The-Great-Gifs-Museum
python3 -m http.server 8000   # then open http://localhost:8000
```

Opening `index.html` straight from disk works too, but serve it over HTTP if
you can — some sources behave better with a real origin.

## Deploy to GitHub Pages

1. Create a repository named `The-Great-Gifs-Museum` and push these files to `main`.
2. Repository → **Settings** → **Pages**.
3. Source: **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. Give it a minute, then open `https://fanxy13.github.io/The-Great-Gifs-Museum/`.

## Notes

- Every GIF is loaded straight from its origin host and belongs to whoever made
  it. Nothing is cached, copied or re-hosted here.
- Content is unfiltered beyond each API's own safe-content flags. It is random
  internet, so the occasional oddity gets through.
- Some sources rate-limit by IP. If the wall runs dry, wait a minute or hit reset.
- Browser console shows what each source returned, useful when something stops
  working.

## Tech

Single HTML file. Vanilla JS, no framework, no bundler. CSS grid for the wall,
IntersectionObserver plus a scroll check for the endless loading, JSONP as a
fallback where CORS blocks a plain `fetch`.

## Licence

MIT — see [LICENSE](LICENSE). Applies to the code, not to the GIFs it displays.
