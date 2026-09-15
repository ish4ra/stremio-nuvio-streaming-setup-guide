# Nuvio Streaming Setup Guide

> A clean, practical setup for **Nuvio + AIOStreams (Midnight) + TorBox**, with a Real-Debrid alternative and buffering/network troubleshooting.

[![Nuvio](https://img.shields.io/badge/Nuvio-media%20client-4f46e5)](https://nuvio.tv)
[![AIOStreams](https://img.shields.io/badge/AIOStreams-Midnight-111827)](https://docs.aiostreams.viren070.me/)
[![TorBox](https://img.shields.io/badge/TorBox-Essential%20%243%2Fmo-2563eb)](https://torbox.app/pricing)

## What this setup does

My preferred stack is:

```text
Nuvio
  ├─ AIOStreams (Midnight public instance)
  │    └─ returns source/P2P results
  │
  └─ Nuvio native debrid integration
       └─ TorBox resolves playable links
```

The main advantage of this layout is that your **TorBox account is linked directly inside Nuvio**. AIOStreams can be used as the source layer without needing your TorBox key.

This guide is intended for media you own or are otherwise authorized to access. Nuvio, AIOStreams, TorBox, Real-Debrid, and this repository are independent projects/services.

---

## Recommended stack

| Part | Recommended | Why |
|---|---|---|
| Client | **Nuvio** | Free/open-source client with native TorBox integration |
| Source aggregator | **AIOStreams — Midnight** | Good public-instance option; stable + nightly channels available |
| Debrid | **TorBox Essential** | Low-cost entry tier, native Nuvio support |
| Alternative debrid | **Real-Debrid** | Works through AIOStreams, but is not currently a native Nuvio Connected Service |

### Current pricing snapshot

- **TorBox Essential:** **$3/month**
- **Real-Debrid:** **€4 / 30 days**, **€9 / 90 days**, **€16 / 180 days**

So the simple 30-day Real-Debrid option is a little more expensive than TorBox Essential. However, the longer Real-Debrid plans have a lower effective cost per 30 days, so compare the actual duration you plan to buy rather than only the headline monthly price.

Prices and limits can change. Always check the provider's current pricing page before paying.

---

# 1. Install Nuvio

Use the official Nuvio project for your device:

- Website: https://nuvio.tv
- Android TV releases: https://github.com/NuvioMedia/NuvioTV/releases
- Mobile: https://github.com/NuvioMedia/NuvioMobile
- Desktop: https://github.com/NuvioMedia/NuvioDesktop/releases

Keep Nuvio updated because addon, player, and debrid behavior changes fairly quickly.

---

# 2. Get TorBox

For a normal personal setup, **TorBox Essential** is a good starting point.

Current Essential-plan highlights include:

- $3/month
- 3 concurrent download slots
- up to 200 GB per download
- up to 1 Gbps listed speed
- API / third-party app access
- 300 GB permanent storage

Sign up / pricing:

https://torbox.app/pricing

> You do **not** need to place the TorBox API key inside AIOStreams for the primary setup in this guide.

---

# 3. Connect TorBox directly to Nuvio

In Nuvio:

1. Open **Settings**.
2. Go to **Integrations → Connected Services**.
3. Select **TorBox**.
4. Complete the browser/device-code authorization flow.
5. Confirm the account shows as **Connected**.
6. Turn on **Resolve playable links**.
7. Optional: enable **Cloud library** if you want Nuvio to browse files already stored in your TorBox account.

Nuvio's native debrid integration can take raw P2P hashes returned by compatible addons and resolve them through your linked TorBox account.

---

# 4. Configure AIOStreams — Midnight

AIOStreams has several community-run public instances. I personally prefer **Midnight's instance** for this setup.

### Midnight URLs

**Stable**

https://aiostreamsfortheweebsstable.midnightignite.me

**Nightly**

https://aiostreamsfortheweebs.midnightignite.me

For most people, start with **Stable**. Try Nightly only if you need a newer feature or a fix that has not reached stable yet.

## Important: use P2P/source mode for native Nuvio + TorBox

For the primary setup in this guide:

- configure AIOStreams as a source/P2P layer;
- **do not add your TorBox API key to AIOStreams**;
- let Nuvio's native TorBox integration resolve playable links.

AIOStreams' template/setup flow allows debrid selection to be skipped. The exact UI can change between releases, so the important rule is simple:

> **AIOStreams finds the raw source; Nuvio + TorBox resolves it.**

When AIOStreams gives you the final addon/manifest URL, install it in Nuvio.

Typical Nuvio path:

**Settings → Content & Discovery → Addons → Install from URL**

On Android TV, the addon menu may be accessible from the sidebar depending on the Nuvio version.

---

# 5. Why I use Midnight instead of ElfHosted for this setup

ElfHosted is a reputable and professionally hosted public AIOStreams instance, and the AIOStreams documentation describes it as a stable option.

However, its **public instance forcefully excludes P2P, HTTP, and Live stream types**. That makes it a poor fit for this particular Nuvio-native-debrid workflow, because Nuvio needs compatible raw/P2P results to hand to its own TorBox resolver.

Public instances can also experience temporary load, routing, availability, or buffering-related issues. That does **not** mean ElfHosted is inherently slow or broken. If playback is poor, compare the same title/source with another instance before blaming the host.

For my setup, I use **Midnight** because it better matches the source/P2P workflow described above.

AIOStreams public-instance list:

https://docs.aiostreams.viren070.me/getting-started/public-instances/

---

# 6. Real-Debrid alternative

You can also use **Real-Debrid** with AIOStreams.

The important difference is architecture:

```text
TorBox route in this guide:
AIOStreams (source/P2P) → Nuvio → native TorBox integration

Real-Debrid alternative:
AIOStreams + Real-Debrid credentials → Nuvio receives resolved debrid streams
```

At the moment, Nuvio's native Connected Services debrid integration supports **TorBox and Premiumize**, not Real-Debrid. Therefore, if you want Real-Debrid, configure it inside AIOStreams instead of looking for a Real-Debrid button inside Nuvio's native Connected Services menu.

AIOStreams supports Real-Debrid as a service and can accept its API credentials in the configuration flow.

### Pricing

Current commonly listed Real-Debrid prices are:

| Duration | Price | Approx. cost per 30 days |
|---|---:|---:|
| 15 days | €3 | €6.00 |
| 30 days | €4 | €4.00 |
| 90 days | €9 | €3.00 |
| 180 days | €16 | ~€2.67 |

For a one-month test, TorBox Essential is usually cheaper on the headline price. For longer periods, Real-Debrid's effective 30-day cost can become competitive.

> Security note: putting a debrid API credential into a public AIOStreams instance means you are trusting that public instance with the configuration needed to use that service. If you want maximum control, self-host AIOStreams or use Nuvio's native TorBox route where possible.

---

# 7. Buffering: what to try first

Do not immediately assume your internet speed is the problem. Playback can depend on the selected file, provider route, CDN, public AIOStreams instance, player settings, and the debrid service.

Try these in order:

1. **Try another source/file** — one bad file does not mean the full setup is broken.
2. **Prefer cached sources** when using a debrid-resolved configuration.
3. **Try a smaller file / lower bitrate** to see whether the problem is raw throughput.
4. **Compare Midnight Stable vs Nightly** if one instance has a temporary issue.
5. **Test another AIOStreams public instance** to isolate instance-specific routing/load problems.
6. **Check TorBox service status / speed** before changing Nuvio settings.
7. If your Nuvio version exposes them, test **HTTP/2** and **Parallel Connections** under its custom network/player options.

### Parallel connections

Some hosts/CDNs cap throughput per TCP connection. Nuvio can use multiple HTTP range connections for progressive files when the host supports byte ranges. This can improve aggregate throughput on some connections, but more connections are not automatically better — they also increase memory and connection overhead.

Start conservatively and compare playback rather than maxing every setting.

---

# 8. IPv6: can it reduce buffering?

**Sometimes — but IPv6 is not a universal buffering fix.**

If your ISP has a better IPv6 route to the debrid/CDN server than its IPv4 route, IPv6 may improve latency or throughput. If the IPv6 route is worse, it can make no difference or even perform worse.

### Recommended way to test it

Do **not** replace your router with IPv6-only networking.

Use **dual stack** instead:

```text
IPv4 + IPv6
```

Then:

1. Enable your ISP's **native IPv6** option on the router if your ISP supports it.
2. Keep IPv4 enabled.
3. Reboot/reconnect the router and client device.
4. Confirm the device actually received IPv6 connectivity.
5. Play the same source/file and compare startup time + buffering.
6. If it gets worse, disable IPv6 again and compare.

Modern networking stacks often prefer the route that establishes connectivity fastest, but app behavior and provider routing still vary.

### Bottom line

- Good native IPv6 route → **may help**.
- Same-quality route → **probably no noticeable difference**.
- Poor/broken IPv6 route → **may hurt playback**.

So treat IPv6 as an **A/B test**, not a mandatory tweak.

---

# 9. Quick troubleshooting table

| Problem | First thing to check |
|---|---|
| No sources at all | Confirm AIOStreams addon is installed/enabled |
| P2P results appear but do not resolve | Confirm TorBox is connected in Nuvio and **Resolve playable links** is enabled |
| Real-Debrid does not appear in Nuvio Connected Services | Expected — configure RD in AIOStreams instead |
| Constant buffering on one file | Try another source / smaller file |
| Everything buffers | Test TorBox speed/status, network route, then another AIOStreams instance |
| ElfHosted does not return P2P streams | Expected on the public instance; P2P/HTTP/Live are excluded |
| Midnight temporarily fails | Try stable/nightly or another public instance |
| IPv6 made things worse | Return to IPv4 or dual-stack with IPv6 disabled and compare |

---

# Useful links

### Nuvio
- https://nuvio.tv
- https://github.com/NuvioMedia

### Nuvio community documentation
- https://github.com/haaihond/Nuvio-Wiki

### AIOStreams
- Documentation: https://docs.aiostreams.viren070.me/
- Public instances: https://docs.aiostreams.viren070.me/getting-started/public-instances/
- Setup guide: https://docs.aiostreams.viren070.me/configuration/setup/

### TorBox
- https://torbox.app/
- https://torbox.app/pricing

### Real-Debrid
- https://real-debrid.com/

---

# Notes

This is a personal/community setup guide, not official documentation for any of the projects or services mentioned above. Public instance URLs, pricing, features, and menus may change over time.

If something in this guide is outdated, open an issue or PR with the current behavior and a source where possible.
