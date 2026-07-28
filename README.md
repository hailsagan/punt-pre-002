# Punt · PRE-002 — Discovery that arms the call (POC)

An interactive proof-of-concept for **discovery that reads a player's known interest and
surfaces the matching market fast** — arming their first bet instead of dropping them into a
generic, undifferentiated feed. Built directly on top of the real `adaptive-discovery` page
from `punt-explorations` (the actual Predict landing page, header, category rails, and all),
with only the **hero slot** swapped per concept.

## View it

Open [`index.html`](index.html) (or [`pre-002-discovery.html`](pre-002-discovery.html)) in any
modern browser. `assets/discovery.css` is the real punt-explorations stylesheet — keep it
alongside the HTML file.

## The brief

- **Proves Bet 3** — a single *player profile*, not just a wallet. Reading what a player
  already engages with to power discovery makes personalization a platform-owned capability.
- **Moves TAM** — bounce rate at the choice-overload stage is the primary signal. Getting the
  right market in front of a motivated player faster means more players reach a first bet.
- **The moment** — a new player lands in Predict facing dozens of live markets. The block is
  choice overload, not trust. They already know what they care about; the platform should too.
- **Scope** — Predict room only. Personalization should read as **inferred** ("this already
  knows me"), not as an up-front preferences form.

## The scenario

One new player with a known interest — the **Lakers / LeBron** — inferred from behaviour
(follows, watch history, repeat prop checks). The rest of the real Predict landing page
(header, "Customize your view" panel, trending movers, Sports/Politics/Economics rails) is
untouched; only the hero card responds to the known interest.

## How this build works

This isn't a hand-styled wireframe — it's the actual saved DOM + CSS from
`https://punt-explorations.vercel.app/adaptive-discovery/`, with:

- The **hero card only** (the big "Trending now" feature tile) replaced with a small
  `#heroSlot` that our own script renders per concept — everything else on the page
  (header, category tabs, "Customize your view", the movers row, and the Sports/Politics/
  Economics sections) is the real markup, styled by the real linked stylesheet.
- The **review bar** is the real one from that build (`PRE-002 · review`), with its
  `Variant: Adaptive / Generic` segment relabeled to `Model: V1 / V2` to drive which concept
  renders in the hero. `Player`, `Fidelity`, `Device`, `Reset learning`, and `Flags` are the
  same controls from the reference build (Fidelity and Device are fully wired the same way the
  real app does it — attribute swaps the CSS already handles; Player and Flags are decorative
  here).
- A few small `.pre-*` classes (in `index.html`'s `<style>`) cover the bits that don't exist in
  the real design system yet — the inferred-signal chips, the pick arrows/dots for V2 — built
  from the same design tokens (`--punt-*`) so they sit inside the hero without looking bolted on.

## The two concepts

| # | Concept | Pattern |
|---|---------|---------|
| V1 | The Read | Single inferred lead — the hero opens on the one matching market, with the signals that produced it shown as chips |
| V2 | The Narrowing | Guided one-at-a-time triage — arrows page through the top 3 ranked picks in the same hero slot; never a wall |

Both are purely inferred — no preference form. The brief's open flag (inferred-only vs. some
direct input) isn't resolved by either; that's a further variant if the team wants to test it.

## Status

Internal POC. Cover images (`/adaptive-discovery/covers/...`) point at the live reference site
and won't resolve offline — cards fall back to a solid dark tile, which is the same fallback
the real component uses. Everything below the hero is static demo content from the reference
build (not wired to Model/Player), matching what that page actually ships today.
