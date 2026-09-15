# Stremio & Nuvio Streaming Setup Guide

> A practical setup guide for **Stremio or Nuvio + AIOStreams + TorBox / Real-Debrid**, with client-specific instructions and buffering/network troubleshooting.

[![Stremio](https://img.shields.io/badge/Stremio-media%20center-7b5cff)](https://www.stremio.com/)
[![Nuvio](https://img.shields.io/badge/Nuvio-media%20client-4f46e5)](https://nuvio.tv)
[![AIOStreams](https://img.shields.io/badge/AIOStreams-Midnight-111827)](https://docs.aiostreams.viren070.me/)
[![TorBox](https://img.shields.io/badge/TorBox-Essential%20%243%2Fmo-2563eb)](https://torbox.app/pricing)

This guide is for media you own or are otherwise authorized to access. Stremio, Nuvio, AIOStreams, TorBox, Real-Debrid, and this repository are independent projects/services.

---

## Start here

Choose your client:

- **Stremio:** [STREMIO.md](STREMIO.md)
- **Nuvio:** [NUVIO.md](NUVIO.md)
- Verification / source notes: [SOURCES.md](SOURCES.md)

---

## The most important difference

The AIOStreams setup should be different depending on the client.

### Stremio route

```text
Stremio
  └─ AIOStreams
       ├─ TorBox API key
       └─ or Real-Debrid API key
            ↓
       resolved playable streams
```

Stremio does not provide Nuvio's native TorBox resolver, so for the setup in this guide your debrid credentials are configured **inside AIOStreams**.

### Nuvio + native TorBox route

```text
AIOStreams
  └─ raw/P2P source results
       ↓
Nuvio native debrid resolver
  └─ TorBox
       ↓
playable stream
```

If your Nuvio build exposes **Settings → Integrations → Connected Services → TorBox**, this is the route I recommend for TorBox:

- connect TorBox directly in Nuvio;
- configure AIOStreams **without** a TorBox API key;
- keep P2P/raw-source results available;
- let Nuvio resolve them through TorBox locally.

> **Do not configure the same TorBox account inside AIOStreams if your goal is to use Nuvio's native TorBox resolver.** If AIOStreams resolves the link first, Nuvio never receives the raw source that its own resolver needs.

### Nuvio + Real-Debrid / fallback route

```text
AIOStreams + Real-Debrid or TorBox credentials
       ↓
resolved playable stream
       ↓
Nuvio
```

Use this route when:

- you want **Real-Debrid** in Nuvio;
- your Nuvio build does not expose native TorBox Connected Services;
- or you simply prefer AIOStreams to handle debrid resolution.

Current Nuvio community documentation lists **TorBox and Premiumize** for its native debrid integration, not Real-Debrid.

---

## My AIOStreams instance choice

For this guide I use **Midnight's AIOStreams**.

**Stable**

https://aiostreamsfortheweebsstable.midnightignite.me

**Nightly**

https://aiostreamsfortheweebs.midnightignite.me

I prefer Midnight for my own setup. Public-instance performance can vary by location, routing, load, and upstream addon health, so this is a personal preference rather than a claim that every other host is worse.

### What about ElfHosted?

AIOStreams' current documentation describes the public ElfHosted instance as a reputable, professionally hosted and very stable option. However, that public instance **forcefully excludes P2P, HTTP, and Live stream types**.

That matters especially for **Nuvio's native TorBox route**, because Nuvio needs compatible raw/P2P results to resolve itself.

For normal **Stremio + debrid-through-AIOStreams**, ElfHosted may still work well. If you personally experience buffering, slow startup, or routing differences on any public host, compare the same source using Midnight or another public instance before concluding the debrid service itself is the problem.

AIOStreams' own setup guide currently recommends **Yeb's** as the general starting point for most users, while listing Midnight as another community instance. This repo uses Midnight because that is my preferred setup.

---

## Debrid options

### TorBox — recommended starting point for this guide

Current TorBox Essential plan:

- **$3/month**
- 3 concurrent download slots
- unlimited downloads
- 200 GB max per download
- up to 1 Gbps listed speed
- API / third-party app access
- 300 GB permanent storage

Official pricing:

https://torbox.app/pricing

For **Stremio/AIOStreams**, TorBox's AIOStreams setup requires the API key from:

**TorBox → Settings → API**

For **Nuvio native TorBox**, link the account inside Nuvio instead and leave TorBox credentials out of AIOStreams.

### Real-Debrid

AIOStreams supports Real-Debrid credentials directly. Its setup documentation points users to:

**Real-Debrid → My Account → API**

Commonly documented current price points:

| Duration | Price | Approx. cost per 30 days |
|---|---:|---:|
| 15 days | €3 | €6.00 |
| 30 days | €4 | €4.00 |
| 90 days | €9 | €3.00 |
| 180 days | €16 | ~€2.67 |

So a **30-day Real-Debrid plan is a little more expensive than TorBox Essential** on the headline price, while longer RD packages reduce the effective 30-day cost.

AIOStreams' current docs also describe Real-Debrid as having a larger cache but a one-IP-at-a-time restriction. Check the provider's current rules before purchase because policies can change.

---

## AIOStreams Stable vs Nightly

AIOStreams public instances may offer:

- **Stable** — official tagged releases; safer default for everyday use.
- **Nightly** — newest changes and fixes first, with a higher chance of regressions.

The official AIOStreams template documentation says its current template is developed/tested primarily against **Nightly**, although it generally works on Stable too.

My suggestion:

1. Start with **Midnight Stable**.
2. If the current template or a new feature does not work correctly, test **Midnight Nightly**.
3. Once fixed/released, move back to Stable if you prefer fewer changes.

---

## Buffering: what to test first

Do not immediately assume your internet package is too slow. Playback depends on the selected file, bitrate, debrid/CDN route, player, public AIOStreams instance, upstream addons, and your ISP path.

Try these in order:

1. **Try another source/file.**
2. **Try a smaller file / lower bitrate.**
3. **Compare Midnight Stable vs Nightly.**
4. **Compare another AIOStreams public instance.**
5. **Check TorBox / Real-Debrid service status.**
6. Test on Ethernet or strong 5 GHz / 6 GHz Wi-Fi.
7. If your client exposes them, test HTTP/network options such as parallel connections conservatively rather than maxing them immediately.

If one public AIOStreams instance buffers while another does not, that can indicate host/routing/upstream differences rather than a problem with Stremio/Nuvio itself.

---

## IPv6: will it reduce buffering?

**Possibly, but not automatically.**

Enabling IPv6 can help only when your ISP has a better IPv6 route to the debrid/CDN endpoint than its IPv4 route. If IPv6 routing is equal, you may see no difference. If it is poor or broken, playback can become worse.

### Best way to test

Keep **dual stack** enabled:

```text
IPv4 + IPv6
```

Do not switch your home network to IPv6-only just for streaming.

1. Enable your ISP's **native IPv6** option if supported.
2. Keep IPv4 enabled.
3. Reconnect/reboot the router and client.
4. Confirm the device actually has working IPv6 connectivity.
5. Test the **same source/file** before and after.
6. Compare startup time, sustained bitrate, and buffering.
7. If it becomes worse, disable IPv6 again.

Modern clients commonly race or prefer the route that establishes connectivity best, but application and provider behavior still varies.

**Bottom line:** IPv6 is an **A/B test**, not a guaranteed anti-buffering tweak.

---

## Security / privacy notes

- Never commit a TorBox, Real-Debrid, TMDB, TVDB, or other API key to GitHub.
- A public AIOStreams instance has to process the configuration needed to use services configured through that instance. If you do not want to trust a community host with that configuration, self-host AIOStreams or use Nuvio's native TorBox route where available.
- Keep your AIOStreams configuration UUID/password private.
- Public instance URLs, restrictions, and availability can change at any time.

---

## Quick architecture table

| Client / service | Where the debrid account goes | AIOStreams mode |
|---|---|---|
| **Stremio + TorBox** | TorBox API key in AIOStreams | Debrid-enabled |
| **Stremio + Real-Debrid** | RD API key in AIOStreams | Debrid-enabled |
| **Nuvio + native TorBox** | TorBox connected inside Nuvio | P2P/raw-source, no TorBox key in AIOStreams |
| **Nuvio + Real-Debrid** | RD API key in AIOStreams | Debrid-enabled |
| **Nuvio without native TorBox support** | TorBox API key in AIOStreams | Debrid-enabled |

---

## Useful links

### Stremio
- https://www.stremio.com/
- https://stremio.zendesk.com/hc/en-us/articles/360021348391-How-to-install-uninstall-Add-ons

### Nuvio
- https://nuvio.tv
- https://github.com/NuvioMedia
- Community docs: https://github.com/haaihond/Nuvio-Wiki

### AIOStreams
- Docs: https://docs.aiostreams.viren070.me/
- Setup: https://docs.aiostreams.viren070.me/configuration/setup/
- Public instances: https://docs.aiostreams.viren070.me/getting-started/public-instances/
- Configure options: https://docs.aiostreams.viren070.me/configuration/options/

### Debrid
- TorBox: https://torbox.app/
- TorBox pricing: https://torbox.app/pricing
- Real-Debrid: https://real-debrid.com/

---

## Notes

This is a personal/community setup guide, not official documentation for any project or service mentioned above. Menus, pricing, instance restrictions, and integrations change quickly.

If something is outdated, open an issue or PR with a current source where possible.
