# Troubleshooting

> Change **one thing at a time**. If you change the source, AIOStreams instance, debrid service and network settings together, you will not know what actually fixed the problem.

[← Back to README](README.md) · [Addons](ADDONS.md) · [Stremio](STREMIO.md) · [Nuvio](NUVIO.md)

---

## Quick diagnosis

| Symptom | Most likely area |
|---|---|
| No streams at all | AIOStreams addon/config/instance |
| Streams appear but none play | Debrid authorization or source type |
| Only one title buffers | Source/file problem |
| Everything buffers | Provider route, network, player or instance |
| Duplicate streams everywhere | Same addons installed both standalone and inside AIOStreams |
| Nuvio native TorBox never resolves | AIOStreams is returning resolved links instead of raw/P2P hashes |
| Real-Debrid missing from Nuvio Connected Services | Expected; use Real-Debrid through AIOStreams |
| Wrong / out-of-sync subtitles | Subtitle release does not match the selected video release |
| ElfHosted public has no P2P/HTTP results | Expected public-instance restriction |

---

# 1. No streams at all

Check in this order:

1. Confirm AIOStreams is still installed/enabled in the client.
2. Open the AIOStreams configuration URL and make sure the public instance itself loads.
3. Confirm at least one source addon is enabled inside AIOStreams.
4. Try a very common title to separate a setup failure from a rare-title coverage problem.
5. Test a second public AIOStreams instance.

If the same config works on another host, the problem is probably instance-specific rather than your client.

---

# 2. Streams show up but do not play

## Stremio

With the normal Stremio route, the debrid service is configured in **AIOStreams**.

Check:

- the TorBox / Real-Debrid credential is still valid;
- the correct service is enabled in AIOStreams;
- the generated AIOStreams addon was reinstalled/saved after a credential/config change;
- the selected result is actually compatible with the service/configuration you chose.

Stremio does **not** have Nuvio's native TorBox Connected Services resolver.

## Nuvio native TorBox

If TorBox is linked under Nuvio's Connected Services, your scraper layer needs to provide **raw/P2P hashes**.

Do **not** configure the same TorBox key inside AIOStreams for this route, because AIOStreams may resolve the result first and Nuvio will no longer receive the raw hash its native resolver expects.

Check:

1. TorBox shows as connected in Nuvio.
2. Native link resolving is enabled.
3. AIOStreams is configured for P2P/raw output for the relevant sources.
4. Your public AIOStreams instance permits P2P results.

---

# 3. Buffering

## First: isolate the file

Before touching the router, try another release/source for the same title.

If one file buffers and another does not, your internet connection is probably not the primary problem.

## Then: isolate bitrate / size

Try a smaller file or lower-bitrate release.

If that fixes playback, the route/device may simply not sustain the original bitrate reliably.

## Then: isolate the AIOStreams host

Try the same setup through another AIOStreams public instance.

A public instance can affect search/aggregation latency and which stream types are allowed. Once a resolved media URL is playing, buffering can also depend heavily on the debrid/CDN route and selected file.

## Then: isolate the debrid/network route

Check your provider's status and, where available, its speed/routing tools.

A fast generic speed test to a nearby ISP server does **not** guarantee an equally fast route to your debrid/CDN host.

---

# 4. IPv6 — test, do not assume

IPv6 can help **only if** the IPv6 path from your ISP to the provider is better than the IPv4 path.

Recommended test:

```text
IPv4 + IPv6 (dual stack)
```

1. Keep IPv4 enabled.
2. Enable native IPv6 on the router only if your ISP supports it properly.
3. Confirm the playback device actually receives IPv6 connectivity.
4. Play the **same source/file** and compare startup time + buffering.
5. If playback is worse, disable IPv6 and compare again.

Do not switch the home network to IPv6-only just to chase a streaming problem.

---

# 5. Too many duplicate streams

The usual cause is this:

```text
AIOStreams
  ├─ Comet
  ├─ Meteor
  └─ MediaFusion

PLUS standalone Comet + Meteor + MediaFusion
```

Unless you intentionally want a standalone fallback, remove the duplicates and let AIOStreams deduplicate/sort the combined results.

See [ADDONS.md](ADDONS.md) for the lean profile.

---

# 6. Results are badly sorted

Do not fix bad sorting by adding more scrapers.

Use AIOStreams' own filtering/sorting options instead:

- prioritise cache/service state that matches your workflow;
- prefer the resolutions you actually want;
- set language/audio preferences;
- use a file-size ceiling if giant remuxes are not practical on your connection;
- exclude visual/audio formats your playback chain cannot handle;
- enable deduplication;
- use a readable formatter.

The official AIOStreams options reference explains these controls:

https://docs.aiostreams.viren070.me/configuration/options/

---

# 7. Subtitle problems

Different releases of the same movie/episode can have different:

- cuts/runtimes;
- frame rates;
- intros/recaps;
- Blu-ray vs WEB timing.

So a subtitle being "for the same movie" does not guarantee synchronization.

Recommended approach:

1. Use **Stremio Community Subtitles** as the first subtitle layer.
2. Set your preferred language(s).
3. If the automatic match is wrong, choose a subtitle matching the release/encode when possible.
4. Add only one backup provider if your language has weak coverage.

On Nuvio, its subtitle startup setting can also affect when addon subtitles are queried; a faster startup mode may delay/skip automatic subtitle fetching.

---

# 8. ElfHosted works differently from Midnight/Yeb's

The **public** ElfHosted AIOStreams instance excludes P2P, HTTP and Live stream types.

So this is normal:

```text
Works on Midnight/Yeb's
but disappears on ElfHosted public
```

if the missing result is one of those excluded types.

That restriction is especially important for the **Nuvio native TorBox + raw/P2P** workflow.

It is not evidence that ElfHosted is broken; it is a documented public-instance policy.

---

# 9. Public instance suddenly stops working

Community instances are not permanent infrastructure.

Try:

1. The host's Stable URL.
2. Its Nightly URL only if you need a current fix.
3. Another listed community instance.
4. The AIOStreams public-instance/status pages.
5. Self-hosting if you want to remove public-instance dependency.

Public instances:

https://docs.aiostreams.viren070.me/getting-started/public-instances/

---

# 10. Codec / player-specific failures

If a stream starts but has black video, no audio, severe frame drops, or immediately crashes the player, test another encode before blaming AIOStreams/debrid.

Look for differences in:

- HEVC/H.265 vs AVC/H.264;
- AV1 support;
- HDR / Dolby Vision profile support;
- TrueHD / DTS-HD / multichannel audio support;
- hardware-decoding capability of the device.

If your client/device supports another playback engine or external player, a quick comparison can help identify a decoder/player issue.

---

# Minimal recovery profile

When everything has become too complicated, temporarily reduce the setup to:

```text
AIOStreams
  ├─ StremThru Torz
  ├─ Comet
  ├─ Meteor
  └─ MediaFusion

one debrid service
one metadata layer
one subtitle layer
```

Test that. Then add optional pieces back **one at a time**.

That approach is usually faster than debugging a 15-addon stack.
