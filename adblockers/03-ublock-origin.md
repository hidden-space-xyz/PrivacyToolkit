**[🏠 Guide index](README.md)** · Chapter 3 of 9

# 3. 🧩 uBlock Origin

## 3.1. Keep the Default Configuration

Open:

<kbd>uBO</kbd> → <kbd>Dashboard</kbd> → <kbd>Filter lists</kbd>

uBlock Origin already ships with an excellent baseline.

Do not rebuild it from scratch unless you have a specific reason to do so.

This guide defines an **exact set** of lists for uBlock Origin. The sections below build it up piece by piece; [3.7. Final Configuration](#37--final-configuration) states the finished set in one place.

### 🧱 Built-in — the five uBlock filters lists

* ✅ **uBlock filters – Ads**
* ✅ **uBlock filters – Badware risks**
* ✅ **uBlock filters – Privacy**
* ✅ **uBlock filters – Quick fixes**
* ✅ **uBlock filters – Unbreak**

> [!CAUTION]
> **Do not disable `Quick fixes` or `Unbreak`.**
>
> Aggressive blocking also requires rules designed to **repair website breakage**, not just additional blocking rules.

### 🌐 General-purpose lists — enable exactly these

| Category | List |
| -------- | ---- |
| 📢 **Ads** | ✅ **EasyList** |
| 🕵️ **Privacy** | ✅ **EasyPrivacy** |
| 🦠 **Malware protection, security** | ✅ **Online Malicious URL Blocklist** |
| 🧰 **Multipurpose** | ✅ **Peter Lowe's Ad and tracking server list** |

No other entry in these categories should be enabled.

---

## 3.2. 🌍 Regional Lists

Under **Regions, languages**, enable the lists that match the languages you actually browse.

For Spanish, enable both:

* ✅ **EasyList Spanish**
* ✅ **AdGuard Spanish/Portuguese**

There is little value in enabling regional lists for languages you rarely or never use, and every extra list is one more candidate to check when a page breaks. Leave the rest of the category disabled.

---

## 3.3. 🔗 URL Tracking Protection

Under **Privacy**, enable:

* ✅ **AdGuard/uBO – URL Tracking Protection**

This list can remove common tracking parameters such as:

```text
utm_source
utm_campaign
fbclid
gclid
msclkid
```

Conceptually:

```diff
- https://example.com/article?utm_source=newsletter&utm_campaign=summer
+ https://example.com/article
```

This addresses a different tracking mechanism from conventional ad or domain blocking, so it is a useful addition.

---

## 3.4. 🍪 Cookie Notices and Other Annoyances

uBO groups these filters into three categories:

* 🍪 **Cookie notices**;
* 👥 **Social widgets**;
* 🧹 **Annoyances**.

In this guide, **all three categories stay empty**. Leave every list in them disabled.

Annoyance filtering is the most cosmetic and the most breakage-prone part of a blocker's ruleset, and it is the part that buys the least in return. Keeping these categories off is what makes the rest of the configuration cheap to troubleshoot: when a page misbehaves, the cause is a network rule you can find in the Logger, not a hidden element.

> [!NOTE]
> Hiding a consent banner does **not necessarily mean that consent has been actively rejected**.
>
> Annoyance filters are interface-cleanup tools, not a substitute for browser privacy controls or explicit consent handling — another reason not to rely on them here.

> [!TIP]
> If you decide you want a specific annoyance category anyway, enable **one** list, live with it for a while, and treat it as a deliberate departure from this guide. Do not enable the categories wholesale.

---

## 3.5. 🏠 Local Network Protection

Under **Privacy**, enable:

* ✅ **Block Outsider Intrusion into LAN**

This protects against websites attempting to interact with resources on private network ranges such as:

```text
192.168.x.x
10.x.x.x
172.16.x.x – 172.31.x.x
```

<details>
<summary><strong>⚠️ When can this cause problems?</strong></summary>

It may interfere with browser-based access to legitimate local services such as:

* Home Assistant;
* Jellyfin;
* NAS dashboards;
* router interfaces;
* printers;
* development servers;
* self-hosted web applications;
* other local administration panels.

If you regularly access local services from the browser, be prepared to create narrow exceptions.

</details>

---

## 3.6. 🧱 External Lists — Default Full Profile

Import these three lists in the browser by default:

```text
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Dandelion%20Sprout%27s%20Anti-Malware%20List.txt
```

| List                          | Purpose                                                |
| ----------------------------- | ------------------------------------------------------ |
| **HaGeZi Multi PRO++ — Full** | Ads, tracking, telemetry, affiliate infrastructure, and other unwanted domains |
| **HaGeZi TIF — Full**         | Malware, phishing, scams, and malicious infrastructure |
| **Dandelion Sprout Anti-Malware** | Malware redirection chains, domain-parking schemes, PUP nags, and related scam infrastructure |

> [!IMPORTANT]
> **PRO++ Full + TIF Full + Dandelion Sprout Anti-Malware is the normal browser configuration in this guide.**
>
> Do not choose smaller variants merely to save resources on paper. Keep the full lists unless they cause an observable performance or stability problem on that device.

> [!CAUTION]
> **Use the browser version of the Dandelion Sprout list here.**
>
> The URL above is the uBlock Origin version, which is also the most frequently updated one. The DNS variant (`AntiMalwareAdGuardHome.txt`) belongs in [5.3. 🦠 Dandelion Sprout Anti-Malware](05-adguard-home.md#53--dandelion-sprout-anti-malware) and must not be imported here.

### 🪶 Performance fallback

Only if the full profile causes real performance problems, replace **both** full HaGeZi lists with this single reduced profile:

```text
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.mini.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.medium.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Dandelion%20Sprout%27s%20Anti-Malware%20List.txt
```

| List                           | Role in the fallback profile |
| ------------------------------ | ---------------------------- |
| **HaGeZi Multi PRO++ — Mini**  | Reduced-size PRO++ variant   |
| **HaGeZi TIF — Medium**        | Reduced-size TIF variant     |
| **Dandelion Sprout Anti-Malware** | Unchanged — the same list and URL as in the default profile |

> [!WARNING]
> Do not treat this as an alternative preference profile. It is only a resource fallback for systems that cannot run PRO++ Full + TIF Full comfortably.
>
> **Only the two HaGeZi lists are downgraded.** Dandelion Sprout Anti-Malware is comparatively small and stays in both profiles.

> [!IMPORTANT]
> All manually imported external list URLs in this guide point to **`raw.githubusercontent.com`**.

---

## 3.7. 📋 Final Configuration

This is the **complete** uBlock Origin configuration in this guide. Every list is shown by the category uBO files it under, and nothing outside this tree should be enabled:

```text
uBlock Origin — Filter lists
│
├── 🧱 Built-in
│   ├── uBlock filters – Ads
│   ├── uBlock filters – Badware risks
│   ├── uBlock filters – Privacy
│   ├── uBlock filters – Quick fixes
│   └── uBlock filters – Unbreak
│
├── 📢 Ads
│   └── EasyList
│
├── 🕵️ Privacy
│   ├── EasyPrivacy
│   ├── AdGuard/uBO – URL Tracking Protection
│   └── Block Outsider Intrusion into LAN
│
├── 🦠 Malware protection, security
│   └── Online Malicious URL Blocklist
│
├── 🧰 Multipurpose
│   └── Peter Lowe's Ad and tracking server list
│
├── 🍪 Cookie notices ......... none
├── 👥 Social widgets ......... none
├── 🧹 Annoyances ............. none
│
├── 🌍 Regions, languages
│   ├── EasyList Spanish
│   └── AdGuard Spanish/Portuguese
│
└── 🔥 Custom
    ├── Dandelion Sprout's Anti-Malware List
    ├── HaGeZi's Pro++ DNS Blocklist
    └── HaGeZi's Threat Intelligence Feeds DNS Blocklist
```

> [!IMPORTANT]
> **This is a closed set.** The lists above enabled, every other list disabled, those three imported URLs, nothing else.
>
> Work through each category and confirm its end state directly, rather than assuming a list is already in the right position.

> [!NOTE]
> **Custom always holds exactly these three entries.** Switching to the [performance fallback](#-performance-fallback) changes *which* HaGeZi lists occupy two of them — Full by default, reduced only when needed — not how many entries there are. Dandelion Sprout Anti-Malware is the same list in both profiles.
>
> The regional entries follow the languages you browse; for Spanish that is the two lists shown above.

---

## 3.8. 🧨 Dynamic Filtering

uBlock Origin supports much more restrictive configurations, including:

* *medium mode*;
* *hard mode*;
* dynamic filtering;
* per-domain rules;
* stricter script and frame policies.

These modes are powerful, but they should not be part of a general-purpose recommendation.

> [!WARNING]
> Dynamic filtering requires active maintenance and per-site decisions.
>
> If you are not prepared to maintain those rules, a well-designed static configuration is preferable to a poorly maintained advanced mode.

---

| ⬅️ Previous | 🏠 Index | Next ➡️ |
|:----------- |:--------:| ---------:|
| **[2. Quick Configuration](02-quick-configuration.md)** | **[All chapters](README.md)** | **[4. Brave Shields](04-brave-shields.md)** |
