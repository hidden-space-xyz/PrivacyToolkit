**[🏠 Guide index](README.md)** · Chapter 8 of 9

# 8. ✅ Verification

Do not optimize your configuration for a synthetic `100%` score.

A test page only checks the domains and techniques its author chose to include.

Passing every test does not necessarily mean your real-world configuration is better.

---

## 🧩 uBlock Origin

* [ ] The Logger shows blocked requests.
* [ ] You can identify the rule responsible for a block.
* [ ] Filter lists update successfully.
* [ ] The enabled lists match [3.7. Final Configuration](03-ublock-origin.md#37--final-configuration) exactly, and nothing else is enabled.
* [ ] **Cookie notices**, **Social widgets**, and **Annoyances** are empty.
* [ ] The Dandelion Sprout list imported here is the **browser** version, not `AntiMalwareAdGuardHome.txt`.
* [ ] Your normal websites still work.

See [3. 🧩 uBlock Origin](03-ublock-origin.md) for the configuration these checks assume.

---

## 🦁 Brave

* [ ] Shields is enabled.
* [ ] Trackers & ads blocking is set to **Aggressive**.
* [ ] Regional lists for the languages you browse are enabled — for Spanish, *Spanish website ad blocker* and *Spanish and Portuguese website ad blocker*.
* [ ] **Tracking URL blocker** is enabled.
* [ ] **Annoying distractions blocker** is enabled.
* [ ] Every other catalog entry is disabled.
* [ ] The only imported URLs are the two HaGeZi lists and Dandelion Sprout Anti-Malware.
* [ ] Custom lists update correctly.
* [ ] The Dandelion Sprout list imported here is the **browser** version, not `AntiMalwareAdGuardHome.txt`.
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
* [ ] Dandelion Sprout Anti-Malware is enabled and uses the **DNS** version (`AntiMalwareAdGuardHome.txt`).

See [5. 🌐 AdGuard Home](05-adguard-home.md). If devices are missing from the Query Log, check [6. 🚧 Preventing AdGuard Home Bypass](06-bypass-prevention.md).

---

## 📱 Outside the Browser

* [ ] A smartphone without a content-blocking extension appears in AdGuard Home.
* [ ] A Smart TV or IoT device appears in AdGuard Home.
* [ ] Native applications generate visible DNS queries.

> [!TIP]
> Confirming that a Smart TV or native application is actually being filtered through AdGuard Home tells you far more about your DNS layer than achieving `100/100` on an ad-block testing website.

---

| ⬅️ Previous | 🏠 Index | Next ➡️ |
|:----------- |:--------:| ---------:|
| **[7. Troubleshooting](07-troubleshooting.md)** | **[All chapters](README.md)** | **[9. Maintenance](09-maintenance.md)** |
