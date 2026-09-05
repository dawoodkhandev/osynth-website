# Osynth — marketing site

Single-page marketing site for Osynth. Live at **https://osynth.vercel.app**

## Running it

No build step, no dependencies. Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 4173
```

Keep `index.html` and `Media/` together — the page loads all video and imagery by relative path.

## Structure

| Path | What it is |
|---|---|
| `index.html` | The entire site: markup, CSS and JS in one file |
| `Media/` | Source videos (7 clips) |
| `Media/posters/` | Poster frame per video, generated so the page doesn't load 19MB up front |
| `Media/avatars/` | Face crops used for testimonial and proof-chip imagery |
| `vercel.json` | Cache headers: one year immutable on `/Media`, revalidate on the page |

## Sections

Hero (orbiting video wheel) → platform strip → stats → how it works → guarantee →
video wall → spotlight → testimonials → backed by → community → CTA → footer.

## Implementation notes

- Fonts load from Google Fonts, so the page needs a network connection for its
  intended typography. It falls back to system fonts offline.
- The video wheel and the three process illustrations are scroll and time
  driven. Both respect `prefers-reduced-motion`.
- Wheel speed is a single constant: `SPIN`, in degrees per second.
- Video metadata (platform, duration, view counts) lives in the `CLIPS` array
  near the top of the `<script>`. Durations are measured from the source files.
- Per-frame work in the wheel is limited to `transform` and `opacity` so it stays
  on the compositor. Anything that repaints is written only when its value changes.

## Before launch

- [ ] Replace testimonial names, roles, companies, quotes and photos with real
      customers. Current entries are placeholder copy, marked with TODOs in the source.
- [ ] Verify the Y Combinator and a16z speedrun references.
- [ ] Review the "Viral videos, guaranteed" claim.
- [ ] Move the waitlist from a personal address to a form or a role account,
      so it is not scraped.
- [ ] Add client logos to the platform strip once usage rights are confirmed.
