**[🏠 Guide index](README.md)** · Chapter 4 of 9

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

This guide defines an **exact set** of catalog entries and imported URLs for Brave. The sections below build it up piece by piece; [4.6. Default Profile](#46--default-pro-full--tif-full-profile) states the finished set in one place.

---

## 4.3. 🌍 Regional Coverage

**Always enable the regional lists for the languages you actually browse.** They are part of the default profile, not an optional extra: Brave's built-in lists cover English-language advertising far better than anything else, and regional sites are the gap they leave.

Brave's catalog uses **its own titles**, which do not match the names uBlock Origin gives the same sources. For Spanish, enable both:

| Brave catalog title | Underlying source |
| ------------------- | ----------------- |
| ✅ **Spanish website ad blocker** | EasyList Spanish |
| ✅ **Spanish and Portuguese website ad blocker** | AdGuard Spanish/Portuguese |

> [!TIP]
> Do not search the catalog for `EasyList Spanish` — you will not find it. Brave lists these entries by language, in the form `<Language> website ad blocker`.

Enable the equivalent entries for any other language you browse regularly. There is little value in enabling regional lists for languages you never use.

Always prefer Brave's built-in catalog entry over manually importing the same list's URL.

---

## 4.4. 🔗 URL Tracking Protection

**Always enable:**

* ✅ **Tracking URL blocker**

It is backed by the AdGuard URL Tracking filter, which strips tracking parameters such as `utm_source`, `fbclid`, or `gclid` from the URLs you load.

Brave also includes its own mechanisms for stripping selected tracking parameters, so treat this as a complementary layer rather than the sole source of URL cleanup.

---

## 4.5. 🧹 Annoyance Filters

**Always enable:**

* ✅ **Annoying distractions blocker**

It bundles Fanboy's Annoyance list together with the uBlock Origin annoyances and cookie-notice filters, which makes it the single broadest annoyance source in the catalog — including coverage of cookie notices.

### 🚫 Everything else stays off

This guide uses a **closed set** of Brave filters: the entries listed in [4.6. Default Profile](#46--default-pro-full--tif-full-profile) and nothing more.

Every other entry in the catalog must end up **disabled** — the narrower annoyance blockers for newsletter popups, social media, chat apps, AI suggestions, cookie notices, mobile app promos, and YouTube elements included. Much of their coverage already lives inside *Annoying distractions blocker*, and each additional entry adds one more candidate to check when a page breaks.

> [!IMPORTANT]
> Go through the catalog and confirm the end state directly, rather than assuming an entry is already in the right position. Which entries a fresh Brave ships enabled is a moving target; the configuration in this guide is not.

> [!NOTE]
> Brave's own core filters are always active and are **not exposed as toggles** in the catalog. The closed-set rule governs the entries you can actually switch and the URLs you import — not Brave's built-in baseline.

> [!TIP]
> With this configuration, *Annoying distractions blocker* is the only annoyance source you have enabled. If a page loses an important dialog, button, or form, it is the first thing to toggle off when testing.

---

## 4.6. 🧱 Default PRO++ Full + TIF Full Profile

Import the same **full** browser lists used with uBlock Origin:

```text
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Dandelion%20Sprout%27s%20Anti-Malware%20List.txt
```

> [!CAUTION]
> **Use the browser version of the Dandelion Sprout list here.**
>
> Brave Shields consumes browser filter syntax, so it takes the same uBlock Origin version used in [3.6. 🧱 External Lists](03-ublock-origin.md#36--external-lists--default-full-profile). The DNS variant (`AntiMalwareAdGuardHome.txt`) belongs only in [5.3. 🦠 Dandelion Sprout Anti-Malware](05-adguard-home.md#53--dandelion-sprout-anti-malware).

### Normal result

This is the **complete** Brave configuration in this guide. Nothing outside this tree should be enabled:

```text
Brave Shields
│
├── 🛡️ Trackers & ads: Aggressive
│
├── ✅ Catalog entries — enabled, and only these
│   ├── 🌍 Regional lists for the languages you browse
│   │   ├── Spanish website ad blocker
│   │   └── Spanish and Portuguese website ad blocker
│   ├── 🔗 Tracking URL blocker
│   └── 🧹 Annoying distractions blocker
│
├── 🚫 Every other catalog entry — disabled
│
└── 🔥 Imported lists — these three, and only these
    ├── HaGeZi Multi PRO++ — Full
    ├── HaGeZi TIF — Full
    └── Dandelion Sprout Anti-Malware
```

> [!IMPORTANT]
> **This is a closed set, in both directions.** The catalog entries listed above enabled, every other one disabled, those three imported URLs, nothing else.
>
> Work through the catalog and confirm each position rather than trusting what a fresh installation happens to ship with.
>
> Brave's built-in core filters are not toggleable and are unaffected by this rule — see [4.5](#45--annoyance-filters).

> [!NOTE]
> **Brave always holds exactly these three imported URLs.** Switching to the [performance fallback](#-performance-fallback) below changes *which* HaGeZi lists occupy two of them — Full by default, reduced only when needed — not how many there are. Dandelion Sprout Anti-Malware is the same list in both profiles.

Keep this configuration unless Brave shows an actual resource or stability problem attributable to the list size.

### 🪶 Performance fallback

If the full profile causes real performance problems, replace both HaGeZi lists with:

```text
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.mini.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.medium.txt
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Dandelion%20Sprout%27s%20Anti-Malware%20List.txt
```

```text
Brave Shields — performance fallback
│
├── HaGeZi Multi PRO++ — Mini
├── HaGeZi TIF — Medium
└── Dandelion Sprout Anti-Malware
```

> [!WARNING]
> This is the **only reduced Brave profile** in the guide. Do not use it unless the full profile creates a measurable performance or stability issue.
>
> **Only the two HaGeZi lists are downgraded.** Dandelion Sprout Anti-Malware stays in both profiles.

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

| ⬅️ Previous | 🏠 Index | Next ➡️ |
|:----------- |:--------:| ---------:|
| **[3. uBlock Origin](03-ublock-origin.md)** | **[All chapters](README.md)** | **[5. AdGuard Home](05-adguard-home.md)** |
