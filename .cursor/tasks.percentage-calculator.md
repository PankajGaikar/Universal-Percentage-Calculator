# Universal Percentage Calculator — Tasks for Cursor

> Save this file as **`.cursor/tasks.percentage-calculator.md`** (or `tasks.md`).  
> Open it in Cursor and run each task in order.  
> **Important:** These tasks ask Cursor to generate files; you don’t have to hand-write code.

---

## 0) Workspace & Repo Bootstrap

**Goal:** Initialize the repo and standard folders.

**Prompt for Cursor**  
Create:
- A new git repo.
- Folders: `docs/`, `App/`, `Modules/`, `xcodegen/`, `.cursor/`.
- A minimal `README.md` titled **Universal Percentage Calculator** with a 1-paragraph description and a section **Build & Test with Cursor (MCP)** as a placeholder (will fill later).

**Deliverables**
- Initialized git repo
- Required directories
- `README.md` with title + short description

**Acceptance Criteria**
- Running `ls` shows `docs App Modules xcodegen .cursor`
- `README.md` has app name and short description

---

## 1) MCP (Cursor) Configuration

**Goal:** Enable build/test operations from Cursor.

**Prompt for Cursor**  
Create `.cursor/mcp.json` that:
- Registers `XcodeBuildMCP` via `npx xcodebuildmcp@latest`.
- Enables workflows: `swift-package`, `project-discovery`, `project-scaffolding`, `build`, `tests`.
- Disables Sentry.
Also append to `README.md` a short **Build & Test with Cursor (MCP)** section describing how to run discovery, build, and tests using the MCP UI in Cursor.

**Deliverables**
- `.cursor/mcp.json`
- README updated with MCP usage notes

**Acceptance Criteria**
- JSON is valid and references the workflows above
- README explains discovery → build → tests sequence

---

## 2) Architecture Overview

**Goal:** Lock a clean structure for generation.

**Prompt for Cursor**  
Create `docs/ARCHITECTURE.md` covering:
- **Layers:**  
  - `Modules/PercentageCore` (Swift Package; pure math/logic; unit-tested; no UI)  
  - `App/` (SwiftUI app; Liquid Glass design system; features call into core)
- **Data Flow:** View → ViewModel/State → Core API → Result → Formatting → Render
- **Error Handling:** typed errors; user-friendly messages
- **Rounding:** banker’s rounding for currency display; specify where rounding occurs (input normalization → calculation precision → formatted output)
- **Performance:** recalculation < 100ms on device; smooth slider interactions

**Deliverables**
- `docs/ARCHITECTURE.md`

**Acceptance Criteria**
- Clear module map, data flow, error + rounding + performance sections present

---

## 3) Calculator Catalog & Requirements

**Goal:** Freeze v1 scope and rules.

**Prompt for Cursor**  
Create `docs/CALCULATORS_SPEC.md` with v1 calculators:
1) **Tip** (split, optional rounding rules)  
2) **Discount**  
3) **Tax** (add + reverse)  
4) **Profit Margin/Markup** (solve any two of: cost, price, margin%)  
5) **ROI** (absolute %, optional annualized if period provided)  
6) **Compound Interest** (FV with `n` per year; no contributions in v1)  
7) **Stock Profit/Loss** (fees optional)  
8) **Mutual Fund CAGR**  
9) **Percentage Change/Difference** (from → to)

For each, define:
- Inputs
- Outputs
- Validation & bounds (e.g., % ranges)
- Edge cases
- Display formatting notes

**Deliverables**
- `docs/CALCULATORS_SPEC.md`

**Acceptance Criteria**
- Each calculator has inputs/outputs/edge cases/formatting
- Reverse tax and solve-any-two behavior described

---

## 4) Liquid Glass UI Guide (Design System)

**Goal:** Establish visual & interaction rules (no code).

**Prompt for Cursor**  
Create `docs/UI_DESIGN_LIQUID_GLASS.md` documenting:
- **Aesthetic:** glass cards (translucent/blur), elevation, generous radius, subtle shadows
- **Controls:** sliders with live results, steppers, segmented “solve for” toggles
- **Layouts:** standardized sectioning (Header → Inputs → Result → Optional Chart)
- **iPad:** two-pane (inputs | visualization) responsive layout
- **Haptics:** key increments (e.g., 5%, 10%, 25%)
- **Accessibility:** contrast on materials, Dynamic Type, VoiceOver labels
- **Charts:** where to show bar/pie visuals and when to keep form-only

**Deliverables**
- `docs/UI_DESIGN_LIQUID_GLASS.md`

**Acceptance Criteria**
- Clear, testable UI guidance for later implementation

---

## 5) Globalization (i18n, l10n, Currency)

**Goal:** Specify localization/currency behavior.

**Prompt for Cursor**  
Create `docs/I18N_L10N.md` defining:
- **Phase-1 languages:** `en`, `hi`, `es`, `fr`, `de`, `it`, `pt-BR`, `ja`
- **Keys to localize:** titles, input labels, results, errors, buttons
- **Locale formatting:** numbers, decimal/group separators, percent, currency
- **Currency policy:** default to device locale; allow per-session override
- **RTL readiness checklist** (mirroring, alignment, icons, navigation)

**Deliverables**
- `docs/I18N_L10N.md`

**Acceptance Criteria**
- Keys/formatting/RTL/override policy clearly described

---

## 6) QA Strategy & Test Plan

**Goal:** Define what will be tested (before code exists).

**Prompt for Cursor**  
Create `docs/QA_TESTPLAN.md` with:
- **Unit tests** per calculator: happy paths + edge cases
- **Rounding assertions** (currency/percent display)
- **UI tests**: input → action → verify output; slider ↔ numeric sync; locale flip affects formatting
- **Performance checks:** recomputation < 100ms
- **Accessibility checks:** VoiceOver labels; Dynamic Type

**Deliverables**
- `docs/QA_TESTPLAN.md`

**Acceptance Criteria**
- Enumerated, unambiguous cases and expected outcomes

---

## 7) Core Package Contracts (No Code)

**Goal:** Specify public APIs and file layout.

**Prompt for Cursor**  
Create:
- `docs/CORE_API_CONTRACT.md` defining public APIs (names, inputs, outputs, errors) for:  
  `Percentage`, `Discount`, `Tax`, `Tip`, `ProfitMargin`, `ROI`, `CompoundInterest`, `StockProfit`, `MutualFundCAGR`
- `docs/CORE_FILE_LAYOUT.md` listing exact files/paths under `Modules/PercentageCore/` (e.g., `Package.swift`, one source file per type, `Tests/…`)

**Deliverables**
- `docs/CORE_API_CONTRACT.md`
- `docs/CORE_FILE_LAYOUT.md`

**Acceptance Criteria**
- API signatures described in prose (no code)
- File tree planned precisely

---

## 8) App Structure Plan (No Code)

**Goal:** Define app targets, folders, screens.

**Prompt for Cursor**  
Create `docs/APP_STRUCTURE.md` specifying:
- Targets: `UniversalPercentageCalculator` (app), `…UITests`
- Folders under `App/Sources/App`:  
  - `Design/` (glass card, theme, haptics abstractions)  
  - `Components/Controls/` (percent slider, numeric input sync)  
  - `Components/Charts/` (simple bar/pie stubs)  
  - `Features/Home/`  
  - `Features/Tip/`, `Discount/`, `Tax/`,  
    `Business/ProfitMargin/`,  
    `Finance/ROI/`, `Finance/CompoundInterest/`, `Finance/Stocks/`, `Finance/MutualFunds/`,  
    `Generic/PercentChange/`
- Screen responsibilities: inputs, interactions (sliders/steppers), solve action, result, optional chart
- Navigation: Home → feature screens

**Deliverables**
- `docs/APP_STRUCTURE.md`

**Acceptance Criteria**
- Concrete folders/screens; consistent patterns across features

---

## 9) Xcode Project Generation Plan (No YAML Yet)

**Goal:** Describe XcodeGen spec precisely.

**Prompt for Cursor**  
Create `docs/XCODEGEN_SPEC.md` that specifies what `xcodegen/Project.yml` must contain:
- App target (iOS 16+), sources path, resources path, `Info.plist` location
- UI tests target
- Local Swift Package dependency: `Modules/PercentageCore`
- Instructions: install XcodeGen; run generation; open project
*(Do not generate the YAML yet—this is a spec.)*

**Deliverables**
- `docs/XCODEGEN_SPEC.md`

**Acceptance Criteria**
- Unambiguous inputs for generating `Project.yml` later

---

## 10) Non-Functional Requirements

**Goal:** Guardrails for quality.

**Prompt for Cursor**  
Create `docs/NFRS.md` detailing:
- **Precision:** decimal math for money; where/when to round
- **Performance:** <100ms recompute; 60fps slider updates
- **Accessibility:** contrast, Dynamic Type, VoiceOver
- **Privacy:** offline-first; no network by default; optional telemetry (opt-in)
- **Errors:** plain language, localized, consistent placement

**Deliverables**
- `docs/NFRS.md`

**Acceptance Criteria**
- NFRs map to QA checks and are testable

---

## 11) Release Roadmap

**Goal:** Phased delivery with gates.

**Prompt for Cursor**  
Create `docs/ROADMAP.md`:
- **v1.0:** core calculators, Liquid Glass base, i18n basics, unit/UI tests
- **v1.1:** reverse-tax auto-detect, grade calculator, favorites/history, share result cards
- **v1.2:** widgets, Apple Watch mini-calculators, more locales & RTL polish, SIP contributions/fees in finance

**Deliverables**
- `docs/ROADMAP.md`

**Acceptance Criteria**
- Milestones include brief acceptance criteria

---

## 12) Build & Test with Cursor (MCP)

**Goal:** Document how to run builds/tests from Cursor.

**Prompt for Cursor**  
Append to `README.md` a section **Build & Test with Cursor (MCP)** that explains how to:
- Run **project discovery**
- Generate the project with **XcodeGen** (command and steps)
- Build the **app target**
- Run **unit tests** for `PercentageCore`
- Run **UI tests**
List the exact MCP workflow names/buttons to click in Cursor.

**Deliverables**
- Updated `README.md`

**Acceptance Criteria**
- Anyone can build/test via Cursor without guessing

---

## 13) Implementation Prompts Library (No Code)

**Goal:** Ready-made prompts for later codegen.

**Prompt for Cursor**  
Create `docs/PROMPTS_IMPLEMENTATION.md` with **copy-paste prompts** (no code) to generate:
- Core package files & unit tests (one prompt per file group)
- App screens and shared components (one prompt per feature)
- Localization files & sample strings
- Charts stubs (bar/pie)
- UI tests skeletons  
Each prompt must reference the relevant spec doc and acceptance criteria.

**Deliverables**
- `docs/PROMPTS_IMPLEMENTATION.md`

**Acceptance Criteria**
- Prompts are specific, point to specs, and avoid leaking implementation details here

---

## 14) Definition of Done (v1)

**Goal:** One page that must turn fully green.

**Prompt for Cursor**  
Create `docs/DEF_OF_DONE_V1.md` listing v1.0 completion gates:
- All calculators implemented per spec with validation & rounding
- Consistent Liquid Glass visuals and accessibility checks passed
- Unit tests: ≥90% coverage for `PercentageCore` hot paths
- UI tests: happy paths for every feature
- Localization present for all keys in `en` + at least one non-English language
- README build/test instructions verified on a clean machine

**Deliverables**
- `docs/DEF_OF_DONE_V1.md`

**Acceptance Criteria**
- Items are objective, testable, and map back to earlier docs

---

## 15) Backlog (Post-v1 Ideas)

**Goal:** Capture stretch items without scope creep.

**Prompt for Cursor**  
Create `docs/BACKLOG.md` with prioritized ideas:
- Currency converter helper (optional)
- Grade calculators (weighted, target score)
- SIP contributions & fees in CI and MF flows
- Shareable result cards (social images)
- Data export of recent calcs (CSV/JSON)
- Apple Watch standalone mini calculators
- In-app tutorial for percentage concepts (micro-lessons + sliders)

**Deliverables**
- `docs/BACKLOG.md`

**Acceptance Criteria**
- Prioritized list with brief value statement per item

---

## 16) Final Readiness Gate

**Goal:** Ensure everything needed to start coding is in place.

**Prompt for Cursor**  
Validate presence and completeness of:
- `docs/ARCHITECTURE.md`
- `docs/CALCULATORS_SPEC.md`
- `docs/UI_DESIGN_LIQUID_GLASS.md`
- `docs/I18N_L10N.md`
- `docs/QA_TESTPLAN.md`
- `docs/CORE_API_CONTRACT.md`
- `docs/CORE_FILE_LAYOUT.md`
- `docs/APP_STRUCTURE.md`
- `docs/XCODEGEN_SPEC.md`
- `docs/NFRS.md`
- `docs/ROADMAP.md`
- `docs/PROMPTS_IMPLEMENTATION.md`
- `docs/DEF_OF_DONE_V1.md`
- `docs/BACKLOG.md`
…and `.cursor/mcp.json`.

Create `docs/READINESS_REPORT.md` summarizing any gaps (should be none).

**Deliverables**
- `docs/READINESS_REPORT.md`

**Acceptance Criteria**
- Report states the repo is ready for generation & build, or lists specific gaps