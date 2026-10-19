# Köch Audio

Site of Köch Audio, the Bishkek distributor that puts Iradi music on the streaming platforms (Irad ARG; lore in
`mjsbroadbent/irad_persona_skill`, see the Köch Audio line in `canon.md`). The site itself is fully in-world.

Domain: **kochaudio.online** (`CNAME`). Contact addresses on the site: `info@` and `artists@kochaudio.online`.
DNS: apex A records 185.199.108.153, .109.153, .110.153, .111.153 (AAAA 2606:50c0:8000::153, 8001::153, 8002::153,
8003::153) and `www` CNAME to `mjsbroadbent.github.io`.

## Structure

No build step; GitHub Pages deploys from `main`, root.

- `index.html` all five pages as sections, switched by the hash: `#/`, `#/catalogue`, `#/live`, `#/artists`, `#/about`.
- `data.js` the catalogue (`releases`) and concert dates (`gigs`), plus the e-mail domain.
- `i18n.js` interface text in English, Iradi (`ir`, Kyrgyz-based Latin) and Russian. Same keys in every block.
- `app.js` rendering, language switch (remembered in `localStorage` `koch_lang`; `?lang=ru` also works), ticket dialog.
- `styles.css` all styling (fonts: Unbounded, Golos Text).

## Adding a gig

Add an object to `gigs` in `data.js`:

```js
{ id: "tt-almaty-1117", date: "2026-11-17", time: "20:00", artist: "tüntolk", city: "almaty", country: "kz",
  venue: "Zhylu Club", kind: "abroad", status: "onsale", price: "9,000 ₸", noteKey: "gJolchu26" }
```

- `kind`: `abroad` (tickets through Sahna Bilet; `status` `onsale` or `soon`, the button opens a dialog, no outside link)
  or `home` (ISEZ; `status` `door` or `free`; `tulpar: true` shows "Tulpar Pay accepted", otherwise "Cash at the door";
  every home date shows the municipal-permit note, `permit: "pending"` the "permit requested" version).
- `city` / `country` are keys in the `cities` / `countries` blocks of each language in `i18n.js`; add new ones there in
  all three languages. Irad venues use `country: "irad"`.
- `noteKey` (optional) points at a `gnotes` entry in each language.
- Dates before today (Bishkek time) move to "Past shows" by themselves. Past entries need only date, artist, city,
  country, venue, kind.
- Keep to the canon: avoid home dates on All Souls' (2 Nov), the Ninevite fast and the Great Fast; from 1 Jan 2027
  Tulpar Pay settles only in Tulparcoin, so 2027 home venues are cash.

## Adding a release

Add to `releases` (canon releases only); `p` is the ℗ year, `label` the label of record, `noteKey` an optional
`notes` entry in `i18n.js`. The ℗ line is built as "℗ <p> <label> under exclusive licence to Köch Audio".
Optional `links` maps a platform name from `platforms` to the real album URL (only for releases that are really up);
those platforms show as links, the rest as plain text. Jolchu has Spotify, Apple Music and YouTube Music (Yandex
Music couldn't be checked from outside its region; the album is also on Amazon Music and TIDAL).
