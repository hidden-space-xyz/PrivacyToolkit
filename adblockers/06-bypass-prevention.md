[🏠 Guide index](README.md) · Part 6 of 9

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

## 🔗 Related

* [5. 🌐 AdGuard Home](05-adguard-home.md) — the resolver this chapter protects.
* [5.6. 🔐 Encrypted Upstream DNS](05-adguard-home.md#56--encrypted-upstream-dns) — encryption you *do* want, between AdGuard Home and its upstream.
* [8. ✅ Verification](08-verification.md) — confirming devices really query AdGuard Home instead of bypassing it.

---

⬅️ Previous: [5. 🌐 AdGuard Home](05-adguard-home.md) · 🏠 [Index](README.md) · ➡️ Next: [7. 🔍 Troubleshooting and False Positives](07-troubleshooting.md)
