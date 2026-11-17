# LotLogic Pro

**A universal position-sizing and trade calculator for traders.**

LotLogic Pro combines two practical workflows in one browser-based application:

1. **Risk-based position sizing** — estimate a position size from a fixed cash-risk amount or a percentage of your account balance.
2. **Fixed-lot trade calculation** — enter the lot size or quantity you intend to trade and estimate possible profit, loss, margin and account impact.

The instrument catalogue is grouped by asset class: Forex, Indices / CFDs, Metals / Commodities, Stocks, Futures, Crypto and Other/custom instruments. The interface also supports System, Light and Dark appearance modes.

> **Important:** LotLogic Pro is an estimate calculator. It is not connected to MetaTrader 5 (MT5), a broker, an exchange or live market data. Results depend on the values you enter. Always verify contract and trading specifications with your broker before placing an order.

---

## 1. Project overview

The project started as a position-size calculator. It was expanded into one universal tool that keeps the original risk-based calculator and adds an MT5-style fixed-lot workflow. Both modes are available in the same application and share the instrument, account and trade inputs.

The design goals were to:

- Keep both calculation modes in one application.
- Group instruments by asset class so the symbol list is easier to navigate.
- Allow broker-specific contract and point-value inputs.
- Present important estimates together in a results dashboard.
- Make the interface responsive and provide light, dark and system themes.
- Keep the app simple to run without installation, a backend or a database.

## 2. How it was built — development steps

The current project is a standalone web app made with HTML, CSS and vanilla JavaScript.

1. **Start with position sizing.** The original purpose is to calculate a position size from account balance, chosen risk and stop-loss distance.
2. **Add a fixed-lot calculation mode.** This second workflow lets a trader enter a lot size or quantity directly and estimate a trade without asking the calculator to choose the size.
3. **Combine both workflows.** A calculation-mode selector switches between risk-based sizing and fixed-lot calculation in the same interface.
4. **Organize the asset catalogue.** Add grouped symbols for Forex, Indices / CFDs, Metals / Commodities, Stocks, Futures and Crypto, plus a custom-symbol option.
5. **Add broker-specific inputs.** Provide contract units, point value, account-currency conversion, leverage and fees because these can vary by broker and instrument.
6. **Create the results dashboard.** Display size, notional exposure, estimated stop-loss loss, take-profit profit, risk/reward, break-even win rate, margin and balance after the modeled outcomes.
7. **Add a price-level visual.** A simple price ladder marks entry, stop-loss and take-profit.
8. **Add input checks and warnings.** Validate required values and warn about incorrect stop/target direction, insufficient risk for the minimum rounded size, and estimated margin or loss exceeding balance.
9. **Design the interface.** Use responsive CSS, dashboard tiles, a teal/coral visual identity and System, Light and Dark appearance options.
10. **Document and package the project.** Keep the app self-contained in index.html with this README and a .gitignore file in the repository root.

### Technology

- **HTML:** page structure, labels, fields and results.
- **CSS:** layout, responsive design, visual styling and themes.
- **Vanilla JavaScript:** instrument lists, validation, calculations and live result updates.
- **Browser local storage:** remembers the appearance selection on the current browser/device.

There is no framework, build step, server-side code, database, MT5 connection or broker API in this version.

## 3. Project files

- **index.html** — the complete application, including its HTML, CSS and JavaScript.
- **README.md** — this build, usage and calculation guide.
- **.gitignore** — ignores common operating-system, editor and log files.

## 4. How to run LotLogic Pro

### Option A — Open locally

1. Download or clone this repository.
2. Open the project folder.
3. Open index.html in a modern browser such as Chrome, Edge or Firefox.
4. The calculator should load directly. No installation or build command is required.

### Option B — Use a local Python server

Open a terminal in the project folder and run:

    python -m http.server 8000

Then visit http://localhost:8000 in your browser. Press Ctrl+C in the terminal to stop the server.

### Option C — Publish with GitHub Pages

1. Open the LotLogic-Pro repository on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select the main branch and the /(root) folder.
5. Save the settings.
6. GitHub Pages will publish the site and show its URL in the Pages settings.

## 5. How to use the calculator

### Step 1 — Choose the calculation mode

Use the Calculation mode selector.

- **Position sizing (risk-based):** choose this when you know the maximum amount you want to risk and want the calculator to estimate the position size.
- **Trade calculator (enter lot size):** choose this when you already know the lot size or quantity and want to estimate the trade outcome.

### Step 2 — Select an asset class and instrument

Choose an asset class:

- Forex
- Indices / CFDs
- Metals / Commodities
- Stocks
- Futures
- Crypto
- Other

Then select an instrument from its grouped list. For Other, select the custom instrument option and type the symbol yourself.

The symbol catalogue is a convenience list, not an official broker instrument list. Brokers may use different symbol names and contract specifications.

### Step 3 — Enter account details

- **Account balance:** the balance amount used for the estimates.
- **Account currency:** the currency in which account-level results are displayed.

### Step 4 — Enter the trade details

- **Trade direction:** Buy / Long or Sell / Short.
- **Entry price:** the planned entry price.
- **Stop-loss price:** the price at which the modeled loss is calculated.
- **Take-profit price:** the planned target price.
- **Total fees / commission:** estimated round-trip fees in the account currency.

Make sure the stop-loss and take-profit are on the correct sides of entry for the chosen direction.

### Step 5 — Enter broker and instrument specifications

These values can vary significantly between brokers and products:

- **Contract units per lot:** the contract multiplier used for estimated notional exposure.
- **Point value:** the account-currency value of a 1.0 price-unit move for one lot/unit. The app uses this directly in its profit/loss calculation.
- **Notional conversion:** a conversion multiplier used for the notional and margin estimate.
- **Leverage:** enter 100 to represent 1:100 leverage.
- **Fees:** enter estimated round-trip costs in the account currency.

Check your broker's symbol specification or contract details. Do not assume these values are universal across Forex, indices, CFDs, stocks, futures or crypto.

### Step 6A — Use risk-based position sizing

When Position sizing (risk-based) is selected:

1. Choose Fixed cash risk or Percentage of account.
2. Enter the amount or percentage you are prepared to risk.
3. Optionally choose one of the percentage shortcut buttons.
4. Enter the entry and stop-loss prices to define the stop distance.
5. Review the calculated position size and estimated loss.

This version rounds risk-sized quantity down to 0.01 increments. If the risk budget is too small to produce at least 0.01, the app warns that the result rounds to zero.

### Step 6B — Use fixed-lot trade calculation

When Trade calculator (enter lot size) is selected:

1. Enter the lot size or quantity you plan to trade.
2. Enter the entry, stop-loss and take-profit prices.
3. Confirm fees, contract units, point value, conversion and leverage.
4. Review estimated loss at the stop, profit at the target, margin and other results.

This mode does not choose a lot size. It calculates estimates using the quantity you enter.

### Step 7 — Understand the results

The results panel can show:

| Result | What it means |
|---|---|
| Calculated position size | Risk-sized quantity or the fixed quantity entered |
| Position notional | Estimated exposure using quantity, contract units, entry and conversion |
| Loss if stop-loss hits | Estimated loss including entered fees |
| Profit if take-profit hits | Estimated profit after entered fees |
| Risk / reward ratio | Estimated net reward compared with estimated net risk |
| Break-even win rate | Theoretical win rate implied by the modeled net risk/reward |
| Required margin (estimate) | Estimated notional divided by entered leverage |
| Balance after stop-loss | Starting balance minus estimated loss |
| Balance after take-profit | Starting balance plus estimated profit |
| Risk / reward as % of balance | Estimated loss and profit as percentages of balance |
| Notional / account balance | Estimated exposure as a percentage of balance |
| Estimated margin level | Starting balance divided by estimated margin, shown as a percentage |

The price ladder visually marks the entry, stop-loss and take-profit levels. Warnings appear when the app detects selected input conditions that need attention.

### Step 8 — Choose the appearance

Use the Appearance selector to choose:

- System theme
- Light mode
- Dark mode

The selected option is remembered in the current browser on that device.

## 6. Calculation conventions

The current implementation uses these calculation conventions:

- Stop distance = absolute difference between entry and stop-loss.
- Target distance = absolute difference between take-profit and entry.
- Gross stop-loss amount = quantity × stop distance × point value.
- Gross take-profit amount = quantity × target distance × point value.
- Estimated net loss = gross stop-loss amount + entered fees.
- Estimated net profit = gross take-profit amount − entered fees.
- Estimated notional = quantity × contract units × entry × notional conversion.
- Estimated margin = estimated notional ÷ leverage.
- Risk-sized quantity = (risk budget − fees) ÷ (stop distance × point value), rounded down to 0.01 increments.

The point-value input is treated as the account-currency value of a 1.0 price-unit move for one lot/unit. The conversion input is used for notional and margin; it is not applied a second time to the profit/loss formula. Configure point value for the account currency you are using.

The displayed margin level is a simplified estimate based on starting balance divided by estimated margin. A broker may calculate margin level using equity, used margin and other rules.

## 7. Limitations and risk notice

LotLogic Pro is an educational and planning calculator, not financial advice or a trade execution system.

This version does not automatically retrieve:

- Live prices or quotes.
- Broker contract specifications.
- MT5 account data or open positions.
- Live exchange rates.
- Broker-specific margin tiers or margin rules.

Spread, slippage, swaps, funding, taxes, price gaps, commissions not entered by the user, liquidation rules, minimum/maximum volume and broker lot-step constraints can affect real results. The calculator's 0.01 sizing increment may not match every instrument's permitted volume step.

Estimated margin uses a simplified notional-divided-by-leverage formula and may differ from a broker's margin method. The accuracy of results depends on the inputs and assumptions. Always verify the values against your broker's platform and specifications before placing a trade. Trading can result in losses, including losses greater than the planned amount in fast-moving or gapping markets.

## 8. Possible future improvements

Ideas for later versions include:

- Save and load user-defined instrument specifications.
- Add configurable lot steps and minimum/maximum volume rules.
- Add more account currencies and conversion helpers.
- Add downloadable calculation reports.
- Add automated tests for the calculation formulas.
- Add broker-specific profiles, but only when their specifications can be verified.

These are suggestions for future development, not features claimed to exist in the current version.

## 9. Contributing

1. Fork the repository.
2. Create a feature branch.
3. Make a focused change.
4. Test both calculation modes and the light/dark themes in a modern browser.
5. Submit a pull request explaining the change and the tests performed.

## 10. License

No license has been selected yet. Until a license is added, standard copyright applies; do not assume that reuse, redistribution or modification is automatically permitted.
