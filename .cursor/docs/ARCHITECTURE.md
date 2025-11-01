# Architecture

## Layers
- **Core (Modules/PercentageCore)**  
  Pure Swift Package with percentage math logic. No UI, no Apple frameworks. Deterministic, unit-tested.
- **App (SwiftUI in App/)**  
  Screens, state, and visuals (Liquid Glass). Calls Core APIs. Localization & formatting live here.

## Data Flow
SwiftUI View → ViewModel/State → Core API → Result → Formatting (locale, currency, rounding) → Render

## Error Handling
- Core throws typed errors for invalid inputs (e.g., divide-by-zero, negative years, invalid split).
- App maps errors to user-friendly, localized messages.

## Rounding Strategy
- Internal calculations use Decimal where needed (money-sensitive).
- Display: banker’s rounding (to 2 decimals for currency, to 2–4 for percentages as needed).
- Explicit rounding points:  
  1) Input normalization →  
  2) Core returns raw Decimal →  
  3) Display formatting applies rounding.

## Performance
- Recompute under 100ms for typical inputs.
- Slider interactions remain 60fps by debouncing heavy formatting and chart re-layouts.

## Testing
- Core: XCTest with edge cases & precise numeric assertions.
- App: UI tests verify inputs ↔ outputs, slider sync, localization formatting.

## Privacy
- Offline-first. No network calls by default.
- Optional telemetry (opt-in) can be added later (see NFRs).