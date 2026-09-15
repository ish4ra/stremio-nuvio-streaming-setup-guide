# Sources and verification notes

Last reviewed: **2026-09-15**

This file records the main documentation used to keep the guide accurate.

## Nuvio

- Official organization: https://github.com/NuvioMedia
- Website: https://nuvio.tv
- Android TV releases: https://github.com/NuvioMedia/NuvioTV/releases
- Mobile repository: https://github.com/NuvioMedia/NuvioMobile
- Desktop releases: https://github.com/NuvioMedia/NuvioDesktop/releases
- Community Wiki — debrid integration: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/debrid.md
- Community Wiki — addons: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/addons.md
- Community Wiki — player/network settings: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/settings/player.md

### Nuvio native debrid note

At the time of this review, the Nuvio community documentation describes native Connected Services debrid support for **TorBox** and **Premiumize**. It also documents the architecture where a P2P-capable addon supplies raw source information and Nuvio performs the debrid resolution itself.

## AIOStreams

- Documentation: https://docs.aiostreams.viren070.me/
- Setup guide: https://docs.aiostreams.viren070.me/configuration/setup/
- Public instances: https://docs.aiostreams.viren070.me/getting-started/public-instances/
- Configure options: https://docs.aiostreams.viren070.me/configuration/options/

### Midnight public instance

The AIOStreams public-instance documentation currently lists:

- Stable: https://aiostreamsfortheweebsstable.midnightignite.me
- Nightly: https://aiostreamsfortheweebs.midnightignite.me

### ElfHosted public-instance note

The AIOStreams documentation currently states that the public ElfHosted instance excludes **P2P, HTTP, and Live** stream types. This is the reason the main guide does not recommend it for the specific Nuvio-native-TorBox P2P workflow.

This is not a claim that ElfHosted is generally unreliable; the official AIOStreams documentation describes it as a reputable/stable hosted option.

## TorBox

- Website: https://torbox.app/
- Pricing: https://torbox.app/pricing
- Help Center: https://support.torbox.app/

At the time of this review, TorBox lists the Essential plan at **$3/month**.

## Real-Debrid

- Website: https://real-debrid.com/
- AIOStreams setup documentation confirms Real-Debrid is one of the supported debrid services in its service-selection/configuration flow.

Commonly listed direct Real-Debrid price points at the time of review:

- €3 / 15 days
- €4 / 30 days
- €9 / 90 days
- €16 / 180 days

Because pricing can change, always verify the provider's checkout page before purchasing.

## IPv6 / buffering note

The guide deliberately does **not** claim that IPv6 automatically reduces buffering.

The practical recommendation is to use **dual stack (IPv4 + IPv6)** when the ISP provides native IPv6, then compare playback on the same source. Different IPv4/IPv6 routes can have different latency, congestion, and throughput, so results are ISP/provider/location dependent.

Do not switch a normal home network to IPv6-only just to troubleshoot streaming.

## Accuracy / updates

Public AIOStreams instances, Nuvio menus, provider integrations, prices, and limits change often. If one of the statements above becomes outdated, please open an issue or pull request with an updated source.
