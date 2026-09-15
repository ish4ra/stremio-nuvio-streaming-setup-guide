# Sources and verification notes

Last reviewed: **2026-09-15**

This file records the primary/current documentation used to keep the guide accurate.

---

## Stremio

- Official downloads / platforms: https://www.stremio.com/downloads
- Addon installation help: https://stremio.zendesk.com/hc/en-us/articles/360021348391-How-to-install-uninstall-Add-ons
- Official addon catalogue / platform overview: https://addons.stremio.com/

### Stremio setup note

Stremio community addons are attached to the user's account when installed while signed in. AIOStreams' own installation page offers direct Stremio, Stremio Web, and manifest-URL installation methods.

For the architecture in this repository, Stremio does not use Nuvio's native TorBox resolver. TorBox or Real-Debrid credentials are configured in AIOStreams instead.

---

## Nuvio

- Website: https://nuvio.tv
- Official GitHub organization: https://github.com/NuvioMedia
- Community Wiki — integration overview: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/index.md
- Community Wiki — debrid integration: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/debrid.md
- Community Wiki — addons: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/addons.md

### Nuvio native debrid architecture

The current Nuvio community documentation describes native debrid support for **TorBox and Premiumize**.

It documents this flow:

1. a compatible addon supplies raw/P2P source information;
2. Nuvio receives the raw source;
3. Nuvio resolves that source through the linked TorBox/Premiumize account.

The same documentation explicitly warns that putting a debrid API key into the addon bypasses Nuvio's native resolver because the addon resolves the link before Nuvio sees the raw source.

Because Nuvio platform/build support changes, the guide says to use the native route **where Connected Services exposes TorBox** and otherwise fall back to AIOStreams-managed debrid.

---

## AIOStreams

- Main documentation: https://docs.aiostreams.viren070.me/
- Introduction: https://docs.aiostreams.viren070.me/getting-started/
- Setup guide: https://docs.aiostreams.viren070.me/configuration/setup/
- Public instances: https://docs.aiostreams.viren070.me/getting-started/public-instances/
- Configure options: https://docs.aiostreams.viren070.me/configuration/options/
- Deployment / self-hosting: https://docs.aiostreams.viren070.me/getting-started/deployment/

### Supported services

AIOStreams' current configuration documentation supports services including **TorBox** and **Real Debrid**.

The official setup flow currently instructs:

- TorBox users: **TorBox → Settings → API** → copy API key.
- Real-Debrid users: **My Account → API** / https://real-debrid.com/apitoken → copy API key.

The template service-selection screen can also be skipped, which is important for Nuvio's native-TorBox P2P/raw-source architecture.

### Template channel note

The current AIOStreams setup documentation says the main template is developed/tested against **Nightly**. It generally works on Stable, but new template features may land on Nightly first.

The guide therefore recommends Midnight Stable for normal use, with Midnight Nightly as a troubleshooting/fresh-feature option.

---

## AIOStreams public instances

Official comparison:

https://docs.aiostreams.viren070.me/getting-started/public-instances/

### Midnight

Current listed URLs:

- Stable: https://aiostreamsfortheweebsstable.midnightignite.me
- Nightly: https://aiostreamsfortheweebs.midnightignite.me

The docs identify Midnight's instance as hosted by `@midnightignite`.

This repository uses Midnight as a **personal preference**. It does not claim Midnight is universally faster for every ISP/location.

### ElfHosted

AIOStreams' current docs describe the public ElfHosted instance as professionally hosted and highly stable, but state that it forcefully excludes:

- P2P
- HTTP
- Live

That restriction makes the public ElfHosted instance a poor match for the **Nuvio native TorBox** route in this guide, which depends on compatible raw/P2P source results.

For normal Stremio + AIOStreams-managed debrid, ElfHosted may still be suitable.

The guide deliberately phrases buffering as a possible host/routing/load difference rather than claiming ElfHosted is inherently broken.

### General AIOStreams recommendation

AIOStreams' current setup documentation recommends **Yeb's** as the general starting point for most users. This repository still uses Midnight because that is the author's preferred configuration.

---

## TorBox

- Website: https://torbox.app/
- Official pricing: https://torbox.app/pricing
- Help Center: https://support.torbox.app/

At the time of this review, the official pricing page lists the **Essential** plan at:

- $3/month
- 3 concurrent slots
- unlimited downloads
- 200 GB max per download
- up to 1 Gbps listed speed
- API access
- third-party apps
- 300 GB permanent storage

Provider limits/pricing can change, so the official pricing page should always win over this snapshot.

---

## Real-Debrid

- Website: https://real-debrid.com/
- API token page: https://real-debrid.com/apitoken
- AIOStreams setup documentation: https://docs.aiostreams.viren070.me/configuration/setup/

AIOStreams' current setup docs describe Real-Debrid as a supported service, with a larger cache than TorBox and a one-IP-at-a-time restriction.

Commonly documented current price points in the Nuvio community debrid guide and recent comparisons are:

- €3 / 15 days
- €4 / 30 days
- €9 / 90 days
- €16 / 180 days

The guide treats these as a snapshot rather than a permanent promise. Always check Real-Debrid's current checkout / Premium Offers page before purchasing.

---

## IPv6 / buffering note

The guide intentionally does **not** claim that IPv6 automatically reduces buffering.

IPv4 and IPv6 can take different network paths. If an ISP has a less congested or lower-latency IPv6 path to the debrid/CDN endpoint, IPv6 may improve playback. If IPv6 routing is worse or broken, it may do nothing or make playback worse.

The recommended test is therefore:

- keep IPv4 enabled;
- enable native IPv6 if the ISP supports it;
- use **dual stack**;
- test the same file/source before and after;
- revert if performance becomes worse.

This is an A/B troubleshooting step, not a guaranteed optimization.

---

## Accuracy / updates

AIOStreams instances, Nuvio menus, provider integrations, prices, and limits change frequently.

If a statement becomes outdated, open an issue or pull request with a current source where possible.
