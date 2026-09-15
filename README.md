<div align="center">

# 🎬 Stremio + Nuvio Streaming Setup Guide

### One clean AIOStreams setup. Two clients. Less addon clutter.

A practical setup reference for **Stremio** and **Nuvio** using **AIOStreams**, a small curated addon stack, optional debrid integration, and focused troubleshooting.

![Stremio](https://img.shields.io/badge/Stremio-guide-7B5CFA?style=for-the-badge)
![Nuvio](https://img.shields.io/badge/Nuvio-guide-4F46E5?style=for-the-badge)
![Reviewed](https://img.shields.io/badge/reviewed-September%202026-0969da?style=for-the-badge)

**[Stremio setup](STREMIO.md)** · **[Nuvio setup](NUVIO.md)** · **[Curated addons](ADDONS.md)** · **[Troubleshooting](TROUBLESHOOTING.md)**

</div>

---

## ✨ Pick your path

<table>
<tr>
<td width="50%" valign="top">

### 🟣 Stremio

Best when you want a mature cross-platform client with an addon-driven workflow.

**Recommended architecture:** let AIOStreams handle the configured stream/debrid layer and return the final results to Stremio.

**[Open the Stremio guide →](STREMIO.md)**

</td>
<td width="50%" valign="top">

### 🔵 Nuvio

Best when you prefer Nuvio's interface/features and want the option to use its native provider integrations where supported.

The exact AIOStreams role depends on whether Nuvio itself is handling the provider side.

**[Open the Nuvio guide →](NUVIO.md)**

</td>
</tr>
</table>

> **Important:** do not blindly copy the same AIOStreams/debrid configuration between Stremio and Nuvio. The client architecture can differ.

---

## 🧭 Architecture at a glance

### Stremio route

```text
Stremio
   │
   ▼
AIOStreams
   │
   ├── curated source/addon layer
   └── optional provider/debrid handling
   │
   ▼
Returned stream results
```

### Nuvio route

```text
Nuvio
   │
   ├── native provider integration (when used)
   │
   └── AIOStreams
          │
          └── curated source/addon layer
```

The goal is not “install everything.” The goal is a predictable stream pipeline that is easy to troubleshoot.

---

## 🚀 Quick setup flow

| Step | Action |
|---|---|
| **1** | Choose **Stremio** or **Nuvio** as the main client |
| **2** | Add/configure **AIOStreams** for that client architecture |
| **3** | Keep the source stack small |
| **4** | Add metadata/subtitle helpers only if useful |
| **5** | Test a few titles and confirm result quality |
| **6** | Tune filters/sorting instead of adding dozens of addons |
| **7** | Use the troubleshooting guide before changing everything at once |

---

## 🧩 Lean addon stack

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

Why keep it small?

- fewer duplicate results;
- fewer moving parts;
- easier debugging;
- easier migration between instances;
- less time maintaining addon clutter.

**[See the addon notes and advanced recommendations →](ADDONS.md)**

---

## ⚙️ AIOStreams: what to tune first

AIOStreams is most useful when treated as the **single organization/filtering layer** rather than just another addon.

| Setting area | Practical goal |
|---|---|
| **Resolution** | Prioritize formats your device can actually play |
| **File size** | Avoid results that exceed your connection/device limits |
| **Audio** | Prefer languages/codecs your setup supports |
| **HDR / DV / visual tags** | Exclude formats your display/player cannot handle well |
| **Sorting** | Put the most useful results first |
| **Deduplication** | Reduce equivalent duplicate entries |
| **Backup sources** | Keep them available without letting them dominate results |

> Start with a boring config that works. Add complexity only when you can point to a real problem it solves.

---

## 🌍 Instance / host choice

| Option | Best for | Note |
|---|---|---|
| **Midnight** | Community-hosted option | Stable / Nightly availability can vary |
| **Yeb's** | Easy community starting point | Useful general default when available |
| **ElfHosted public** | Professionally hosted public option | Public policy/features may differ from self-hosting |
| **Self-hosted** | Maximum control | You manage uptime, updates and resources |

Public instances can change policy, capacity, or availability. If reliability matters, keep the setup portable enough to switch hosts.

---

## 🧠 Stable vs Nightly

<table>
<tr>
<td width="50%" valign="top">

### ✅ Stable

Use this by default.

Best for people who want fewer surprises and do not need a newly added fix immediately.

</td>
<td width="50%" valign="top">

### 🧪 Nightly

Use when a specific new fix/feature matters to you and you are willing to troubleshoot regressions.

Do not choose Nightly just because the version number is newer.

</td>
</tr>
</table>

---

## 🧯 Buffering / missing-stream troubleshooting

Do **one test at a time**.

```text
Problem
  │
  ├─ Try another result/source
  │
  ├─ Try a smaller file / lower bitrate
  │
  ├─ Compare another AIOStreams instance
  │
  ├─ Check provider/debrid status if used
  │
  ├─ Compare network path / IPv4 / IPv6 where relevant
  │
  └─ Only then change player/filter settings
```

| Symptom | First thing to check |
|---|---|
| No results | Instance/addon health and filtering rules |
| Many duplicates | Deduplication / source overlap |
| Buffering | Bitrate, source quality, routing, provider health |
| One title fails | Try another result for the same title |
| Subtitles missing | Subtitle addon/configuration |
| Works on one client but not another | Client playback/codec differences |

IPv6 can help when your ISP has a better route to the host, but it is **not** a universal buffering fix.

**[Open the full troubleshooting flow →](TROUBLESHOOTING.md)**

---

## 📚 Guide map

<table>
<tr>
<td width="50%" valign="top">

### Client setup

- **[STREMIO.md](STREMIO.md)** — Stremio architecture and setup
- **[NUVIO.md](NUVIO.md)** — Nuvio architecture and setup

</td>
<td width="50%" valign="top">

### Reference

- **[ADDONS.md](ADDONS.md)** — curated addon/source notes
- **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** — diagnostic flow
- **[SOURCES.md](SOURCES.md)** — documentation / verification notes

</td>
</tr>
</table>

---

## 🎯 What this guide deliberately avoids

- installing every addon that exists;
- giant configs copied without understanding them;
- treating Nightly as automatically better;
- changing ten settings at once when troubleshooting;
- pretending one client architecture maps perfectly onto another;
- maintaining a huge stale list of public instances.

The ecosystem moves quickly. A smaller architecture-focused guide ages better than a giant catalogue.

---

## 🌐 Related repos

- **[jellyfin-media-server-guide](https://github.com/ish4ra/jellyfin-media-server-guide)** — build your own personal media server
- **[open-source-alternatives](https://github.com/ish4ra/open-source-alternatives)** — discover open-source replacements and media tools
- **[selfhosted-picks](https://github.com/ish4ra/selfhosted-picks)** — self-hosted software worth running
- **[homelab-from-zero](https://github.com/ish4ra/homelab-from-zero)** — build the infrastructure underneath self-hosted services

---

## Responsible use

Use apps, services, addons and integrations only with media you own or are authorized to access. This community guide is not affiliated with Stremio, Nuvio, AIOStreams, hosting providers, or addon developers.

---

<div align="center">

### Useful setup reference?

A ⭐ helps other users discover the guide.

**Keep the stack small. Keep the architecture understandable.**

<sub>Last reviewed: September 2026</sub>

</div>
