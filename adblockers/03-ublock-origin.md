**[🏠 Guide index](README.md)** · Chapter 3 of 9

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

## 3.6. 🧱 External Lists — Default Full Profile

Use the **full** HaGeZi lists in the browser by default:

```text
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.txt
```

| List                          | Purpose                                                |
| ----------------------------- | ------------------------------------------------------ |
| **HaGeZi Multi PRO++ — Full** | Ads, tracking, telemetry, affiliate infrastructure, and other unwanted domains |
| **HaGeZi TIF — Full**         | Malware, phishing, scams, and malicious infrastructure |

> [!IMPORTANT]
> **PRO++ Full + TIF Full is the normal browser configuration in this guide.**
>
> Do not choose smaller variants merely to save resources on paper. Keep the full lists unless they cause an observable performance or stability problem on that device.

### 🪶 Performance fallback

Only if the full profile causes real performance problems, replace **both** full HaGeZi lists with this single reduced profile:

```text
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.plus.mini.txt
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/tif.medium.txt
```

| List                           | Role in the fallback profile |
| ------------------------------ | ---------------------------- |
| **HaGeZi Multi PRO++ — Mini**  | Reduced-size PRO++ variant   |
| **HaGeZi TIF — Medium**        | Reduced-size TIF variant     |

> [!WARNING]
> Do not treat this as an alternative preference profile. It is only a resource fallback for systems that cannot run PRO++ Full + TIF Full comfortably.

<details>
<summary><strong>🦠 Dandelion Sprout Anti-Malware — optional additional source</strong></summary>

If you also want Dandelion Sprout Anti-Malware, import it from its source repository:

```text
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Dandelion%20Sprout%27s%20Anti-Malware%20List.txt
```

This is an additional malware- and scam-oriented source. The normal HaGeZi profile remains PRO++ Full + TIF Full; the reduced HaGeZi profile is only for performance problems.

</details>

> [!IMPORTANT]
> All manually imported external list URLs in this guide point to **`raw.githubusercontent.com`**.

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

| ⬅️ Previous | 🏠 Index | Next ➡️ |
|:----------- |:--------:| ---------:|
| **[2. Quick Configuration](02-quick-configuration.md)** | **[All chapters](README.md)** | **[4. Brave Shields](04-brave-shields.md)** |
