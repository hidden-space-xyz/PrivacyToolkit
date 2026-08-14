**[🏠 Guide index](README.md)** · Chapter 2 of 9

# 2. ⚡ Quick Configuration

This guide has **one recommended default profile** and **one performance fallback**.

The rule is simple:

> **Start with and keep PRO++ Full + TIF Full.**
>
> Only switch to the performance fallback if the device or server shows real performance problems such as excessive memory use, very slow filter reloads, browser instability, or clearly degraded responsiveness.

## ✅ Default profile — use this first

| Tool              | Configuration                                                                  |
| ----------------- | ------------------------------------------------------------------------------ |
| **uBlock Origin** | Built-in lists + regional lists + URL Tracking Protection + LAN protection + PRO++ Full + TIF Full + Dandelion Sprout Anti-Malware — **and nothing else** |
| **Brave Shields** | Aggressive mode + regional lists + Tracking URL blocker + Annoying distractions blocker + PRO++ Full + TIF Full + Dandelion Sprout Anti-Malware — **and nothing else** |
| **AdGuard Home**  | HaGeZi Multi PRO++ Full + TIF Full + Dandelion Sprout Anti-Malware           |

The default external profile is:

* **HaGeZi Multi PRO++ — Full**
* **HaGeZi Threat Intelligence Feeds — TIF Full**
* **Dandelion Sprout Anti-Malware**

This is the profile users should normally run in both the browser and DNS layers.

## 🪶 Performance fallback — only when necessary

If the full profile causes measurable performance problems, replace the two HaGeZi lists with this **single reduced profile**:

* **HaGeZi Multi PRO++ — Mini**
* **HaGeZi Threat Intelligence Feeds — TIF Medium**
* **Dandelion Sprout Anti-Malware** — unchanged

Do not reduce the lists pre-emptively. Do not choose intermediate combinations. In this guide, the reduced profile exists only as a fallback for hardware or browser resource limitations.

> [!NOTE]
> **The fallback only downgrades HaGeZi.** Dandelion Sprout Anti-Malware is part of both the default and the reduced profile in all three tools. It is comparatively small, so removing it saves little and costs a security-oriented source.

### 🦠 Two versions of the Dandelion Sprout list

The list ships in engine-specific variants. Import the one that matches the layer:

| Layer | URL |
| ----- | --- |
| 🧩 uBlock Origin · 🦁 Brave Shields | `https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Dandelion%20Sprout%27s%20Anti-Malware%20List.txt` |
| 🌐 AdGuard Home | `https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareAdGuardHome.txt` |

> [!CAUTION]
> **Do not swap these two URLs.** The browser version uses full request context that a DNS resolver cannot evaluate; the DNS version is rewritten as domain-oriented rules. Each engine must receive the syntax it can actually interpret.

### External list policy

All manually imported external lists in this guide are loaded directly from their source repository on **`raw.githubusercontent.com`**, tracking each project's default branch so the URL always serves the current version of the list.

> [!WARNING]
> **PRO++ Full and TIF Full are intentionally heavy and aggressive.**
>
> Higher memory usage and longer list reloads are expected compared with the fallback profile. That alone is not a reason to downgrade unless it creates an actual usability or stability problem.

---

## 🔗 Where to apply this profile

| Layer | Section with the exact URLs |
| ----- | --------------------------- |
| 🧩 uBlock Origin | [3.6. External Lists — Default Full Profile](03-ublock-origin.md#36--external-lists--default-full-profile) |
| 🦁 Brave Shields | [4.6. Default PRO++ Full + TIF Full Profile](04-brave-shields.md#46--default-pro-full--tif-full-profile) |
| 🌐 AdGuard Home | [5.4. Recommended AdGuard Home Profile](05-adguard-home.md#54--recommended-adguard-home-profile) |

The downgrade decision itself is covered in [9. 🔧 Maintenance](09-maintenance.md).

---

| ⬅️ Previous | 🏠 Index | Next ➡️ |
|:----------- |:--------:| ---------:|
| **[1. Recommended Architecture](01-architecture.md)** | **[All chapters](README.md)** | **[3. uBlock Origin](03-ublock-origin.md)** |
