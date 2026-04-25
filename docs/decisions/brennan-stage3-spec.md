## FX Hedge Model – Technical Specification

### 1. Problem Definition

This model evaluates the foreign exchange risk associated with a EUR-denominated receivable. The firm expects to receive €12,500,000 in one year, and the USD value of this payment is exposed to fluctuations in the EUR/USD exchange rate.

The purpose of this model is to compare multiple hedging strategies and show how each one affects USD proceeds under different exchange rate scenarios.

---

### 2. Inputs

The model uses a centralized inputs section so all assumptions can be easily adjusted. Key inputs include:

* Foreign currency receivable: €12,500,000
* Spot exchange rate (USD/EUR)
* Forward exchange rate (USD/EUR)
* USD 1-year interest rate
* EUR 1-year interest rate
* Time to maturity (365 days)
* Put option strike price
* Call option strike price
* Put option premium (USD per EUR)
* Call option premium (USD per EUR)

All inputs are clearly labeled and highlighted to distinguish them from calculated values.

---

### 3. Model Logic

The model calculates USD proceeds for four strategies.

#### No Hedge

The firm converts EUR to USD at the future spot rate:

USD proceeds = FC × S_T

This represents full exposure to exchange rate risk.

---

#### Forward Hedge

The forward contract locks in a fixed exchange rate:

USD proceeds = FC × forward rate

This removes uncertainty and guarantees a fixed USD outcome.

---

#### Money Market Hedge

The money market hedge replicates a forward contract:

1. Borrow EUR today equal to the present value of the receivable
2. Convert EUR to USD at the spot rate
3. Invest USD at the domestic interest rate

USD proceeds = (FC / (1 + r_EUR)) × S₀ × (1 + r_USD)

This should produce a value very close to the forward hedge.

---

#### Option Hedges

**Long Put**

Provides downside protection while keeping upside potential:

USD proceeds = FC × max(K_put, S_T) − premium

This creates a floor on USD proceeds.

---

**Long Call**

Caps the upside after accounting for premium:

USD proceeds = FC × min(K_call, S_T) − premium

This limits gains but provides controlled exposure.

---

### 4. Sensitivity Analysis

The model includes a sensitivity table that varies the ending spot rate across a ±5% range around the current spot rate.

* Ending spot rate ranges from 0.95×S₀ to 1.05×S₀
* USD proceeds are calculated for each strategy
* Results are displayed in both a table and a chart

This allows for direct comparison of how each strategy performs under different market conditions.

---

### 5. Outputs

The model produces:

* USD proceeds for each hedging strategy
* Comparison between hedged and unhedged outcomes
* A chart showing performance across exchange rate scenarios

These outputs help evaluate trade-offs between risk and return.

---

### 6. Limitations and Improvements

This model uses simplified assumptions:

* No transaction costs or bid-ask spreads
* Annual interest rate compounding
* Estimated option premiums rather than real market quotes

Possible improvements include:

* Using real market data
* Expanding the sensitivity range
* Adding probability-weighted scenarios
* Automating calculations with Excel data tables

---

### 7. Model Structure and Implementation Details

The model is organized into two main tabs: “Main Model” and “Notes & Assumptions.”

The Main Model tab includes:

* An inputs section (top left)
* Hedge calculations (middle section)
* Sensitivity table (bottom section)
* Chart for visualization

Key formulas used:

* No hedge: USD = FC × S_T
* Forward hedge: USD = FC × forward rate
* Money market hedge: USD = (FC / (1 + r_EUR)) × S₀ × (1 + r_USD)
* Long put: USD = FC × max(K_put, S_T) − premium
* Long call: USD = FC × min(K_call, S_T) − premium

The sensitivity table applies these formulas across all spot rate scenarios.

This structure ensures the model is transparent, easy to follow, and can be rebuilt by another analyst.
