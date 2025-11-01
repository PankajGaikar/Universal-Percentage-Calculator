# Calculators Spec (v1)

Each calculator defines: Inputs, Outputs, Validation, Edge Cases, Display Formatting.

---

## 1) Tip
- **Inputs:** billAmount, tipPercent (0–100), splitCount (≥1), rounding (none/total/per-person optional)
- **Outputs:** tipAmount, totalAmount, perPersonAmount
- **Validation:** splitCount ≥ 1; negative bill invalid
- **Edge Cases:** large split counts; high tips; zero bill
- **Display:** currency for amounts; percent with 1 decimal optional

## 2) Discount
- **Inputs:** originalPrice, discountPercent (0–100+ clamp)
- **Outputs:** newPrice, savedAmount
- **Validation:** clamp discountPercent to [0, 100]; non-negative price
- **Edge:** discount > 100 → clamp; zero price
- **Display:** currency for prices; show saved

## 3) Tax (Add & Reverse)
- **Inputs:** price, taxPercent (0–100), mode (add|reverse)
- **Outputs:** priceWithTax (add) or basePrice (reverse)
- **Validation:** reverse divisor must not be zero
- **Edge:** very high tax rates; rounding accumulation
- **Display:** currency

## 4) Profit Margin / Markup
- **Inputs:** any two of {cost, sellPrice, marginPercent}; optionally compute markupPercent
- **Outputs:** marginPercent, markupPercent, profit, solved price/cost
- **Validation:** cost ≥ 0; sellPrice > 0 where required
- **Edge:** cost=0; sell=cost (0% margin)
- **Display:** currency & percent

## 5) ROI
- **Inputs:** initial, final, period (years optional)
- **Outputs:** absolutePercent; if period provided → annualizedPercent (CAGR)
- **Validation:** initial > 0; period > 0 for annualized
- **Edge:** loss (negative %); zero gain
- **Display:** percent to 2 decimals

## 6) Compound Interest
- **Inputs:** principal, ratePercent, years, compoundsPerYear (n∈{1,2,4,12})
- **Outputs:** futureValue, interestEarned
- **Validation:** principal ≥ 0; years > 0; n ≥ 1
- **Edge:** long horizons; high n
- **Display:** currency; optional chart over time

## 7) Stock Profit/Loss
- **Inputs:** buyPrice, shares, sellPrice, fees (optional)
- **Outputs:** profitAmount, profitPercent
- **Validation:** buyPrice > 0; shares > 0
- **Edge:** high fees; small spreads
- **Display:** currency & percent

## 8) Mutual Fund CAGR
- **Inputs:** initial, final, years
- **Outputs:** cagrPercent
- **Validation:** initial > 0; years > 0
- **Edge:** negative growth
- **Display:** percent (2 decimals)

## 9) Percentage Change / Difference
- **Inputs:** from, to
- **Outputs:** deltaPercent (signed), direction (up/down/flat)
- **Validation:** from ≠ 0 (else show guidance)
- **Edge:** from close to zero
- **Display:** percent (2 decimals), arrow icon maybe