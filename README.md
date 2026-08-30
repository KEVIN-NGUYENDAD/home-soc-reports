# home-soc-reports

Sanitized Home SOC status feed. Read by a Claude Scheduled Task to generate the daily
🏠 Home Security Bulletin.

This repo is a **publication surface**, not a data store. It holds exactly three files,
always overwritten in place, never appended.

---

## Files

| File | Purpose |
|---|---|
| `ROUTER-SECURITY-AUDIT-LATEST.md` | Human-readable network audit narrative |
| `BASELINE-LATEST.json` | Machine-readable control states + alerts |
| `DEVICE-SUMMARY.json` | Device counts and per-device status |

Filenames are **fixed**. No dates in filenames — `LATEST` always means current.
This removes the need for the reader to glob or sort by timestamp.

---

## Sanitization rules (enforced before every push)

**Never publish:**

- Passwords, tokens, API keys, secrets of any kind
- Full or partial MAC addresses
- Internal IP addresses (any octet)
- Public IP address
- Router make, model, or firmware version
- SSID names
- Serial numbers, device fingerprints
- Exact geolocation
- Raw port numbers for internal services

**Publish instead:**

| Instead of | Publish |
|---|---|
| `192.168.0.233` | `link: wifi-2.4ghz` |
| `9c:b1:50:xx:xx:xx` | `id: desktop-01` |
| `ARRIS CGM4331COM v23.2` | `firmware: current` |
| `Reolink RLC-810A` | `label: Indoor Camera`, `category: iot` |
| `port 1883 open` | `local message-broker port, LAN-only` |

Rule of thumb: publish **states and verdicts**, never **identifiers and addresses**.
A reader should be able to tell whether the network is healthy, and unable to tell
which network it is.

---

## How it works

Every file in this repo is written by `export-home-soc-reports.js`, which lives in the
private repo. Nothing here is edited by hand.

```
PRIVATE  mcp-cyber-tools
┌──────────────────────────────────────────────┐
│  network-scan-data/network-scan-*.json       │  device inventory, open ports
│  laptop-collection-data/*.json               │  DNS, WiFi, host state
│  baseline/BASELINE-*.json                    │  approved baseline
│  state.json + baseline.json  (optional)      │  security-watch control states
└──────────────────────────────────────────────┘
                     │  newest of each type
                     ▼
        export-home-soc-reports.js
                     │
                     ├── classify   addresses → link type
                     │              MAC       → device id  (gateway-01, camera-01)
                     │              vendor    → discarded
                     │              model/fw  → discarded
                     │              port      → service class (web-ui, video-stream…)
                     │              resolvers → provider class (isp_default…)
                     │
                     ├── derive     alerts from control changes + LAN remote-access
                     │              risk level GREEN / YELLOW / RED
                     │              data_age_hours + stale flag
                     │
                     └── LEAK GUARD  regex sweep over the exact output bytes
                                     MAC · IPv4 · IPv6 · credential keywords ·
                                     private-key blocks · vendor names · SSID
                                     any hit → abort, write nothing, push nothing
                     │
                     ▼
PUBLIC  home-soc-reports
┌──────────────────────────────────────────────┐
│  ROUTER-SECURITY-AUDIT-LATEST.md             │
│  BASELINE-LATEST.json                        │
│  DEVICE-SUMMARY.json                         │
└──────────────────────────────────────────────┘
                     │  git add -f · commit · push origin main
                     ▼
        Claude Scheduled Task — daily 20:10
        fetches the three raw.githubusercontent.com URLs
                     │
                     ▼
            🏠 Home Security Bulletin  →  Email
```

**Two properties worth knowing:**

*Unknown is reported as unknown.* A control with no collector output is published as
`state: "unknown"` and shown as `NO DATA` in the audit, never as a pass. The bulletin
therefore cannot mistake a coverage gap for a clean result.

*The leak guard is a gate, not a filter.* It does not scrub — it aborts. If any output
byte still matches an identifier pattern, the export stops before writing and before
pushing. A partial or half-sanitized publish is not reachable.

The private repo keeps the full, unsanitized data and all tooling. Only the projection
lands here.

---

## Raw URLs used by the scheduled task

```
https://raw.githubusercontent.com/KEVIN-NGUYENDAD/home-soc-reports/main/ROUTER-SECURITY-AUDIT-LATEST.md
https://raw.githubusercontent.com/KEVIN-NGUYENDAD/home-soc-reports/main/BASELINE-LATEST.json
https://raw.githubusercontent.com/KEVIN-NGUYENDAD/home-soc-reports/main/DEVICE-SUMMARY.json
```

---

## Freshness contract

Every file carries a timestamp (`generated_at` / `approved_at` / audit date).
If the newest timestamp is more than **48 hours** old, the bulletin must report
`Dữ liệu cũ — collector có thể đã dừng` rather than presenting stale state as current.
