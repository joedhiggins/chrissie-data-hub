# Data Hub v2.1

## Added

- **Mission** record type — mission start/end time, battery at start and end (0–100% in 20% steps), tactical movement start/end, battery swaps, visibility and audibility to adversary, and whether the system generated tracks in TAK or SCCA. Uses the same session metadata (collector, date, time, event, system, location) as other records.
- **NET/NEF Feedback** record type — operator, system configuration (Fixed Site / Mobile / Dismounted/handheld), C2 framework, setup rating (1–5), NET evaluation prompts, PMCS/manuals, after-operations performance, and additional comments.
- Operator Feedback **Conditions** free-text fields that appear when **Conditional** is selected on “carry this system on an actual mission?” and “use without vendor support?”

## Changed

- System Properties **Network connectivity** options are now TAK, SCCA, TAK and SCCA, and No connectivity (was Wired Only / Wireless Only / Both / None).
- System Properties **Battery chemistry** list shortened from 8 options to 5:
  - Before: Lithium-Ion (Li-Ion); Lithium Polymer (Li-Po); Lithium Iron Phosphate (LiFePO4); Nickel-Metal Hydride (NiMH); Nickel-Cadmium (NiCd); Alkaline; Lead-Acid; Other / Custom
  - After: Lithium-Ion (Li-Ion / Li-Po); Lithium Iron Phosphate (LiFePO4); Nickel-Metal Hydride (NiMH); Alkaline; Other
  - Li-Po is folded into Lithium-Ion. NiCd and Lead-Acid (uncommon on current cUAS kits) map to Other when old records are opened.
- Engagement **Attack geometry** adds Treetop-level and High-altitude.
- Engagement **DDIL environment** is renamed **DDIL effects on cUAS system**, with No effects, Intermittent connection, Lost connection, and Spoofed. Prior “No (optimal)” values migrate to No effects.
- Engagement **Track continuity** adds False positive.
- Engagement **Observed effect** adds No effects.

# Data Hub v2.0

## Added

- **Session tab** — collector chips and date (device clock). Stamped on every record so concatenated JSON stays traceable by collector.
- **Event ID** — prefills from the last saved value; editable per record.
- **New record picker** — one **New** button, then choose System / Engagement / GCS / Failures / Operator Feedback / Quick Note. Bottom nav is Session · New · Data (labels, not icon-only).
- **Unique IDs** — `Collector_YYYYMMDD_HHMMSS_xxxxxx` plus full metadata (`createdAt`, `updatedAt`, schema version).
- **Edit / delete** — tap a data card to open the same form; delete asks for confirmation with type, collector, time, and system.
- **Quick notes** — timestamped text; system optional.
- **General notes** on every type — ~200-character window, 1500-character max.
- **Optional GPS** — “Use my location” (never automatic). Converts WGS84 to MGRS and can fill GCS denial location. Shows accuracy. Clear to remove.
- **Draft autosave** — unsaved fields restore if you leave a new record.
- **JSON import merge** — match on record ID; keep the newer `updatedAt`. Export filename `{collector}-{date}.json`.
- **PWA bits** — manifest, icon, service worker (works when served over http(s), not `file://`).

## Changed

- Short exclusive lists and ratings are **chips** (segmented controls). Multi-selects (frequencies, intended effect) are toggle chips. Long lists (chemistry, mil-spec) stay dropdowns. Counts are numeric fields.
- Collection time and failure/resolution time default to **now** and stay editable (`Now` button).
- System stays **per record** (last system remembered per type). Collector/date live on Session and copy onto each new form.
- After a new save, stay on the form (toast) for the next entry. After an edit, return to Data.
- Data view is **cards** with type filters, not a wide table.
- Failures header no longer mentions unused calculated metrics.

## Fixed

- Broken operator-feedback markup from a leftover edit note.
- Failure/resolution field reset (form vs section id).
- Form type panels not switching (`setActiveFieldSection` was missing).

## Changed (v2.0.1)

- Record header slimmed: **time + event + + Loc** on one row, **system** on the next. Collector/date come from Session only (still stored on every JSON row).
- **+ Loc** toggles on/off (blue when tagged); MGRS shows in grey under the row.
- Mobile **pair-sm** grids keep short fields side-by-side (temp/RH, posture/DDIL, detect time/range, etc.).


- Serve the folder (`python3 -m http.server`) or host it so Add to Home Screen / offline cache actually install.
- PNG app icons if iOS ignores the SVG.
- Optional link from a resolution row to a prior failure (same system / last failure).
- Calculated metrics (e.g. defeat rate) if they still want them.
- Photo or screenshot attach on notes (device storage gets messy fast).
- Git remote — this folder is not a git repo yet; nothing has been committed.
- Event ID “next” helper if auto-increment is more useful than “same as last.”
