# Car Deal Calculator

A simple, single-page calculator that shows whether **trading in** your car or **selling it for cash** is the better deal, at each dealer you're considering, after sales tax and financing.

It's one `index.html` file with no build step, no backend and no tracking.

## What it does

The page is laid out as a decision tree:

```
              Your current car
     (still owe · best cash offer · cash down)
                     │
        ┌────────────┴────────────┐
     Dealer 1                  Dealer 2        (up to 3)
  price, fees, APR…         price, fees, APR…
     ┌────┴────┐               ┌────┴────┐
 Trade in   Sell for       Trade in   Sell for
   here    cash, buy        here    cash, buy
              here                     here
```

Every path gets a net cost, and the cheapest one is highlighted.

- **Sales tax by state.** Pick a state to fill in its vehicle tax rate and trade-in rule. The rate stays editable.
- **Trade-in tax credit.** In most states a trade-in lowers the taxable price and a cash sale doesn't. The page handles the exceptions:
  - No credit in California, Hawaii, Virginia and DC.
  - Michigan's credit is capped.
  - South Carolina's $500 fee cap.
- **Connecticut luxury rate.** An optional toggle applies 7.75% to vehicles over $50,000.
- **Dealer discounts vs. manufacturer rebates.** Discounts lower the taxable price; rebates don't (based on Connecticut's rule).
- **Loan payoff.** On a trade-in, the dealer pays off your loan and any shortfall is rolled into the new loan. On a cash sale, the payoff comes out of the sale and the rest goes toward the new car.
- **Financing.** Shows monthly payment, total interest and amount financed. Leave APR and months blank if paying cash.
- **Shareable links.** Your numbers are saved in the page URL, so a copied link or bookmark reopens with everything filled in.
- **Mobile friendly.** On phones the tree runs top to bottom.

## How net cost is calculated

```
net cost = price − dealer discount − manufacturer rebate
         + dealer fees + title & registration
         + sales tax + loan interest
         − what you get for your car (trade-in or cash offer)
         + what you still owe on it
```

Sales tax is applied to `price − discount + dealer fees − trade-in credit`, following the selected state's trade-in rule.

## Tax rates disclaimer

The built-in table has **state-level rates only**, last checked **November 2026**. It doesn't include county or city taxes, and rates change. Always confirm your actual rate with your state's DMV or tax department and enter it in the **Sales tax %** field.

To update a rate, edit the `STATES` table near the top of the script in `index.html`. Each row looks like this:

```js
["CT", "Connecticut", 6.35, "full", "7.75% applies to vehicles over $50,000.", { luxRate: 7.75, threshold: 50000 }],
//code  name          rate%  trade-in credit: "full" | "none" | "cap"   note    optional extras
```

## Run it

Open `index.html` in any browser.

## Publish on GitHub Pages

1. Put `index.html` (and this README) in a GitHub repository.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, and save.
4. The site will be live at `https://<your-username>.github.io/<repo-name>/` in a minute or two.

## Privacy

Nothing is sent to a server. Your numbers stay in your browser (local storage) and in the page URL. Anyone you share a link with can see the numbers in it.

## Disclaimer

This calculator gives estimates for comparison only. It isn't financial or tax advice. Dealer fees, local taxes and lender terms vary, so check the final numbers on your purchase contract.

## Author

Built by [Viyaleta Apgar](https://www.linkedin.com/in/viyaleta/) · [GitHub](https://github.com/viyaleta) · [Buy me a coffee](https://buymeacoffee.com/viyaleta)
