# Valmo — pre-launch site

Static teaser for Valmo Light Co. (legal: Valmo Oy, founding in progress) — a Finnish light-therapy and healthy-lighting company. 
Purpose: establish the brand's visual identity, collect waitlist emails, tease an October launch. Nothing else. Resist scope growth.

## Stack & deployment
- Plain HTML + CSS. No frameworks, no build step, no npm, no JS unless a component strictly needs it.
- Hosted on GitHub Pages. Custom domain: `virvalight.com` (via `CNAME` file) — temporary,
  since the intended domain `valmolight.fi` isn't available yet due to domain issues; swap
  the `CNAME` file and update absolute URLs (MailerLite redirect) once `.fi` is secured.
  ALL asset paths relative (`./style.css`, `./assets/…`) — never root-absolute. This must
  survive future domain changes unchanged.
- Local preview: `python3 -m http.server` in repo root. Test at 375 px width first.
- Files: `index.html`, `style.css`, `/assets/` (SVG + images). One page. New pages only if asked.

## Design tokens
All values live in one `:root` block; never
hardcode a color/size elsewhere.

```css
:root {
  --black: #0c0b0a;   /* page background — near-black, warm */
  --ink:   #f2ede1;   /* primary text — warm white, never #fff */
  --dim:   #8a8478;   /* secondary text */
  --faint: #5c574e;   /* tertiary, captions */
  --rule:  #262420;   /* hairline borders */
  --red:   #b5442f;   /* 660 nm accent — the ONLY non-neutral on the site */
  --font-display: 'Michroma', sans-serif;      /* wordmark, headings, model names */
  --font-mono: 'IBM Plex Mono', monospace;     /* data, serials, spec lines, footer */
  --font-prose: 'Barlow', sans-serif;          /* body copy */
}
```

- Red is rationed: the period in "VALMO LIGHT CO." lockup, at most one or two other
  points per viewport. If red appears in a third place, remove one.
- Google Fonts: Michroma 400; IBM Plex Mono 400/500; Barlow 400/500/600.
  `preconnect` + `display=swap`.

## Typography rules
- Michroma is a stand-in for licensed Eurostile Next; the final wordmark will be replaced
  by an outlined-path SVG. Build the lockup so the swap is one file change.
- White-on-black halation: prefer regular/medium weights; go one step lighter than
  what looks right, especially below 16 px.
- Display and lockup lines: uppercase via CSS `text-transform`, letter-spacing 0.07–0.22 em
  (wider as size shrinks). Body prose: sentence case, normal tracking, 16–18 px, line-height ≥ 1.6.
- Numbers styled like calibration values: mono font, `660 · 850 nm`, `370 €`, `No. 001`.
  No charm pricing ever (no ,99).

## Page structure (in order)
1. Lockup: VALMO (display, large) over VALMO LIGHT CO. (small, tracked, red period on "CO.")
2. Creed (approved copy below, ~5 lines, prose font, generous whitespace)
3. Spec tease line (mono): `Erä 001 — kolme laitetta — lokakuu 2026`
4. Email capture (see below)
5. Footer: left `mitattu, ei väitetty` · right `Valmo Light Co. · Suomi · No. 001`
Emblem (Brocken spectre: rough silhouette in precise glory rings) arrives later as SVG;
leave a commented slot above the lockup, don't improvise one.

## Approved copy — do not invent alternatives, ask instead
Finnish is the primary and only v1 language (`lang="fi"`). Hand-written EN version is
Phase 1.1 (`/en/`), never machine-translated.

Creed (draft v1, Artturi approves final):
> Aurinko on kaiken elämän lähde. Ihmiskeho on rakennettu elämään sen valossa.
> Kuitenkin nykyään vietämme paljon aikaa sisätiloissa. Valmo suunnittelee ja valmistaa valaisimia
> ja valohoitolaitteita, jotka tuovat ulkotilan ominaisuudet sisälle.
> Ei lupauksia vaan dataa.

## Copy tone — hard rules
- Declarative sentences. No exclamation marks, no emoji, no superlatives
  ("paras", "mullistava", "vallankumouksellinen" kielletty).
- Physics vocabulary allowed: aallonpituus, spektri, irradianssi, välkyntä, K, nm, mW/cm².
- Medical-claim verbs BANNED in any language: hoitaa, parantaa, lievittää, ehkäisee,
  treats, heals, cures, relieves. We publish measurements, not promises. This is a legal
  constraint (EU wellness-device rules), not a style preference.
- No wellness clichés: "hehkuva iho", "palauttava", "holistinen" — out.

## Email capture
- Maillite embedded form, double opt-in ON. Style the embed with our tokens
- No cookies, no analytics, no tracking scripts → no cookie banner. Keep it that way.
  If analytics are ever requested: privacy-first (e.g. GoatCounter), still no banner.
- A one-paragraph tietosuoja note at `#tietosuoja`, linked from the consent line.

## Workflow
- One change at a time; show the diff before any restructure.
- Never modify `:root` tokens or approved copy without asking.
- No new dependencies, pages, or sections without asking.
- Performance budget: page < 100 KB excluding fonts; no images above 150 KB; SVG preferred.
- Accessibility: semantic landmarks, visible focus states, contrast is already ≥ AAA on
  these tokens — keep it so; `prefers-reduced-motion` respected if any animation is added.