# Project X pivots away from China — impact on Lantern‑box (and MahsaFreeConfig)

_Analysis prepared 2026‑07‑10 in response to a link shared by Mark._

## 1. What the shared link actually says

The link is a post by **李老师不是你老师 (@whyyoutouzhele)**:
<https://x.com/i/status/2074312447167541312>

Translated, the post reports:

> **Anti‑censorship project Project X announces it is cutting off mainland China: no
> longer updating for the GFW, pivoting to Russia and Iran.**
> Recently the open‑source anti‑censorship project Project X posted a series of
> messages in its Telegram channel… The announcement says that because the "Chinese
> circumvention scene" has too many problems and is too high‑risk, Project X will
> *"pivot entirely to Russia and Iran"* and *"strictly prohibit use inside mainland
> China."*

A parallel summary circulating in the community (@geekbb) puts it more bluntly:

> "R佬 [RPRX, the lead maintainer] announced Xray‑core only targets the Russian and
> Iranian firewalls, forbidden for use inside mainland China. The features are
> developed only for them; if it happens to work in China that's purely accidental.
> Project X has completely severed ties with the Chinese ecosystem."

**Project X** is the umbrella for **Xray‑core** and the protocols it authored —
**VLESS, VMess, XTLS "Vision" (`xtls-rprx-vision`), and REALITY**. It is one of the
two engines (the other being **sing‑box / SagerNet**) that essentially the entire
consumer circumvention ecosystem is built on.

> Sourcing note: I could not independently open the Telegram announcements (the X
> pages 403 without login). The wording above is what @whyyoutouzhele and @geekbb
> reported. Treat the *policy shift* as well‑attested and the *exact quotes* as
> second‑hand.

## 2. Why Mark called these "long‑time known issues"

The announcement itself is new; the weaknesses it exposes are not. Three have been
discussed in the circumvention community for years:

1. **Governance / maintainer concentration.** The global circumvention stack rests on
   a very small number of volunteer‑maintained core engines — Xray‑core (Project X)
   and sing‑box (SagerNet). Their roadmap, threat‑model priorities, and even continued
   existence depend on a handful of individuals. A single maintainer decision can
   redirect or withdraw hardening for an entire censor overnight. That is exactly what
   just happened.

2. **Protocol lineage and detectability arms race.** VLESS, VMess, Shadowsocks, REALITY
   and XTLS‑Vision are in a permanent cat‑and‑mouse with DPI. Each has had detection
   episodes (active probing of Shadowsocks, TLS/ClientHello fingerprinting, REALITY
   whitelist edge cases). Staying ahead of a *specific* censor requires the upstream to
   *actively* keep tuning against that censor. When the upstream drops a censor,
   downstream tools that inherited that hardening quietly stop getting it.

3. **Per‑censor tuning doesn't transfer for free.** Evasion tuned against the GFW is not
   automatically effective against Iran's or Russia's filtering, and vice‑versa. Project X
   explicitly reorienting to Russia/Iran means its future work optimizes for *those*
   networks; anything that still needs GFW resistance can no longer assume upstream help.

The takeaway the community has repeated for years — **don't depend on a single engine or
a single protocol family** — is what this event validates.

## 3. How it affects Lantern‑box

**Reference:** <https://github.com/getlantern/lantern-box> — "extra protocols built for
places where the internet comes with walls," built **on top of sing‑box**. Its
distinctive transports are **Samizdat, Reflex, WATER, Outline SDK (smart dialer),
AmneziaWG, and ALGeneva**; from sing‑box it inherits Shadowsocks, VMess, Trojan,
Hysteria and WireGuard.

### Direct impact: essentially none
Lantern‑box does **not** embed Xray‑core / Project X. It is a sing‑box‑based platform, so
"Project X stops updating for China" does not break its build, its own protocols, or its
release path. Nothing in Lantern‑box needs an emergency change to keep compiling or running.

### Indirect impact: real but bounded
- **Protocol *definitions* still come from Project X.** sing‑box re‑implements VLESS,
  REALITY and `xtls-rprx-vision` — protocols specified and reference‑maintained by
  Project X. Any Lantern‑box deployment (or user config) that leans on **VLESS / REALITY /
  XTLS‑Vision** now depends on protocols whose *hardening is being tuned for Russia/Iran
  only*. For China specifically, treat those paths as "no longer actively hardened against
  the GFW upstream."
- **The same governance risk applies to sing‑box.** The thing that makes this announcement
  worrying is not Xray specifically — it's the *pattern*. sing‑box is a single
  volunteer‑led project subject to the same kind of priority shift. Lantern‑box's whole
  base inherits that concentration risk.

### The reassuring part: this validates Lantern‑box's design
Lantern‑box's *differentiators* — Samizdat, Reflex, WATER, Outline SDK, AmneziaWG,
ALGeneva — are **independently developed and not dependent on Project X**. They come from
Lantern, Jigsaw (Outline), Amnezia, and academic work (WATER, Geneva). This is precisely
the protocol/maintainer diversification that mitigates the "known issue." The event is an
argument *for* Lantern‑box's multi‑transport strategy, not against it.

### Recommended posture for Lantern‑box
1. **Inventory the exposure:** flag any inbound/outbound or fallback path that relies on
   VLESS / REALITY / XTLS‑Vision and label it "GFW‑hardening unmaintained upstream."
2. **Prioritize the independent transports for China‑facing users** (Samizdat, Reflex,
   WATER, ALGeneva, AmneziaWG); keep the sing‑box‑inherited/Xray‑lineage protocols as
   secondary rather than primary GFW paths.
3. **Track the upstreams as a supply‑chain risk:** pin and vendor sing‑box; watch for any
   analogous scope‑narrowing from SagerNet; keep the ability to fork/patch protocol
   hardening yourselves rather than waiting on upstream.
4. **Don't over‑react:** no protocol is "broken" today. The change is a *maintenance‑intent*
   signal, not a live break. Detectability of REALITY/VLESS against the GFW may degrade over
   time, not immediately.

## 4. How it affects this repo (MahsaFreeConfig)

MahsaFreeConfig distributes subscription configs (`vmess://`, `vless://`, `ss://`,
WireGuard/WARP), and at least some entries use **XTLS Vision (`flow=xtls-rprx-vision`)** —
i.e. Project X protocols. Two observations:

- **Audience alignment is favorable.** This project serves **Iranian** users, and Project X
  is now *explicitly prioritizing Iran*. So the pivot is neutral‑to‑positive for the
  protocols these configs rely on — continued/greater upstream attention to the Iranian
  filtering environment, not less.
- **Same governance caveat.** The configs still depend on VMess/VLESS/Vision and on
  third‑party servers, so the single‑ecosystem concentration risk applies here too. The
  mitigations are the usual ones: keep protocol diversity in the pool, and don't let the
  whole subscription rest on one protocol family.

## Sources
- Post shared by Mark: <https://x.com/i/status/2074312447167541312> (@whyyoutouzhele)
- Community summary: <https://x.com/geekbb/status/2073660221948584151>
- Lantern‑box: <https://github.com/getlantern/lantern-box>
- sing‑box VLESS/REALITY/Vision support: <https://sing-box.sagernet.org/configuration/outbound/vless/>
- Project X / Xray‑core: <https://github.com/XTLS/Xray-core>
