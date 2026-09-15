# Curated Addons & Advanced Setup

> The goal is **coverage without clutter**. Start with the core profile, then add something only when it solves a real gap.

[← Back to README](README.md) · [Stremio setup](STREMIO.md) · [Nuvio setup](NUVIO.md)

---

## Recommended core profile

### 1. AIOStreams — stream layer

Use **one AIOStreams install** as the main stream layer and let it combine your sources.

My lean source set:

| Source | Why keep it |
|---|---|
| **StremThru Torz** | Broad general coverage and repeatedly recommended by the community |
| **Comet** | Useful independent source; can find releases other sources miss |
| **Meteor** | Fast additional coverage and useful as a backup source |
| **MediaFusion** | Broad coverage; worth keeping in the pool even if another source usually wins |

This combination shows up repeatedly in 2026 community setups because the sources overlap enough for resilience without turning the result list into noise.

### 2. AIOMetadata — metadata / catalogs

Use **AIOMetadata** when you want richer control over posters, metadata, search and catalogs.

It can combine providers such as TMDB, TheTVDB and anime-focused metadata. Nuvio's community documentation recommends it as the primary metadata addon and notes that your own provider API keys can help avoid shared rate limits.

For Nuvio, keep metadata addons **above stream addons** in the addon order. Nuvio processes metadata priority from top to bottom.

Nuvio also has **TMDB Enrichment**, so you do not need to stack several metadata addons just because they exist.

### 3. Stremio Community Subtitles — subtitle layer

My first subtitle addon choice is **Stremio Community Subtitles**.

It can search multiple providers, including OpenSubtitles, SubDL and Subsource, and its release-matching approach is useful when different encodes/cuts need different subtitle timing.

If it does not cover your language/content well, add **one** backup rather than five:

- SubSource
- SubDL
- OpenSubtitles PRO
- SubSense

---

# Source profiles

## Lean — recommended for most people

```text
StremThru Torz
Comet
Meteor
MediaFusion
```

Use this first. If everything you watch is covered, stop here.

## Wider coverage

Start with Lean, then optionally add:

- **Torrentio** — still useful as an additional source when available, but I would not make the entire setup depend on it.
- **Sootio** — optional secondary source.
- **PenguPlay / HDHub** — optional HTTP fallbacks where your chosen AIOStreams instance supports them.

Public addon availability changes. Do not treat any single public source as permanent infrastructure.

## Anime-focused

Keep the normal Lean profile and add only the anime-specific sources you actually use:

- **SeaDex** — built into AIOStreams; useful for curated anime release data.
- **AnimeTosho** — available through the AIOStreams ecosystem.
- **Meteor** — already part of the Lean profile and often useful for anime as well.

If anime is a major part of your library, pair this with anime-aware metadata in AIOMetadata instead of adding several separate catalog addons.

---

# The most important rule: avoid duplicates

AIOStreams is already an aggregator.

If you put Comet, Meteor and MediaFusion **inside AIOStreams**, then also install all three standalone in Stremio/Nuvio, you will usually get duplicate results and a messier UI.

My rule:

> **AIOStreams is the normal path. Standalone addons are diagnostics or emergency fallbacks.**

A standalone copy is useful when you want to answer a specific question such as:

- Is AIOStreams slow, or is Comet itself slow?
- Is my public AIOStreams instance filtering a stream type?
- Is one wrapped source broken while its standalone instance still works?

Once the test is over, remove the duplicate unless it gives you a real benefit.

---

# AIOStreams tuning that is actually worth doing

AIOStreams can filter, deduplicate, sort and format results. That is more useful than simply enabling more sources.

## 1. Prefer usable results first

For a debrid-managed setup, prioritise cached/debrid-ready results over sources that still require extra work.

For **Nuvio native TorBox**, this is different: AIOStreams must return raw/P2P information so Nuvio can hand the hash to its own TorBox resolver. See [NUVIO.md](NUVIO.md).

## 2. Match the device, not a benchmark

Set preferences around what your actual playback device supports:

- maximum useful resolution;
- HDR / Dolby Vision capability;
- audio codec / channel support;
- preferred audio language;
- a sensible file-size ceiling for the connection and device.

A 4K result is not "better" if the TV/player cannot decode its video or audio format smoothly.

## 3. Filter obvious unwanted formats

If you never use them, filtering things such as 3D or unsupported visual/audio formats makes the source list easier to scan.

Do not copy aggressive filters from another person's setup without understanding them — they can silently remove the only usable source for an older or niche title.

## 4. Use deduplication

Multiple scrapers often discover the same underlying file. Let AIOStreams deduplicate equivalent results instead of presenting the same release several times.

## 5. Make the stream name useful

AIOStreams supports custom formatting. A useful result line should make the important information obvious at a glance:

```text
Resolution · HDR/DV · codec · audio · size · source/service
```

Do not cram every parsed property into the title. The point is faster selection, not a wall of diagnostics.

---

# Public instance strategy

## Midnight

This is **my preferred public instance** for this guide, particularly when I need a workflow that is not compatible with ElfHosted's public-instance restrictions.

Use Stable first; Nightly is for newer features/fixes.

## Yeb's

AIOStreams' current official setup documentation recommends **Yeb's** as the general starting point for most users. It is a good alternative if you do not specifically need Midnight.

## ElfHosted public

ElfHosted is professionally hosted and the AIOStreams docs describe it as a stable option, but its **public** instance excludes:

- P2P
- HTTP
- Live

That matters for Nuvio's native-debrid P2P workflow and for anyone relying on HTTP sources. It does **not** mean ElfHosted is generally bad.

## Self-hosting

If you want maximum control, predictable limits and less dependence on community-host policy, self-host AIOStreams with Docker on your own server/NAS/VPS.

Official deployment docs:

https://docs.aiostreams.viren070.me/deployment/

Self-hosting is an advanced option, not a requirement for a good setup.

---

# Credentials & privacy

A public AIOStreams instance can require credentials for services you connect through it. Treat that instance as a service you are choosing to trust.

If that trust model bothers you:

- self-host AIOStreams; or
- on Nuvio, use a native supported debrid integration where possible and leave the scraper addon in raw/P2P mode.

Never publish your debrid API key, configured private manifest URL, or exported config containing secrets in a GitHub issue/screenshot.

---

# What Reddit/community discussion changed in this guide

I did **not** copy a giant "best addons" list. I looked for names and patterns that repeated across recent 2026 discussions.

The strongest recurring themes were:

- AIOStreams is preferred by many users because it centralises filtering/sorting instead of installing many standalone addons.
- **StremThru Torz + Comet + Meteor** repeatedly appear in lean setups; MediaFusion is a common fourth source.
- Torrentio is still used, but many users now keep alternatives because public availability/reliability changes.
- Subtitle-heavy users repeatedly recommend **Stremio Community Subtitles** or a small number of provider-specific backups.
- More addons are not automatically better.

Community threads used as a signal (not as authoritative documentation):

- https://www.reddit.com/r/StremioAddons/comments/1vq867l/best_addons_august_2026/
- https://www.reddit.com/r/StremioAddons/comments/1ud6t8h/aiostreams_addons_best_order_list/
- https://www.reddit.com/r/StremioAddons/comments/1s3vukx/best_scrapers_aggregators/
- https://www.reddit.com/r/StremioAddons/comments/1uzygxu/the_ultimate_list_of_free_addons/
- https://www.reddit.com/r/StremioAddons/comments/1r8zspf/a_solution_for_people_that_depend_on_using/

For behavior/config claims, prefer the official AIOStreams docs and the Nuvio documentation listed in [SOURCES.md](SOURCES.md).

---

## My final recommendation

For a clean everyday setup:

```text
AIOStreams
  ├─ StremThru Torz
  ├─ Comet
  ├─ Meteor
  └─ MediaFusion

AIOMetadata
Stremio Community Subtitles
TorBox (primary) or Real-Debrid (alternative / backup)
```

Run that for a while **before adding anything else**.
