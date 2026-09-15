# Nuvio + AIOStreams + TorBox / Real-Debrid

This page is the **Nuvio-specific** setup.

> Use this only with media you own or are otherwise authorized to access.

---

## Choose one of these two Nuvio architectures

### Route A — recommended when native TorBox is available

```text
AIOStreams
  └─ raw/P2P source results
       ↓
Nuvio native resolver
  └─ TorBox
       ↓
playable stream
```

Use this route if your Nuvio build exposes:

**Settings → Integrations → Connected Services → TorBox**

For this route, **do not put your TorBox API key into AIOStreams**.

### Route B — AIOStreams handles debrid

```text
AIOStreams + TorBox or Real-Debrid credentials
       ↓
resolved playable stream
       ↓
Nuvio
```

Use this route when:

- you want **Real-Debrid**;
- your Nuvio build does not expose native TorBox Connected Services;
- or you want AIOStreams itself to resolve the links.

---

# Route A — Nuvio native TorBox

## 1. Install and update Nuvio

Use the current build for your platform:

- Website: https://nuvio.tv
- GitHub organization: https://github.com/NuvioMedia

Menus can vary between Nuvio platforms/builds, so keep the client updated.

---

## 2. Link TorBox directly in Nuvio

If your build supports the current native integration:

1. Open **Settings**.
2. Go to **Integrations → Connected Services**.
3. Select **TorBox**.
4. Complete the browser/device authorization flow.
5. Confirm the account shows as connected.
6. Enable **Resolve playable links**.
7. Optional: enable **Cloud library** if you want access to files already stored in your TorBox account.

Current Nuvio community documentation describes native debrid support for **TorBox and Premiumize**.

---

## 3. Open Midnight AIOStreams

### Stable

https://aiostreamsfortheweebsstable.midnightignite.me

### Nightly

https://aiostreamsfortheweebs.midnightignite.me

For normal use I start with **Stable**.

---

## 4. Configure AIOStreams for P2P/raw-source output

This is the critical part.

When the AIOStreams template asks which debrid service you use:

- choose **Skip / no debrid service** for this Nuvio-native-TorBox route;
- do **not** enter your TorBox API key;
- keep compatible **P2P/raw-source** results enabled;
- avoid filters that remove all P2P streams.

Nuvio needs the raw source information so its own TorBox integration can resolve it.

> If you add TorBox credentials to AIOStreams, AIOStreams resolves the debrid link itself and Nuvio's native TorBox resolver is bypassed.

---

## 5. Avoid the public ElfHosted instance for this specific route

AIOStreams' current docs say the public ElfHosted instance forcefully excludes:

- P2P
- HTTP
- Live

Because this native-Nuvio route depends on P2P/raw-source results, the public ElfHosted instance is a poor fit for **this specific architecture**.

That is why I use Midnight here.

This does not mean ElfHosted is generally unreliable — AIOStreams describes it as a reputable, professionally hosted option.

---

## 6. Install the AIOStreams manifest in Nuvio

After creating the AIOStreams configuration:

1. Copy the generated **Manifest URL**.
2. Open Nuvio's addon/settings area.
3. Use **Install from URL** / custom addon URL, depending on your build.
4. Paste the AIOStreams manifest URL.
5. Enable the addon.

Menu names can vary across Nuvio versions, so use the current addon-management section if the wording differs.

---

## 7. Verify native resolution

Open media you are authorized to access and confirm:

- AIOStreams results appear;
- raw/P2P-compatible results are available;
- selecting one is resolved by Nuvio through the connected TorBox account;
- **Resolve playable links** is still enabled.

If P2P results appear but nothing resolves, first check the Nuvio TorBox connection rather than changing AIOStreams credentials.

---

# Route B — Nuvio with Real-Debrid or AIOStreams-managed TorBox

Use this route if native TorBox is unavailable on your build, or if you want Real-Debrid.

## 1. Configure the debrid service inside AIOStreams

### TorBox

Get the API key from:

**TorBox → Settings → API**

Enter it during the AIOStreams service-selection flow.

### Real-Debrid

Get the API key from:

https://real-debrid.com/apitoken

Choose **Real Debrid** in AIOStreams and enter that key.

Current Nuvio community docs do not list Real-Debrid as a native Connected Services debrid provider, so this AIOStreams-managed route is the practical RD setup.

---

## 2. Install the resolved AIOStreams configuration in Nuvio

Create/save the AIOStreams configuration, copy its manifest URL, and add that manifest to Nuvio.

In this architecture:

```text
AIOStreams performs debrid resolution
Nuvio receives the already-resolved playable result
```

Do not expect Nuvio's native TorBox resolver to be involved in this route.

---

# TorBox vs Real-Debrid in Nuvio

| Setup | Where credentials live | Native Nuvio resolver used? |
|---|---|---|
| Nuvio + native TorBox | Nuvio Connected Services | Yes |
| Nuvio + TorBox via AIOStreams | AIOStreams | No |
| Nuvio + Real-Debrid | AIOStreams | No |
| Nuvio + Premiumize native | Nuvio Connected Services | Yes, where supported |

---

# Buffering troubleshooting

Try these in order:

1. Try another source/file.
2. Try a smaller file or lower bitrate.
3. Compare Midnight Stable vs Nightly.
4. Test another public AIOStreams instance where your architecture allows it.
5. Check TorBox / Real-Debrid service status.
6. Verify whether the Nuvio native resolver is actually enabled when using Route A.
7. Test Ethernet or strong 5 GHz / 6 GHz Wi-Fi.
8. If your Nuvio build exposes HTTP/network options, test them conservatively.
9. Test IPv6 only as **dual-stack A/B testing**, not as a guaranteed fix.

If one public AIOStreams host buffers while another does not, the difference may be host routing/load/upstream behavior rather than Nuvio itself.

---

# Common problems

| Problem | What to check first |
|---|---|
| No AIOStreams results | Confirm the manifest is installed/enabled |
| P2P results appear but do not resolve | Native TorBox connected + **Resolve playable links** enabled |
| Using native TorBox but no raw results | Remove TorBox credentials from AIOStreams and make sure P2P is not filtered out |
| Real-Debrid missing from Nuvio Connected Services | Expected with current documented native support; configure RD in AIOStreams |
| ElfHosted gives no P2P | Expected on the public ElfHosted instance |
| Midnight Stable template seems outdated | Try Midnight Nightly |
| Everything buffers | Test provider status, file bitrate, network path, then another instance |

---

# Security notes

- Never commit API keys, manifest credentials, UUIDs, or configuration passwords.
- If using native Nuvio TorBox, keeping the TorBox key out of AIOStreams reduces the number of third parties handling that credential.
- If using a public AIOStreams instance with TorBox/RD credentials, you are trusting that instance with the configuration required to use that service.
- Self-host AIOStreams if you want maximum control.

---

# Useful links

- Nuvio: https://nuvio.tv
- Nuvio GitHub: https://github.com/NuvioMedia
- Nuvio community Wiki: https://github.com/haaihond/Nuvio-Wiki
- Nuvio debrid docs: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/debrid.md
- Nuvio addon docs: https://github.com/haaihond/Nuvio-Wiki/blob/main/docs/integrations/addons.md
- AIOStreams docs: https://docs.aiostreams.viren070.me/
- AIOStreams public instances: https://docs.aiostreams.viren070.me/getting-started/public-instances/
- TorBox: https://torbox.app/
- Real-Debrid: https://real-debrid.com/
