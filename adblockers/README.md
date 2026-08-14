# 🛡️ Ad, Tracker & Threat Blocking Guide

DNS filtering and browser-level filtering are **complementary layers, not alternatives**. This guide describes one coherent setup that combines both: **uBlock Origin** or **Brave Shields** in the browser, and **AdGuard Home** on the network.

Each chapter is a separate document so you can read only what applies to your setup.

---

## 📑 Contents

| # | Document | What it covers |
| - | -------- | -------------- |
| 1 | [🧱 Recommended Architecture](01-architecture.md) | Why DNS and browser filtering solve different problems, and how a request flows through both layers |
| 2 | [⚡ Quick Configuration](02-quick-configuration.md) | The default profile (PRO++ Full + TIF Full) and the single performance fallback |
| 3 | [🧩 uBlock Origin](03-ublock-origin.md) | Built-in lists, regional lists, URL tracking protection, annoyances, external lists, dynamic filtering |
| 4 | [🦁 Brave Shields](04-brave-shields.md) | Aggressive mode, filter lists, regional coverage, external profile, avoiding duplicate blockers |
| 5 | [🌐 AdGuard Home](05-adguard-home.md) | DNS blocklists, recommended profile, what not to import, encrypted upstreams, DNSSEC |
| 6 | [🚧 Preventing AdGuard Home Bypass](06-bypass-prevention.md) | DHCP, port `53`, DoT/DoH, and how far you want to enforce local DNS |
| 7 | [🔍 Troubleshooting and False Positives](07-troubleshooting.md) | Diagnosing breakage per tool and writing the narrowest possible exception |
| 8 | [✅ Verification](08-verification.md) | Per-layer checklists, including devices outside the browser |
| 9 | [🔧 Maintenance](09-maintenance.md) | When to review the setup and the performance downgrade rule |

---

## 🚀 Start here

If you are configuring this from scratch, read in order:

1. [Recommended Architecture](01-architecture.md) — understand what each layer can and cannot see.
2. [Quick Configuration](02-quick-configuration.md) — pick the profile.
3. Then only the tool chapters you actually use: [uBlock Origin](03-ublock-origin.md), [Brave Shields](04-brave-shields.md), [AdGuard Home](05-adguard-home.md).
4. Keep [Troubleshooting](07-troubleshooting.md) at hand for the first weeks.

---

## ✅ Default profile at a glance

| Tool              | Configuration                                                                  |
| ----------------- | ------------------------------------------------------------------------------ |
| **uBlock Origin** | Default lists + regional lists + URL Tracking Protection + PRO++ Full + TIF Full |
| **Brave Shields** | Aggressive mode + regional lists + URL Tracking Protection + PRO++ Full + TIF Full |
| **AdGuard Home**  | HaGeZi Multi PRO++ Full + TIF Full + Dandelion Sprout Anti-Malware           |

> [!IMPORTANT]
> **Start with and keep PRO++ Full + TIF Full.**
>
> Switch to the reduced fallback profile only if the device or server shows a real performance problem. See [Quick Configuration](02-quick-configuration.md) for the full rule and [Maintenance](09-maintenance.md) for the downgrade policy.

---

➡️ Start reading: [1. 🧱 Recommended Architecture](01-architecture.md)
