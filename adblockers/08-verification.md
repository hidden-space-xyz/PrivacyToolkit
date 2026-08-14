[🏠 Guide index](README.md) · Part 8 of 9

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

See [3. 🧩 uBlock Origin](03-ublock-origin.md) for the configuration these checks assume.

---

## 🦁 Brave

* [ ] Shields is enabled.
* [ ] Trackers & ads blocking is set to **Aggressive**.
* [ ] Appropriate regional lists are enabled.
* [ ] Custom lists update correctly.
* [ ] Your normal websites still work.

See [4. 🦁 Brave Shields](04-brave-shields.md).

---

## 🌐 AdGuard Home

* [ ] Your devices appear in the Query Log.
* [ ] DNS requests are actually reaching AdGuard Home.
* [ ] Blocked domains show the expected matching rule.
* [ ] Filter lists update successfully.
* [ ] The server is not under excessive memory pressure.
* [ ] PRO++ Full + TIF Full is still enabled unless you have confirmed a real performance problem.

See [5. 🌐 AdGuard Home](05-adguard-home.md). If devices are missing from the Query Log, check [6. 🚧 Preventing AdGuard Home Bypass](06-bypass-prevention.md).

---

## 📱 Outside the Browser

* [ ] A smartphone without a content-blocking extension appears in AdGuard Home.
* [ ] A Smart TV or IoT device appears in AdGuard Home.
* [ ] Native applications generate visible DNS queries.

> [!TIP]
> Confirming that a Smart TV or native application is actually being filtered through AdGuard Home tells you far more about your DNS layer than achieving `100/100` on an ad-block testing website.

---

## 🔗 Related

* [7. 🔍 Troubleshooting and False Positives](07-troubleshooting.md) — what to do when a check fails.
* [9. 🔧 Maintenance](09-maintenance.md) — how often to repeat these checks.

---

⬅️ Previous: [7. 🔍 Troubleshooting and False Positives](07-troubleshooting.md) · 🏠 [Index](README.md) · ➡️ Next: [9. 🔧 Maintenance](09-maintenance.md)
