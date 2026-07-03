# Figma Variables Video Script — Button Component

Source structure: `TPG DS Documentation/30 Jun.json`
Collections: `primitives` → `brand` → `semantics` → `mapped-tpg` (modes: light/dark)

Cut markers: **S** = Short (3-5min) · **D** = Standard (8-12min) · **X** = Deep-dive (15-20min)
A row tagged `S D X` plays in all three; `D X` only in Standard+Deep; `X` only in Deep-dive.

---

## Intro

| Cut | VO | Screen Action | Figma Panel |
|---|---|---|---|
| S D X | "We're building a Button component the right way — through the token chain: Primitive, Brand, Semantic, Mapped. By the end you'll know exactly where a new value belongs." | Title card, then cut to empty Figma file | — |
| D X | "Two things trip people up: which tier owns a value, and when a component needs its own custom token vs reusing a global one. We'll cover both before touching the button." | — | — |

---

## Section A — The chain (colour only)

> Note for narration: **this chain applies to colour only.** Padding, gap, and radius don't travel through Primitive → Brand → Semantic — those are created directly inside the component's Mapped group. Covered in Section C.

| Cut | VO | Screen Action | Figma Panel |
|---|---|---|---|
| S D X | "Start at Primitive. Raw values, no meaning attached — just a purple." | Open `primitives` collection, scroll to `colour/tpg-purple/500` | Variables panel → primitives |
| S D X | "Brand takes that raw purple and gives it a role in the TPG brand — primary-1, shade 500." | Open `brand` collection, show `tpg/color/primary-1/500` aliasing to `colour/tpg-purple/500` | Variables panel → brand |
| S D X | "Semantic gives it intent — this isn't 'purple' anymore, it's 'action, primary, default' — in light mode." | Open `semantics`, show `tpg/light/color/action/primary/default` aliasing to brand value | Variables panel → semantics |
| D X | "Same chain works for a neutral — white primitive, global/neutral/white in brand, resolves to border/inverse in semantic." | Trace `colour/monochrome/white` → `global/neutral/white` → `tpg/light/color/border/inverse` | Variables panel, alias trace view |
| S D X | "Last stop: Mapped. This is what components actually bind to — and inside Mapped, colour lives in four groups: surface, text, icon, border. These four are the *global* set, shared across every component." | Open `mapped-tpg`, expand `surface`, `text`, `icon`, `border` groups at root level | Variables panel → mapped-tpg |
| X | "Naming convention through the chain: primitive is literal (colour/tpg-purple/500), brand adds role (color/primary-1/500), semantic adds intent + mode (light/color/action/primary/default), mapped adds usage (surface/brand/primary/default). Read the name, know the tier." | Side-by-side of all 4 names | — |

---

## Section B — Global vs Component-specific (Mapped colour groups)

> On-screen title card: **"Two groups inside Mapped — know which one you're editing."**

### Group 1 — Global (mapped/surface, text, icon, border)

| Cut | VO | Screen Action | Figma Panel |
|---|---|---|---|
| S D X | "Group one: Global. These sit at the root of Mapped — surface, text, icon, border. If a component's colour spec matches one of these exactly, don't make a new token — alias straight to it." | Highlight `surface/*`, `text/*`, `icon/*`, `border/*` as one bordered group | Variables panel, group 1 highlighted |
| D X | "Example: when a button border matches the shared border style, you alias the global `border/primary/default` token instead of making a new one. No duplication." | Show a border reusing the root `border/primary/default` global token | Variables panel, alias arrow |

### Group 2 — Component-specific (mapped/component/*)

| Cut | VO | Screen Action | Figma Panel |
|---|---|---|---|
| S D X | "Group two: Component-specific. When a component's colour doesn't match anything in the global set, you create it inside the component's own group. Button gets its own `surface/brand`, `surface/secondary`, `surface/white` states — hover, pressed, disabled — none of which exist globally." | Expand `component/button/surface/*` — brand, default, secondary, success, white | Variables panel → mapped-tpg → component/button |
| D X | "Decision rule, one line: spec matches global → alias global. Spec is custom to this component → create it inside `component/<name>/...`." | On-screen text overlay of the rule | — |
| X | "Common mistake: creating a component-specific token for something that already exists globally — you get five different tokens all resolving to the same white. Check the global group first, every time." | Show a duplicate-token example, then the fix | Variables panel |

---

## Section C — Building the Button

| Cut | VO | Screen Action | Figma Panel |
|---|---|---|---|
| S D X | "Now the button itself. Draw the frame, auto-layout, label — standard component setup." | Create frame → apply auto-layout → add text layer "Button" | Canvas |
| S D X | "Padding, gap, radius — these don't come from Primitive or Semantic. They're defined directly inside Mapped, under the component's own `values` group." | Open `mapped-tpg` → `component/button/values` → show `padding/md`, `gap/xs`, `radius/sm` | Variables panel → component/button/values |
| S D X | "Bind them: padding to the auto-layout padding, gap to item spacing, radius to corner radius." | Select button frame → bind each variable via the properties panel | Right sidebar, variable binding |
| D X | "Colour next. Default state — is 'brand primary' already covered by the global surface group? No — button's brand states (default, hover, pressed, disabled) are unique to button, so they live in `component/button/surface/brand/*`." | Bind fill → `component/button/surface/brand/brand` | Right sidebar → Fill → variable |
| D X | "Label colour, icon colour — same check each time: global first, component-specific only if it doesn't match." | Bind text colour → `component/button/label/primary`; icon → `component/button/icon/default` | Right sidebar |
| X | "Build out the full variant set — brand, secondary, white/ghost, success — each with default, hover, pressed, disabled bound to their matching mapped token." | Create variant properties: `type`, `state`; bind each combination | Variants panel |
| X | "Dark mode check — mapped-tpg has light and dark modes. Switch the mode selector and confirm every bound token resolves correctly without manual overrides." | Toggle mode switcher light → dark on the button frame | Top toolbar, mode switcher |
| S D X | "That's the full path: primitive raw value, brand identity, semantic intent, mapped usage — global where it matches, component-specific where it doesn't. Same process for your next component." | Zoom out to show finished button + variable panel side by side | Canvas + Variables panel |

---

## Cut-length guide

- **Short (3-5 min):** Intro (S line) → Section A (S D X rows only) → Section B (S D X rows only) → Section C (S D X rows only). Skip all trace/rule/mistake asides.
- **Standard (8-12 min):** All `S D X` + `D X` rows. Skip `X`-only naming convention, duplicate-token mistake, full variant build, dark mode.
- **Deep-dive (15-20 min):** Every row, including naming convention rule, common mistake, full variant matrix, dark mode verification.
