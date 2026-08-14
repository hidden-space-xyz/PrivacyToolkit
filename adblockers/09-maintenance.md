**[🏠 Guide index](README.md)** · Chapter 9 of 9

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

> [!NOTE]
> **The downgrade applies to the HaGeZi lists only.** Dandelion Sprout Anti-Malware remains enabled in both profiles and in all three tools, at the variant URL matching each layer. If you ever do remove it, remove it deliberately as a separate decision — not as a side effect of a performance downgrade.

> [!TIP]
> If one particular list repeatedly requires new exceptions, investigate the specific false positives first. Aggressiveness and performance are separate issues: the reduced profile is intended for resource constraints, not as the first response to ordinary site breakage.

---

| ⬅️ Previous | 🏠 Index | Next ➡️ |
|:----------- |:--------:| ---------:|
| **[8. Verification](08-verification.md)** | **[All chapters](README.md)** | *End of the guide* |
