# Stremio + AIOStreams + TorBox / Real-Debrid

This page is the **Stremio-specific** version of the setup.

> Use this only with media you own or are otherwise authorized to access.

---

## Recommended architecture

```text
Stremio
  └─ AIOStreams (Midnight)
       └─ TorBox or Real-Debrid credentials
            ↓
       resolved playable streams
```

Unlike Nuvio's native TorBox route, **Stremio does not provide a built-in TorBox resolver for this workflow**. Configure the debrid service inside AIOStreams.

---

## 1. Install and sign in to Stremio

Download the current Stremio client for your platform:

https://www.stremio.com/downloads

Sign in to your Stremio account before installing AIOStreams. Stremio's official help center describes community addons as being installed to the user's account.

If you use Stremio Web for installation, make sure you are signed in to the **web player**, not using a guest session.

---

## 2. Choose a debrid provider

### Option A — TorBox

TorBox Essential is the starting point I use in this guide.

Current listed Essential plan:

- $3/month
- 3 concurrent download slots
- unlimited downloads
- 200 GB max per download
- up to 1 Gbps listed speed
- API / third-party app support

Create an account and choose a plan:

https://torbox.app/

Then go to:

**TorBox → Settings → API**

Copy your **API Key**. You will enter it into AIOStreams.

### Option B — Real-Debrid

Real-Debrid is also supported by AIOStreams.

After creating an account and activating Premium, get the API token from:

https://real-debrid.com/apitoken

AIOStreams' current setup documentation describes Real-Debrid as having a larger cache, but also a one-IP-at-a-time restriction. Check Real-Debrid's current rules before relying on that behavior long term.

---

## 3. Open Midnight AIOStreams

I use Midnight's community instance.

### Stable

https://aiostreamsfortheweebsstable.midnightignite.me

### Nightly

https://aiostreamsfortheweebs.midnightignite.me

Start with **Stable** for normal use.

The current AIOStreams template documentation is primarily tested against **Nightly**, so if a template option is missing or broken on Stable, try Nightly before assuming your API key is wrong.

---

## 4. Configure AIOStreams

Open the configure/template page on your chosen Midnight instance.

When the template asks for services:

- choose **TorBox** if using TorBox;
- choose **Real Debrid** if using Real-Debrid;
- enter the matching API key when prompted.

AIOStreams currently supports both services in its configuration system.

If the template asks for the TorBox tier, select the plan you actually have so size limits are configured correctly.

Review filtering, resolution, language, size, and sorting options rather than blindly enabling everything.

---

## 5. Save the AIOStreams configuration

On **Save & Install**:

1. Create the configuration.
2. Choose a strong configuration password.
3. Save the generated **UUID and password** somewhere private.
4. Do not commit either one to GitHub.

If an upstream addon is temporarily unavailable and AIOStreams reports that its manifest cannot be fetched, disable that upstream addon temporarily, save the configuration, and try it again later.

---

## 6. Install in Stremio

AIOStreams currently offers several Stremio-compatible install methods:

- **Install to Stremio** — opens the installed Stremio client;
- **Install to Stremio Web** — use this only while signed in to Stremio Web;
- **Manifest URL** — manual installation / compatible-client option.

For the simplest route:

1. Stay signed in to Stremio.
2. Click **Install to Stremio** or **Install to Stremio Web**.
3. Confirm the addon installation in Stremio.
4. Open a title you are authorized to access and verify that AIOStreams results appear.

---

## 7. Why Midnight instead of ElfHosted in my setup?

This is mainly a **personal preference**.

AIOStreams' own docs describe the public ElfHosted instance as reputable and professionally hosted. However, its public instance forcefully excludes:

- P2P
- HTTP
- Live

For a Stremio setup where AIOStreams itself resolves debrid links, that does **not automatically make ElfHosted unusable**.

I use Midnight because it gives me the setup/profile I prefer. Public-host performance can vary by geography, routing, load, and upstream-addon health. If you see buffering on one instance, compare the exact same source on Midnight or another public instance before changing debrid providers.

---

## 8. TorBox vs Real-Debrid for this guide

| Feature | TorBox | Real-Debrid |
|---|---|---|
| AIOStreams support | Yes | Yes |
| Starting price used here | $3/month Essential | €4 / 30 days |
| Longer-term price style | monthly/yearly plans | fixed-duration packages |
| Stremio route | API key in AIOStreams | API key in AIOStreams |
| Nuvio native resolver | Supported where available | Not currently listed as native Nuvio Connected Service |

Real-Debrid commonly lists €3/15 days, €4/30, €9/90 and €16/180. The 180-day package works out to about €2.67 per 30 days, so RD is not always more expensive when comparing longer durations.

---

## 9. Buffering troubleshooting

Try these before rebuilding everything:

1. Pick another source/file.
2. Try a lower bitrate or smaller file.
3. Compare Midnight Stable vs Nightly.
4. Compare Midnight with another AIOStreams public instance.
5. Check your debrid provider status.
6. Test Ethernet or strong 5 GHz / 6 GHz Wi-Fi.
7. Test another Stremio player/device if available.
8. Try IPv6 only as a controlled **dual-stack A/B test** — see the main README.

If only one AIOStreams public host buffers, the cause may be that host's route/load/upstream path rather than Stremio itself.

---

## 10. Security notes

- Treat your TorBox or Real-Debrid API key like a password.
- Never paste API keys into an issue, screenshot, TikTok, README, or public config export.
- A public AIOStreams instance must process the configuration needed to use the services configured through it.
- If you want maximum control, self-host AIOStreams.

---

## Useful links

- Stremio: https://www.stremio.com/
- Stremio addon help: https://stremio.zendesk.com/hc/en-us/articles/360021348391-How-to-install-uninstall-Add-ons
- AIOStreams docs: https://docs.aiostreams.viren070.me/
- AIOStreams setup: https://docs.aiostreams.viren070.me/configuration/setup/
- Public instances: https://docs.aiostreams.viren070.me/getting-started/public-instances/
- TorBox: https://torbox.app/
- Real-Debrid: https://real-debrid.com/
