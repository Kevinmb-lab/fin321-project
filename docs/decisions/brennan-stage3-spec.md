## FX Hedge Model – Technical Specification

### 1. Problem Statement

The firm expects to receive €12,500,000 in one year from a European customer. This creates foreign exchange exposure because the USD value of the receivable depends on the EUR/USD exchange rate at settlement.

If the euro depreciates relative to the U.S. dollar, the firm will receive fewer USD, negatively impacting revenue and margins. The purpose of this model is to evaluate hedging strategies that reduce this risk and stabilize cash flows.

---

### 2. Inputs (Known Variables)

| Named Range | Description                 | Unit     | Value      |
| ----------- | --------------------------- | -------- | ---------- |
| FC_AMT      | Foreign-currency receivable | EUR      | 12,500,000 |
| S0_in       | Spot rate at inception      | USD/EUR  | 1.0765     |
| F0_in       | Forward rate                | USD/EUR  | 1.0910     |
| R_USD       | USD interest rate           | Annual % | 3.7%       |
| R_FC        | EUR interest rate           | Annual % | 2.3%       |
| K_PUT       | Put option strike           | USD/EUR  | 1.0765     |
| K_CALL      | Call option strike          | USD/EUR  | 1.0765     |
| PREM_PUT    | Put premium per EUR         | USD      | 0.0225     |
| PREM_CALL   | Call premium per EUR        | USD      | 0.0369     |
| T_DAYS      | Days to settlement          | Days     | 365        |

---

### 3. Assumptions & Constraints

* Interest rates are treated as annual and applied using simple compounding
* No transaction costs, bid-ask spreads, or fees are included
* Forward and money market hedge parity is assumed
* Option premiums are illustrative and not based on real-time market quotes
* Settlement occurs exactly in 365 days

---

### 4. Calculation Flow

The model calculates USD proceeds for each hedging strategy using the following logic:

#### No Hedge

Convert the foreign currency at the ending spot rate:

USD proceeds = FC_AMT × S_T

---

#### Forward Hedge

Lock in the exchange rate using a forward contract:

USD proceeds = FC_AMT × F0_in

---

#### Money Market Hedge

Replicate a forward contract through borrowing and investing:

Borrow FC → convert at spot → invest USD → compute final USD proceeds

USD proceeds = (FC_AMT / (1 + R_FC)) × S0_in × (1 + R_USD)

This result should closely match the forward hedge outcome.

---

#### Option Hedges

**Long Put**

Provides downside protection:

USD proceeds = FC_AMT × max(K_PUT, S_T) − (FC_AMT × PREM_PUT)

This establishes a minimum USD value.

---

**Long Call**

Limits upside exposure:

USD proceeds = FC_AMT × min(K_CALL, S_T) − (FC_AMT × PREM_CALL)

This caps gains while accounting for premium cost.

---

### 5. Outputs

The model produces:

* USD proceeds for each strategy
* A sensitivity table showing outcomes across exchange rate scenarios
* A chart comparing strategy performance across the range of S_T

Primary output:

**Sensitivity Table: USD Proceeds by Strategy vs. S_T**

---

### 6. Model Review — What Worked & What to Improve

The model successfully computes USD proceeds for all hedging strategies and generates a working sensitivity table and chart. The forward and money market hedge results align closely, supporting the assumption of interest rate parity.

However, improvements can be made. The money market hedge implementation was simplified, and a more detailed breakdown of each step would improve transparency. The use of named ranges throughout the Excel model could also be expanded to enhance clarity and reduce reliance on direct cell references.

Additionally, the option pricing inputs are simplified and could be improved using real market data. The model structure could be further refined by separating intermediate calculations more clearly and enhancing auditability.

---

### 7. Sensitivity Plan

The sensitivity analysis varies the ending spot rate (S_T) across a ±5% range around the initial spot rate (S0_in).

* Range: 0.95 × S0_in to 1.05 × S0_in
* Step size: approximately 1% increments

For each S_T value, USD proceeds are calculated for all strategies. The results are displayed in both tabular and graphical form.

This allows decision-makers to compare downside risk, upside potential, and overall performance across strategies.

---

### 8. Limitations & Next Steps

This model excludes several real-world factors:

* Dynamic hedging adjustments
* Credit risk and counterparty considerations
* Hedge accounting treatment
* Transaction costs and liquidity constraints

Future enhancements could include:

* Incorporating live market data
* Expanding sensitivity ranges
* Adding probabilistic scenario analysis
* Automating the model using Excel data tables

This specification serves as the foundation for Stage 4, where an AI-generated model and final hedge recommendation will be developed.

