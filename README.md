# The Seven Terraces — OSI Model Interactive Pyramid

Part of the **Goblin Eaters Cyber Cavern** toolset, accompanying the post
*"The Seven Terraces of Purgatory: Why the OSI Model Is a Passage, Not a
Destination"* (May 21, 2026) in the **How Protocols Work, and How They
Break** series. Added as a retrospective companion tool.

---

## What it does

Where the Week 2 (ARP) and Week 3 (Layer 3) tools each walk through one
specific attack scenario step by step, this tool is a structural map of the
whole stack. It models the OSI layers as a mountain of seven terraces,
echoing Dante's *Purgatorio* — a pilgrim who picks up burdens climbing up
and sheds them at the summit, mirrored here as a packet that picks up
headers descending the stack on the sending side and strips them off
ascending the stack on the receiving side.

Each terrace is split into three parts:

- **Descending (left)** — what the sender wraps the packet in at this
  layer, and what it adds without being able to verify
- **The sin (center)** — the one trust assumption baked into this layer
  that becomes the exploitable seam
- **Ascending (right)** — what the receiver actually checks (or doesn't)
  when it strips that same header back off

The mountain is widest at Terrace I (Physical) at the base, and narrows
toward the summit at the Terraces V·VI·VII landing — matching both
encapsulation order (data is built up from the bottom layer outward) and
the climb-to-the-summit shape of the metaphor.

## Why Terraces 5, 6, and 7 share a landing

The post argues the OSI model is a passage, not a rigid checklist — and
real-world stacks bear that out. Session, Presentation, and Application
rarely separate cleanly in practice (TLS, session cookies, and the HTTP
request itself all happen in the same effective step). Rather than force
three artificial climbs, the tool fuses them into one wide landing at the
top of the mountain, with a note explaining the collapse rather than
hiding it.

## The seven terraces

| Terrace | OSI Layer | Sin |
|---|---|---|
| I | Physical | Trusts that the medium has only one listener — a tap, splice, or anything else physically attached sees the same signal a legitimate receiver does |
| II | Data Link | Trusts the source MAC as self-reported truth — nothing on the wire verifies a frame actually came from the MAC it claims (the ARP poisoning seam) |
| III | Network | Trusts the source IP as a self-declared return address — an envelope, not a passport (the IP spoofing / BGP hijacking seam) |
| IV | Transport | Trusts whoever can see the sequence numbers — TCP sequence numbers keep streams in order, not identity; UDP has no handshake at all |
| V · VI · VII | Session, Presentation, Application | Trusts that someone above will finally check — the assumption every lower layer deferred comes due here, with no standard answer |

Each lower terrace's unverified trust is inherited by the one above it.
The Application landing is where the chain of deferred verification finally
runs out of layers to pass to.

## Interaction

- Mountain renders fully collapsed on load — each terrace shows its name,
  OSI mapping, and a one-line sin preview
- Click a terrace to expand it; only one terrace is open at a time, and
  opening a new one collapses the previous
- Expanded terraces grow to fit their content (descending text, ascending
  text, sin card, and both packet stacks) rather than a fixed height
- Packet stacks are illustrative, not byte-accurate — they show which
  headers are present and in what order, not literal hex/field values
  (for that level of detail, see the Layer 2 ARP visualizer and the
  Layer 3 packet visualizer)

## Deployment

Single self-contained HTML file — no build step, no external dependencies
beyond Google Fonts (JetBrains Mono, Syne) loaded via `<link>`.

```bash
cp osi-purgatorio-pyramid.html ~/ubritsa/static/tools/
```

Reference from the post body the same way the other tools are embedded —
an `<iframe>` or direct link to
`https://ubritsa.com/tools/osi-purgatorio-pyramid.html`.

## Technical stack

- Vanilla HTML/CSS/JS — no frameworks, no build step
- Fonts: JetBrains Mono (body/mono), Syne (headings) — same pairing as the
  ARP and Layer 3 tools, for toolset visual consistency
- All typography in `rem`/`em`, base `font-size` set on `html` — no fixed
  pixel font sizes
- Dark theme palette matches the rest of the Goblin Eaters Cyber Cavern
  toolset (`--bg`, `--surface`, `--blue`/`--green`/`--red`/`--amber` accent
  system)

## Part of the Goblin Eaters Cyber Cavern Toolset

- [ARP Protocol Visualizer](https://ubritsa.com/tools/arp-visualizer.html) — Week 2, Layer 2
- [Layer 3 Packet Visualizer](https://ubritsa.com/tools/layer3-visualizer.html) — Week 3, Layer 3
- [OSI Attack Explainer](https://ubritsa.com/tools/osi-attack-explainer.html) — The Attack Layer Cake
- [IPv4 vs IPv6 Security Posture Visualizer](https://ubritsa.com/tools/ipv4_v_ipv6_heel_analysis.html) — Week 4
- **The Seven Terraces (this tool)** — Purgatorio companion, retrospective addition
