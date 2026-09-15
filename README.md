<div align="center">

# Stremio + Nuvio Streaming Setup Guide

**A clean, practical setup for AIOStreams + TorBox / Real-Debrid — without addon clutter.**

[![Stremio](https://img.shields.io/badge/Stremio-supported-7B5CFA)](https://www.stremio.com/)
[![Nuvio](https://img.shields.io/badge/Nuvio-supported-4F46E5)](https://nuvio.tv/)
[![AIOStreams](https://img.shields.io/badge/AIOStreams-v2-111827)](https://docs.aiostreams.viren070.me/)
[![Last reviewed](https://img.shields.io/badge/reviewed-Sep%202026-0A7B83)](SOURCES.md)

</div>

---

## Pick your client

| Client | Recommended route | Guide |
|---|---|---|
| **Stremio** | AIOStreams handles your TorBox / Real-Debrid service and returns resolved streams | **[Stremio setup →](STREMIO.md)** |
| **Nuvio + native TorBox** | AIOStreams returns raw/P2P sources; Nuvio resolves them through TorBox | **[Nuvio setup →](NUVIO.md)** |
| **Nuvio + Real-Debrid** | AIOStreams handles Real-Debrid and sends resolved streams to Nuvio | **[Nuvio setup →](NUVIO.md)** |

> **The important difference:** Stremio does not provide Nuvio's native TorBox resolver. With Stremio, configure the debrid service in AIOStreams. With Nuvio's native TorBox integration, keep AIOStreams in raw/P2P mode instead.

---

## The lean setup I recommend

```text
Client
  │
  ├── AIOStreams
  │     ├── StremThru Torz
  │     ├── Comet
  │     ├── Meteor
  │     └── MediaFusion
  │
  ├── AIOMetadata
  └── Stremio Community Subtitles
```

**Debrid:** TorBox is my primary choice. Real-Debrid remains a useful alternative / backup depending on your client and preferred workflow.

This is intentionally a **small stack**. AIOStreams already combines, deduplicates, filters, sorts and formats results, so installing every scraper separately usually creates more duplicates and more things to troubleshoot.

**[See the curated addon list and advanced setup →](ADDONS.md)**

---

## AIOStreams host choice

| Host | Best for | Important note |
|---|---|---|
| **Midnight** | My preferred community instance | Stable + Nightly available |
| **Yeb's** | Easy default | AIOStreams docs currently recommend it as the general starting point |
| **ElfHosted public** | Professionally hosted / stable | Public instance excludes P2P, HTTP and Live stream types |
| **Self-hosted** | Maximum control | No public-instance policy/rate-limit dependency |

For most people, start with **Stable**. Use Nightly when you specifically need a newer fix or feature.

---

## Advanced quality-of-life setup

AIOStreams is most useful when it is treated as a **single stream layer**, not just a bag of addons.

A good configuration should:

- prefer **cached/debrid-ready** results when using a debrid-managed setup;
- sort by the quality and resolution your device can actually play;
- prefer your audio language and supported audio formats;
- set a sensible file-size ceiling for your connection/device;
- exclude formats you do not want, such as 3D or unsupported HDR/DV profiles;
- deduplicate equivalent results;
- keep backup sources enabled without letting them flood the top of the list.

AIOStreams supports filtering by resolution, size, visual tags, language and other stream properties, plus custom sorting/formatting.

**Do not copy someone else's giant config blindly.** Start lean, test it, then add only what fixes a real gap.

---

## Buffering / network problems

Before changing ten settings at once:

1. Test another source for the same title.
2. Try a smaller file / lower bitrate.
3. Compare your current AIOStreams instance with another instance.
4. Check the debrid provider's status/routing.
5. Test IPv4 vs **dual-stack IPv4 + IPv6** if your ISP provides native IPv6.
6. Only then tune player/network options.

IPv6 is **not** a guaranteed buffering fix. It can help when your ISP has a better IPv6 route to the host, and it can be worse when that route is poor.

**[Full troubleshooting flow →](TROUBLESHOOTING.md)**

---

## Guide map

| File | What it contains |
|---|---|
| **[STREMIO.md](STREMIO.md)** | Stremio + AIOStreams + TorBox / Real-Debrid |
| **[NUVIO.md](NUVIO.md)** | Nuvio native-TorBox route + AIOStreams-managed fallback |
| **[ADDONS.md](ADDONS.md)** | Curated addons, source sets and advanced recommendations |
| **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** | Buffering, missing streams, subtitles and instance problems |
| **[SOURCES.md](SOURCES.md)** | Documentation and verification notes |

---

## Why this guide stays small

The 2026 ecosystem changes quickly. Public instances go up and down, addons change hosts, and provider support changes. This repo therefore focuses on **architecture and a small set of reliable building blocks** instead of maintaining a giant list that becomes stale.

Use the services and addons only with media you own or are authorized to access. This is a community guide and is not affiliated with Stremio, Nuvio, AIOStreams, TorBox, Real-Debrid or the addon developers.

<div align="center">

If this setup saved you time, a ⭐ helps other people find the guide.

</div>
