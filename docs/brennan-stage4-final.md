## Stage 4 – Final FX Hedge Analysis, AI Prompt, and Recommendation

### A. Exposure Summary

Our firm expects to receive €12,500,000 in one year from a European customer. Because the firm reports in U.S. dollars, the final USD value of this receivable depends on the EUR/USD exchange rate at settlement. If the euro weakens against the dollar before the payment date, the same €12.5 million receivable will convert into fewer U.S. dollars. This creates cash flow uncertainty and could negatively affect revenue, margins, and budgeting.

The purpose of the hedge model is to compare several strategies for managing this exposure: no hedge, forward hedge, money market hedge, long put option, and long call option. The main decision is whether the firm should prioritize certainty, upside flexibility, or lower upfront cost.

---

### B. Summary of Hedge Outcomes

| Strategy           |                                         Key Result | Interpretation                                                        |
| ------------------ | -------------------------------------------------: | --------------------------------------------------------------------- |
| No Hedge           |               About $13.46 million at current spot | Full exposure to EUR/USD movement                                     |
| Forward Hedge      |                               About $13.64 million | Locks in a certain USD value                                          |
| Money Market Hedge |                               About $13.64 million | Synthetic forward result, close to forward hedge                      |
| Long Put           | About $13.18 million at current spot after premium | Provides downside protection but has an upfront cost                  |
| Long Call          | About $13.00 million at current spot after premium | Less useful for a EUR receivable because it caps upside after premium |

The no hedge strategy provides the most flexibility but also leaves the firm fully exposed to exchange rate changes. The forward hedge gives the cleanest certainty by locking in the EUR/USD rate today. The money market hedge produces a similar result to the forward hedge because it replicates the same economics through borrowing, converting, and investing. The put option provides protection against euro depreciation while still allowing upside if the euro strengthens, but that flexibility comes at a premium cost. The call option is included for comparison, but it is not the best fit for this receivable because the firm’s main risk is euro depreciation, not appreciation.

---

### C. Sensitivity Interpretation

The Stage 2 model tests ending spot rates across a ±5% range around the current spot rate. This makes it easier to see how each strategy behaves if the euro depreciates or appreciates.

If the euro depreciates, the no hedge strategy performs worst because USD proceeds fall directly with the exchange rate. The forward and money market hedges protect against this risk because their proceeds remain fixed. The put option also protects the downside by creating a minimum value, although its result is reduced by the premium cost.

If the euro appreciates, the no hedge strategy benefits the most because the firm receives more dollars for each euro. The forward and money market hedges do not participate in this upside because the exchange rate is locked in. The put option performs better than the forward in stronger euro scenarios only if the appreciation is large enough to overcome the option premium. This is the main trade-off: the forward gives certainty, while the put keeps upside potential but costs money.

---

### D. Strategic Recommendation

I recommend using the forward hedge for this receivable.

The main reason is that the receivable is large enough that even small EUR/USD movements could create a material change in USD cash flow. The forward hedge locks in approximately $13.64 million and removes uncertainty from the transaction. For a CFO, this is valuable because it supports better budgeting, revenue planning, and margin protection.

The put option is also defensible because it protects the downside while preserving upside. However, in this model, the premium cost reduces the expected USD proceeds enough that the forward hedge looks more attractive for a firm focused on cash flow certainty. The money market hedge produces a similar economic result to the forward hedge, but it is more operationally complicated because it requires borrowing, converting, and investing. Therefore, the forward hedge is the cleanest and most practical strategy.

---

### E. Executive Justification

The forward hedge best matches the firm’s need for predictable cash flows. It avoids the downside risk of a weaker euro and provides a known USD amount today. This makes it easier for management to plan around expected revenue and reduces the chance that exchange rate volatility creates an unexpected earnings shortfall.

The main downside is opportunity cost. If the euro strengthens, the firm will not benefit from the favorable move. However, given the size of the receivable and the purpose of hedging, this trade-off is acceptable. The goal is not to speculate on currency movements. The goal is to protect the business from volatility that is unrelated to its core operations.

The money market hedge reaches a similar result, but it is less attractive because it uses more balance sheet activity and adds operational steps. The put option provides useful optionality, but its premium cost makes it less attractive unless management has a strong view that the euro could appreciate meaningfully. Overall, the forward hedge is the best recommendation because it is simple, cost-effective, and directly aligned with cash flow stability.

---

### F. Structured AI Prompt to Regenerate the FX Hedge Spreadsheet

# GOAL

Create an Excel workbook that models FX hedging strategies for a USD-based firm expecting to receive a EUR-denominated receivable. The workbook should compare no hedge, forward hedge, money market hedge, long put option, and long call option strategies. It should calculate USD proceeds under each strategy and include a sensitivity table and chart across ending spot rate scenarios.

# INPUT VARIABLES

Use the following named ranges exactly:

| Named Range |                 Description |      Value | Unit        |
| ----------- | --------------------------: | ---------: | ----------- |
| FC_AMT      | Foreign-currency receivable | 12,500,000 | EUR         |
| S0_in       |      Spot rate at inception |     1.0765 | USD/EUR     |
| F0_in       |                Forward rate |     1.0910 | USD/EUR     |
| R_USD       |           USD interest rate |       3.7% | Annual rate |
| R_FC        |           EUR interest rate |       2.3% | Annual rate |
| K_PUT       |           Put option strike |     1.0765 | USD/EUR     |
| K_CALL      |          Call option strike |     1.0765 | USD/EUR     |
| PREM_PUT    |         Put premium per EUR |     0.0225 | USD/EUR     |
| PREM_CALL   |        Call premium per EUR |     0.0369 | USD/EUR     |
| T_DAYS      |          Days to settlement |        365 | Days        |

# SPREADSHEET STRUCTURE

Create two tabs:

1. Main Model
2. Notes & Assumptions

On the Main Model tab, include the following sections:

1. Inputs section
2. Assumptions section
3. Hedge calculation section
4. Summary output section
5. Sensitivity table
6. Sensitivity chart

Use this color coding:

* Yellow = editable inputs
* Blue = assumptions
* Green = formulas and intermediate calculations
* Gray = outputs and key performance indicators

# MODEL LOGIC

No Hedge:

Calculate USD proceeds as:

USD proceeds = FC_AMT × S_T

Forward Hedge:

Calculate locked-in USD proceeds as:

USD proceeds = FC_AMT × F0_in

Money Market Hedge:

Show the hedge in three steps:

1. Borrow EUR today equal to the present value of the receivable:

Borrowed EUR = FC_AMT / (1 + R_FC × T_DAYS / 365)

2. Convert borrowed EUR into USD at the spot rate:

USD today = Borrowed EUR × S0_in

3. Invest USD at the U.S. interest rate:

USD proceeds = USD today × (1 + R_USD × T_DAYS / 365)

Put Option Hedge:

Calculate net USD proceeds as:

USD proceeds = FC_AMT × max(K_PUT, S_T) − (FC_AMT × PREM_PUT)

Call Option Hedge:

Calculate net USD proceeds as:

USD proceeds = FC_AMT × min(K_CALL, S_T) − (FC_AMT × PREM_CALL)

# SENSITIVITY TABLE

Create a sensitivity table where ending spot rate S_T ranges from 0.95 × S0_in to 1.05 × S0_in in 1% increments.

For each S_T value, calculate USD proceeds for:

* No hedge
* Forward hedge
* Money market hedge
* Long put option
* Long call option

Create a line chart comparing all strategies across the S_T range.

# VERIFICATION

Include the following checks:

1. Forward hedge proceeds should be close to money market hedge proceeds.
2. No hedge should increase as S_T increases.
3. Forward and money market hedge lines should be flat across all S_T scenarios.
4. Put option should provide downside protection after premium.
5. Call option should show capped proceeds after premium.
6. All formulas should be transparent and auditable. Do not use hidden calculations or macros.

# NOTES & ASSUMPTIONS TAB

Include a Notes & Assumptions tab stating:

* Interest rates are annual and use simple compounding.
* No transaction costs or bid-ask spreads are included.
* Option premiums are illustrative.
* The model is for educational analysis and not live trading execution.
* Settlement occurs in 365 days.

# EXPORT

Save the workbook as:

brennan-kevin-stage4-fx-hedge-model.xlsx

The workbook should be clean, professional, and understandable to a treasury analyst reviewing it for the first time.

---

### Extra Credit: Areas for Further Study and Improvement

AI automation could improve this model by pulling live exchange rates, interest rates, and option premiums into the workbook automatically. Instead of manually entering spot rates and assumptions, an AI tool could update the model using current market data and regenerate the sensitivity analysis on demand. A more advanced version could also run Monte Carlo simulations to estimate a range of possible USD proceeds rather than only using a ±5% table.

GitHub also adds value because it creates an audit trail for the project. Each memo, model, spec, and final recommendation can be committed and reviewed later. This makes the analysis more reproducible because another analyst can see how the model changed over time. In a real treasury or audit setting, this kind of version control would help support documentation, review, and governance.
