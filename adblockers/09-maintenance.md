[🏠 Guide index](README.md) · Part 9 of 9

# 9. 🔧 Maintenance

Once configured correctly, this setup should require **very little day-to-day maintenance**.

Review it when:

* 🔴 several websites suddenly begin to break;
* 🔴 a filter list stops updating;
* 🟡 memory usage increases significantly;
* 🟡 you accumulate many manual exceptions;
* 🟡 PRO++ or TIF updates materially increase memory usage or reload times;
* 🟢 you decide to enable additional annoyance categories.

> [!IMPORTANT]
> **Performance downgrade rule:** keep **PRO++ Full + TIF Full** unless you can identify a real resource or stability problem. If that happens, switch directly to the guide's only fallback profile: **PRO++ Mini + TIF Medium**.
>
> Do not create extra intermediate profiles such as Full + Medium or Mini + Full. This keeps the configuration predictable and troubleshooting simple.

> [!TIP]
> If one particular list repeatedly requires new exceptions, investigate the specific false positives first. Aggressiveness and performance are separate issues: the reduced profile is intended for resource constraints, not as the first response to ordinary site breakage.

---

## 🔗 Related

* [2. ⚡ Quick Configuration](02-quick-configuration.md) — the default profile and the fallback, with the rule for choosing between them.
* Fallback list URLs per layer: [uBO](03-ublock-origin.md#-performance-fallback), [Brave](04-brave-shields.md#-performance-fallback), [AdGuard Home](05-adguard-home.md#-performance-fallback).
* [7. 🔍 Troubleshooting and False Positives](07-troubleshooting.md) — the correct first response to breakage.
* [8. ✅ Verification](08-verification.md) — checks worth repeating after any change.

---

⬅️ Previous: [8. ✅ Verification](08-verification.md) · 🏠 [Index](README.md)
