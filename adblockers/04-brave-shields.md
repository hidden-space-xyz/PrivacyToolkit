[🏠 Guide index](README.md) · Part 4 of 9

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

## 4.6. 🧱 Default PRO++ Full + TIF Full Profile

Import the same **full** browser lists used with uBlock Origin:

```text
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/pro.plus.txt
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/tif.txt
```

### Normal result

```text
Brave Shields
│
├── 🛡️ Trackers & ads: Aggressive
├── 🌍 Regional filters
├── 🔗 URL Tracking Protection
├── 🧹 Annoyance filters [optional]
│
└── 🔥 Default external profile
    ├── HaGeZi Multi PRO++ — Full
    └── HaGeZi TIF — Full
```

Keep this configuration unless Brave shows an actual resource or stability problem attributable to the list size.

### 🪶 Performance fallback

If the full profile causes real performance problems, replace both HaGeZi lists with:

```text
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/pro.plus.mini.txt
https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/tif.medium.txt
```

```text
Brave Shields — performance fallback
│
├── HaGeZi Multi PRO++ — Mini
└── HaGeZi TIF — Medium
```

> [!WARNING]
> This is the **only reduced Brave profile** in the guide. Do not use it unless the full profile creates a measurable performance or stability issue.

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

## 🔗 Related

* [1. 🧱 Recommended Architecture](01-architecture.md) — why the complementary layer is DNS.
* [3. 🧩 uBlock Origin](03-ublock-origin.md) — the alternative browser blocker, with the same external profile.
* [5. 🌐 AdGuard Home](05-adguard-home.md) — the DNS layer that pairs with Shields.
* [7.3. Brave Shields](07-troubleshooting.md#73-brave-shields) — diagnosing a broken site without weakening Shields globally.

---

⬅️ Previous: [3. 🧩 uBlock Origin](03-ublock-origin.md) · 🏠 [Index](README.md) · ➡️ Next: [5. 🌐 AdGuard Home](05-adguard-home.md)
