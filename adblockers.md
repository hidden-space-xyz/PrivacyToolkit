# 🛡️ Ad, Tracker & Threat Blocking Guide

![uBlock Origin](https://img.shields.io/badge/uBlock%20Origin-local%20filtering-800000)
![Brave Shields](https://img.shields.io/badge/Brave%20Shields-local%20filtering-FB542B)
![AdGuard Home](https://img.shields.io/badge/AdGuard%20Home-DNS%20filtering-68BC71)
![Last reviewed](https://img.shields.io/badge/last%20reviewed-August%202026-555555)

> [!NOTE]
> This guide focuses **exclusively on content-blocking configuration**.
>
> Browser selection, browser privacy settings, operating-system hardening, password management, and similar topics should be handled separately.

This setup uses three complementary filtering layers:

| Layer          | Tool          | Main purpose                                      |
| -------------- | ------------- | ------------------------------------------------- |
| 🌐 **DNS**     | AdGuard Home  | Network-wide domain blocking                      |
| 🧩 **Browser** | uBlock Origin | Precise network, cosmetic, and advanced filtering |
| 🦁 **Browser** | Brave Shields | Built-in filtering for Brave                      |

> [!IMPORTANT]
> **More filter lists do not automatically mean better protection.**
>
> The goal is to use a small number of reliable lists in the layer where they make the most sense.

---

## 📑 Table of Contents

* [1. Recommended architecture](#1--recommended-architecture)
* [2. Quick configuration](#2--quick-configuration)
* [3. uBlock Origin](#3--ublock-origin)
* [4. Brave Shields](#4--brave-shields)
* [5. AdGuard Home](#5--adguard-home)
* [6. Preventing AdGuard Home bypass](#6--preventing-adguard-home-bypass)
* [7. Troubleshooting and false positives](#7--troubleshooting-and-false-positives)
* [8. Verification](#8--verification)
* [9. Maintenance](#9--maintenance)
* [10. Common mistakes](#10--common-mistakes)
* [11. Final recommended configurations](#11--final-recommended-configurations)

---

# 1. 🧱 Recommended Architecture

DNS filtering and browser-level filtering are **complementary layers, not alternatives**.

Each layer sees different information and therefore solves different problems.

## 🌐 AdGuard Home

AdGuard Home operates primarily at the **DNS/domain level**.

It is particularly useful for:

* applications without their own content blocker;
* smartphones and tablets;
* Smart TVs;
* game consoles;
* IoT devices;
* operating-system and application telemetry;
* advertising and tracking domains;
* known malicious, phishing, and scam domains.

However, DNS filtering cannot inspect the full URL or modify the page itself.

It cannot reliably distinguish between:

```text
example.com/ads/banner.js
```

and:

```text
example.com/article
```

because both requests ultimately resolve the same hostname:

```text
example.com
```

---

## 🧩 uBlock Origin and Brave Shields

Browser-level blockers have much more context.

They can evaluate:

* the full URL;
* the page that initiated the request;
* first-party vs. third-party requests;
* resource type;
* scripts;
* images;
* iframes;
* XHR/fetch requests;
* page elements.

They can also perform tasks that DNS filtering cannot, such as:

* cosmetic filtering;
* scriptlet injection;
* URL parameter removal;
* per-site exceptions;
* contextual network filtering.

---

## 🔄 Simplified request flow

```mermaid
flowchart TD
    A["🌐 Page requests a resource"] --> B{"🧩 uBO / Brave Shields"}
    B -->|"Blocked"| X["🛑 Request stops here"]
    B -->|"Allowed"| C{"🌐 AdGuard Home"}
    C -->|"Domain blocked"| Y["🛑 DNS resolution denied"]
    C -->|"Allowed"| D["🔐 Connection to server"]
    D --> E["🧹 Cosmetic filtering / scriptlets"]
    E --> F["✅ Final page"]

    G["📱 Apps · Smart TVs · IoT · OS"] --> C
```

> [!TIP]
> The browser performs the **fine-grained filtering**.
>
> AdGuard Home provides **broad network coverage** for traffic that never passes through a browser extension or built-in browser blocker.

This redundancy is useful.

Blindly duplicating millions of domain rules across every layer usually is not.

---

# 2. ⚡ Quick Configuration

If you do not need the detailed explanation, use one of these two profiles.

## 🟢 Balanced

Recommended for most users.

| Tool              | Configuration                                            |
| ----------------- | -------------------------------------------------------- |
| **uBlock Origin** | Default lists + regional lists + URL Tracking Protection |
| **Brave Shields** | Aggressive mode + regional lists                         |
| **AdGuard Home**  | HaGeZi Multi PRO + TIF + Dandelion Sprout Anti-Malware   |

### Advantages

* very good overall coverage;
* few false positives;
* low maintenance;
* straightforward troubleshooting;
* modest resource usage.

---

## 🔴 Strict

For users who are comfortable diagnosing occasional breakage.

| Tool              | Configuration                                            |
| ----------------- | -------------------------------------------------------- |
| **uBlock Origin** | Balanced setup + HaGeZi Pro++ Mini + TIF Medium          |
| **Brave Shields** | Balanced setup + HaGeZi Pro++ Mini + TIF Medium          |
| **AdGuard Home**  | HaGeZi Multi PRO++ + TIF + Dandelion Sprout Anti-Malware |

> [!WARNING]
> **PRO++ is intentionally aggressive.**
>
> It may block telemetry, affiliate infrastructure, redirectors, analytics endpoints, or auxiliary services that some websites rely on.

---

# 3. 🧩 uBlock Origin

## 3.1. Keep the Default Configuration

Open:

<kbd>uBO</kbd> → <kbd>Dashboard</kbd> → <kbd>Filter lists</kbd>

uBlock Origin already ships with an excellent baseline.

Do not rebuild it from scratch unless you have a specific reason to do so.

### Important built-in lists

* ✅ **uBlock filters – Ads**
* ✅ **uBlock filters – Badware risks**
* ✅ **uBlock filters – Privacy**
* ✅ **uBlock filters – Quick fixes**
* ✅ **uBlock filters – Unbreak**

> [!CAUTION]
> **Do not disable `Quick fixes` or `Unbreak`.**
>
> Aggressive blocking also requires rules designed to **repair website breakage**, not just additional blocking rules.

---

## 3.2. 🌍 Regional Lists

Enable the regional lists that match the languages you actually browse.

For Spanish-language websites, for example:

* ✅ **EasyList Spanish**
* ✅ **AdGuard Spanish/Portuguese**

There is little value in enabling regional lists for languages you rarely or never use.

---

## 3.3. 🔗 URL Tracking Protection

Enable:

> **AdGuard/uBO – URL Tracking Protection**

This category can remove common tracking parameters such as:

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

uBO provides optional filters for categories such as:

* cookie notices;
* social widgets;
* newsletter prompts;
* notification requests;
* pop-ups;
* other annoyances.

A sensible approach is:

> **Enable only the categories you actually want removed.**

> [!NOTE]
> Hiding a consent banner does **not necessarily mean that consent has been actively rejected**.
>
> Annoyance filters should primarily be treated as interface-cleanup tools rather than as a substitute for browser privacy controls or explicit consent handling.

More cosmetic filtering can also mean more opportunities for page breakage.

---

## 3.5. 🏠 Local Network Protection

Optional:

> **Block Outsider Intrusion into LAN**

This provides additional protection against websites attempting to interact with resources on private network ranges such as:

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

## 3.6. 🧱 External Lists

Avoid loading the largest available domain lists into the browser by default.

For a strict configuration, smaller browser-oriented variants make more sense:

```text
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/pro.plus.mini.txt
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/tif.medium.txt
```

| List                  | Purpose                                                |
| --------------------- | ------------------------------------------------------ |
| **HaGeZi Pro++ Mini** | Ads, tracking, telemetry, and other unwanted domains   |
| **HaGeZi TIF Medium** | Malware, phishing, scams, and malicious infrastructure |

> [!TIP]
> Reserve extremely large domain lists for **AdGuard Home** whenever possible.
>
> Browser blockers provide more value when using their contextual capabilities than when acting as a second DNS blocklist engine.

---

<details>
<summary><strong>🦠 Dandelion Sprout Anti-Malware — optional</strong></summary>

You can also import:

```text
https://raw.githubusercontent.com/DandelionSprout/adfilt/refs/heads/master/Dandelion%20Sprout's%20Anti-Malware%20List.txt
```

This provides an additional source of malware- and scam-related filtering.

If you already use TIF and uBO's built-in security lists, treat it as an **optional additional source**, not a requirement.

</details>

---

## 3.7. 🧨 Dynamic Filtering

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

# 4. 🦁 Brave Shields

## 4.1. Main Setting

Open:

```text
brave://settings/shields
```

Set:

> **Trackers & ads blocking → Aggressive**

Aggressive mode is the most appropriate setting for a configuration focused on comprehensive content blocking.

---

## 4.2. 📚 Filter Lists

Open:

```text
brave://settings/shields/filters
```

Brave already incorporates its own filtering rules and rules derived from established filter-list projects.

> [!IMPORTANT]
> Do not manually import **EasyList, EasyPrivacy, or uAssets** merely because they are commonly used with uBO if Brave already incorporates them.
>
> Duplicating a source does not create an independent layer of protection.

---

## 4.3. 🌍 Regional Coverage

Enable the regional lists relevant to the languages you browse.

For Spanish-language websites, for example:

* **EasyList Spanish**
* **AdGuard Spanish/Portuguese**

If Brave already exposes the relevant list through its built-in catalog, prefer enabling it there instead of manually importing its URL.

---

## 4.4. 🔗 URL Tracking Protection

If available in your installation, enable:

* ✅ **Tracking URL blocker**

Brave also includes its own mechanisms for stripping selected tracking parameters, so this should be considered complementary rather than the sole source of URL cleanup.

---

## 4.5. 🧹 Annoyance Filters

Optional categories may include:

* 🍪 cookie notices;
* 💬 floating chats;
* 🔔 notification prompts;
* 📧 newsletter prompts;
* 📱 “install our app” banners;
* 👥 social widgets;
* 🪟 pop-ups.

Enable them according to your preferences.

> [!TIP]
> If a page suddenly loses an important dialog, button, or form, annoyance filters should be among the first things you investigate.

---

## 4.6. 🧱 Strict Profile

For a stricter configuration, use the same browser-oriented HaGeZi variants:

```text
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/pro.plus.mini.txt
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/tif.medium.txt
```

### Result

```text
Brave Shields
│
├── 🛡️ Trackers & ads: Aggressive
├── 🌍 Regional filters
├── 🔗 URL Tracking Protection
├── 🧹 Annoyance filters [optional]
│
└── 🔥 Strict profile
    ├── HaGeZi Pro++ Mini
    └── HaGeZi TIF Medium
```

---

## 4.7. Use One General-Purpose Browser Blocker

If Brave Shields is your general-purpose content blocker, do not add another general-purpose blocker solely in an attempt to “stack” protection.

Doing so complicates:

* exceptions;
* troubleshooting;
* rule attribution;
* breakage diagnosis.

The complementary layer should be your DNS filter, not a second browser blocker competing for the same requests.

---

# 5. 🌐 AdGuard Home

AdGuard Home is where the **heavy domain-based filtering** should normally live.

Open:

<kbd>Filters</kbd> → <kbd>DNS blocklists</kbd>

---

## 5.1. 🎚️ Choose One HaGeZi Main List

Do not stack several levels of the same HaGeZi family.

Choose one.

### 🟢 Balanced

> **HaGeZi Multi PRO**

A strong balance between coverage and compatibility.

### 🔴 Strict

> **HaGeZi Multi PRO++**

A more aggressive policy against categories such as:

* tracking;
* telemetry;
* affiliate infrastructure;
* analytics;
* advertising;
* other unwanted domains.

> [!CAUTION]
> **Do not enable PRO and PRO++ at the same time.**
>
> Choose the level that matches your preferred balance between blocking and compatibility.

---

## 5.2. ☣️ Threat Intelligence Feeds

Add:

> **HaGeZi Threat Intelligence Feeds — TIF**

TIF is primarily security-oriented and targets categories such as:

* malware;
* phishing;
* scams;
* spam;
* command-and-control infrastructure;
* other malicious domains.

### Choosing the Appropriate Size

| Server resources                 | Variant        |
| -------------------------------- | -------------- |
| 🟢 Plenty of memory              | **TIF Full**   |
| 🟡 Moderate resources            | **TIF Medium** |
| 🔵 Resource-constrained hardware | **TIF Mini**   |

> [!TIP]
> The best TIF variant is not necessarily the largest one.
>
> Use the largest version your server can handle comfortably without excessive memory use, slow filter reloads, or instability.

---

## 5.3. 🦠 Dandelion Sprout Anti-Malware

Use the AdGuard Home-specific version:

```text
https://raw.githubusercontent.com/DandelionSprout/adfilt/refs/heads/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareAdGuardHome.txt
```

> [!IMPORTANT]
> Do not accidentally use the uBO-oriented version here.
>
> Each filtering engine should receive a list in a syntax it can interpret correctly.

---

## 5.4. 📦 Recommended AdGuard Home Profiles

### 🟢 Balanced

```text
AdGuard Home
├── HaGeZi Multi PRO
├── HaGeZi TIF
└── Dandelion Sprout Anti-Malware
```

### 🔴 Strict

```text
AdGuard Home
├── HaGeZi Multi PRO++
├── HaGeZi TIF
│   └── Medium / Mini if hardware is constrained
└── Dandelion Sprout Anti-Malware
```

---

## 5.5. 🚫 What Not to Put in AdGuard Home

Avoid indiscriminately importing lists designed primarily for browser content blockers.

A DNS filter cannot meaningfully apply browser-specific rules such as:

```text
||example.com/ads/banner.js
##.advertisement
$script
$removeparam
```

Those rules depend on information that DNS does not have.

A useful rule of thumb is:

> **DNS → domain-oriented filtering.**
> **Browser → URLs, request context, cosmetic filtering, scriptlets, and precise exceptions.**

---

## 5.6. 🔐 Encrypted Upstream DNS

AdGuard Home can use encrypted upstream resolvers via:

* **DoH** — DNS over HTTPS;
* **DoT** — DNS over TLS;
* **DoQ** — DNS over QUIC.

The architecture then looks like this:

```mermaid
flowchart LR
    A["📱 Client devices"] -->|"Local DNS"| B["🛡️ AdGuard Home"]
    B -->|"DoH / DoT / DoQ"| C["🌍 Upstream resolver"]
```

This encrypts the DNS traffic between:

```text
AdGuard Home → upstream DNS resolver
```

It does not automatically encrypt ordinary DNS traffic between local clients and AdGuard Home.

For a trusted home LAN, unencrypted local DNS combined with an encrypted upstream is a perfectly reasonable design.

---

## 5.7. 🔏 DNSSEC

Check that DNSSEC validation has not been disabled in your installation.

There is no reason to toggle settings unnecessarily if your current configuration already has validation enabled and working correctly.

---

# 6. 🚧 Preventing AdGuard Home Bypass

A filtered DNS resolver can only protect traffic that actually reaches it.

---

## 6.1. 📡 DHCP

Advertise AdGuard Home as the DNS resolver through DHCP.

> [!WARNING]
> Avoid simultaneously advertising an unfiltered public resolver as a “secondary DNS server”.
>
> Many operating systems do not treat the secondary server purely as an emergency fallback and may query it directly.

---

## 6.2. 🔒 Traditional DNS

If your router or firewall supports it, either:

* block outbound TCP/UDP port `53`; or
* redirect outbound port `53` traffic to AdGuard Home.

This prevents simple bypass attempts such as:

```text
device → 8.8.8.8:53
```

---

## 6.3. 🕵️ Encrypted DNS

DoT is relatively straightforward to identify because it commonly uses port:

```text
853
```

DoH is different.

It normally travels over ordinary HTTPS:

```text
TCP/443
```

Blocking port `443` is obviously not a viable solution because it would also break normal web browsing.

<details>
<summary><strong>🔧 Networks where local DNS must be enforced</strong></summary>

If you deliberately want to prevent clients from using alternative resolvers, you can combine firewall rules with lists of known:

* public DoH resolvers;
* VPN endpoints;
* proxy services;
* DNS bypass services.

Be aware that this is an intentionally restrictive policy.

It can interfere with legitimate use of:

* VPNs;
* Tor;
* proxies;
* Private DNS;
* applications with their own resolvers.

Only implement it if enforcing the local DNS policy is actually one of your goals.

</details>

---

# 7. 🔍 Troubleshooting and False Positives

A strict configuration will eventually break something.

The difference between a maintainable setup and a frustrating one is **how you diagnose and repair those failures**.

> [!IMPORTANT]
> **Never disable an entire filter list to fix a single website unless you have determined that the list itself is unsuitable for your setup.**

---

## 🧭 Troubleshooting Flow

```mermaid
flowchart TD
    A["💥 Website breaks"] --> B{"Blocked by uBO / Shields?"}
    B -->|"Yes"| C["🔍 Inspect logger / Shields"]
    B -->|"No"| D["🌐 Inspect AdGuard Home query log"]
    C --> E["🎯 Identify domain and rule"]
    D --> E
    E --> F["➕ Create the narrowest exception possible"]
    F --> G["✅ Retest"]
    G --> H["📨 Report false positive upstream"]
```

---

## 7.1. uBlock Origin

Open the **Logger** and reproduce the problem.

You want to identify:

```text
request
   ↓
matching rule
   ↓
responsible filter list
```

### Example of a Site-Specific Exception

```text
@@||api.example.com^$domain=www.affected-site.com
```

This allows `api.example.com` only when the request originates from:

```text
www.affected-site.com
```

That is generally preferable to allowing the domain globally.

---

## 7.2. AdGuard Home

Open:

<kbd>Query Log</kbd>

Reproduce the issue and inspect the blocked domain and matching rule.

A DNS exception might look like:

```text
@@||api.example.com^
```

> [!NOTE]
> A DNS exception is inherently broader than a contextual browser exception.
>
> AdGuard Home does not know which webpage caused the DNS lookup.

---

## 7.3. Brave Shields

Temporarily disable Shields **for the affected site only**.

If the page starts working:

1. identify which filtering category is responsible;
2. create or apply the narrowest reasonable exception;
3. restore the rest of Shields.

Avoid globally weakening Shields because one website is broken.

---

## 🕵️ Common Sources of False Positives

Typical offenders include:

* 💳 payment processors;
* 🏦 anti-fraud systems;
* 🔑 federated login providers;
* 🛍️ affiliate and cashback redirectors;
* 📶 captive Wi-Fi portals;
* 🏠 local services;
* 📊 analytics endpoints that are also used as functional dependencies.

---

# 8. ✅ Verification

Do not optimize your configuration for a synthetic `100%` score.

A test page only checks the domains and techniques its author chose to include.

Passing every test does not necessarily mean your real-world configuration is better.

---

## 🧩 uBlock Origin

* [ ] The Logger shows blocked requests.
* [ ] You can identify the rule responsible for a block.
* [ ] Filter lists update successfully.
* [ ] Your normal websites still work.

---

## 🦁 Brave

* [ ] Shields is enabled.
* [ ] Trackers & ads blocking is set to **Aggressive**.
* [ ] Appropriate regional lists are enabled.
* [ ] Custom lists update correctly.
* [ ] Your normal websites still work.

---

## 🌐 AdGuard Home

* [ ] Your devices appear in the Query Log.
* [ ] DNS requests are actually reaching AdGuard Home.
* [ ] Blocked domains show the expected matching rule.
* [ ] Filter lists update successfully.
* [ ] The server is not under excessive memory pressure.

---

## 📱 Outside the Browser

* [ ] A smartphone without a content-blocking extension appears in AdGuard Home.
* [ ] A Smart TV or IoT device appears in AdGuard Home.
* [ ] Native applications generate visible DNS queries.

> [!TIP]
> Confirming that a Smart TV or native application is actually being filtered through AdGuard Home tells you far more about your DNS layer than achieving `100/100` on an ad-block testing website.

---

# 9. 🔧 Maintenance

Once configured correctly, this setup should require **very little day-to-day maintenance**.

Review it when:

* 🔴 several websites suddenly begin to break;
* 🔴 a filter list stops updating;
* 🟡 memory usage increases significantly;
* 🟡 you accumulate many manual exceptions;
* 🟡 you switch between PRO and PRO++;
* 🟢 you decide to enable additional annoyance categories.

> [!TIP]
> If one particular list repeatedly requires new exceptions, that list may simply be **too aggressive for your use case**, even if it technically blocks more domains.

---

# 10. ❌ Common Mistakes

## ❌ Adding Lists Without a Clear Purpose

More rules can mean:

* more memory usage;
* more false positives;
* harder troubleshooting;
* diminishing returns.

Every additional list should answer a specific question:

> **What does this list add that my current setup does not already cover well?**

If the answer is unclear, you probably do not need it.

---

## ❌ Running Two General-Purpose Browser Blockers

This does not make your browser “twice as protected”.

It does make troubleshooting look like this:

```text
Who blocked this?
├── Blocker A
├── Blocker B
├── DNS
└── 🤷
```

Use one general-purpose blocker in the browser.

Use AdGuard Home as the complementary network layer.

---

## ❌ Enabling HaGeZi PRO and PRO++ Together

Choose **one level**.

Do not stack both simply because both are available.

---

## ❌ Loading Full TIF Into Every Browser

Use **Medium** or **Mini** browser-oriented variants when appropriate.

Let AdGuard Home handle the heavy domain filtering.

---

## ❌ Disabling an Entire List to Fix One Domain

Find the responsible rule and create the narrowest exception possible.

---

## ❌ Importing Browser-Oriented Lists Into DNS Filtering

Use lists intended for DNS whenever possible.

Browser filtering syntax and DNS filtering syntax solve different problems.

---

## ❌ Enabling Every Annoyance Filter by Default

Annoyance filters are useful, but they can also hide legitimate interface elements.

Enable the categories you actually want.

---

## ❌ Optimizing for a Test Website

Optimize for:

1. **real-world coverage**;
2. **low false-positive rates**;
3. **low maintenance**;
4. **easy troubleshooting**.

---

# 11. 🏁 Final Recommended Configurations

## 🟢 Balanced

```text
🧩 uBlock Origin
├── Default filter lists
├── Relevant regional lists
├── AdGuard/uBO URL Tracking Protection
├── Selected annoyance filters [optional]
└── Block Outsider Intrusion into LAN [optional]

🦁 Brave Shields
├── Trackers & ads: Aggressive
├── Relevant regional lists
├── URL Tracking Protection
└── Selected annoyance filters [optional]

🌐 AdGuard Home
├── HaGeZi Multi PRO
├── HaGeZi TIF
└── Dandelion Sprout Anti-Malware
```

---

## 🔴 Strict

```text
🧩 uBlock Origin / 🦁 Brave Shields
├── Balanced configuration
├── HaGeZi Pro++ Mini
└── HaGeZi TIF Medium

🌐 AdGuard Home
├── HaGeZi Multi PRO++
├── HaGeZi TIF
│   └── Medium / Mini if hardware is constrained
└── Dandelion Sprout Anti-Malware
```

---

> [!IMPORTANT]
>
> ## Rule of Thumb
>
> **Use DNS for heavy domain-level filtering.**
>
> **Use the browser blocker for context, URLs, cosmetic filtering, scriptlets, and precise exceptions.**
>
> A short, understandable, and easy-to-debug configuration is usually better than a huge collection of overlapping lists that nobody can explain.

---

<details>
<summary><strong>📌 One-sentence summary</strong></summary>

**uBlock Origin or Brave Shields handles the fine-grained browser filtering; AdGuard Home provides network-wide coverage; HaGeZi strengthens domain-level filtering; and narrow exceptions keep the whole setup maintainable.**

</details>
