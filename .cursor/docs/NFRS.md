# Non-Functional Requirements

## Precision & Rounding
- Decimal math for currency; avoid float drift.
- Banker’s rounding at display boundaries.

## Performance
- Recompute under 100ms on mid-range devices.
- Slider scrubbing maintains 60fps (debounce formatting & charts).

## Accessibility
- VoiceOver labels for inputs/results/units.
- Dynamic Type across screens; no clipped text.
- Contrast-safe over translucent backgrounds.

## Privacy & Offline
- No network calls by default.
- Optional analytics/telemetry (opt-in) documented; no PII.

## Errors
- Plain-language, localized, short and specific.
- Consistent placement near the related input/result.

## Reliability
- Deterministic core logic with unit tests for edge cases.