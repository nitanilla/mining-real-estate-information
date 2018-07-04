## Real Estate Finance Formulas/Calculations

<p>I urge you to look at the repo and specifically the underlying index.js file and see if you need to edit some code to get the data formatted in another way.</p>

<p>Note: I took out the console logs so it only returns a value. If you would like to console log the return value, just wrap a console log around the function</p>

<p>Note: if any of the arguments are irrelevant just place a 0 in it's proper place. It must still be there or else the function will throw an error</p>

<code>npm install --save real-estate-finance</code>

<code>
    import * as refin from 'real-estate-finance' || const refin = require('real-estate-finance');
</code>

## Functions Available

- All inputs are meant to be in their specifc order listed below and all inputs are meant to be Numbers, not Strings or Floats!

- annualGrossPotentialIncome
    <code>
        refin.annualGrossPotentialIncome(expectedMonthlyRentIncome)
    </code>

- netOperatingIncome
    <code>
        refin.netOperatingIncome(
          monthlyIncome,
          vacancies,
          nonPayments,
          taxes,
          mortgageInterest,
          marketing,
          advertising,
          management,
          legal,
          accounting,
          utilities,
          repairs,
          maintenance,
          acquisition,
          sale_costs
        )
    </code>


- grossRentalMultiplier
    <code>
        refin.grossRentalMultiplier(marketValue, annualGrossPotentialIncome)
    </code>

- estimatedPropertyValueByGRM
    <code>
        refin.estimatedPropertyValueByGRM(grossRentalMultiplier, annualIncome)
    </code>

- grossOperatingIncome
    <code>
        refin.grossOperatingIncome(monthlyIncome, estimatedLossPercentage);
    </code>

- capitalizationRate
    <code>
        refin.capitalizationRate(
          monthlyIncome,
          vacancies,
          nonPayments,
          taxes,
          marketing,
          advertising,
          management,
          legal,
          accouting,
          utilities,
          repairs,
          maintenance,
          acquisition,
          sale_costs,
          sale_earned
        )
    </code>

- estimatedPropertyValueByCapRate
    <code>
        refin.estimatedPropertyValueByCapRate(
            netOperatingIncome,
            capitalizationRate
        )
    </code>


- cashFlowBeforeTaxes
    <code>
        refin.cashFlowBeforeTaxes(
          netOperatingIncome,
          interestRate,
          loanPrinciple,
          capitalExpenditures,
          capitalExpenditureLoans,
          earnedInterest
        )
    </code>


- cashFlowAfterTaxes
    <code>
        refin.cashFlowAfterTaxes(
          cashFlowBeforeTaxes,
          stateIncomeTax,
          federalIncomeTax
        )
    </code>


- breakEvenRatio
    <code>
        refin.breakEvenRatio(
          interestRate,
          loanPrinciple,
          marketing,
          advertising,
          management,
          legal,
          accounting,
          utilities,
          repairs,
          maintenance,
          grossOperatingIncome
        )
    </code>


- returnOnEquity
    <code>
        refin.returnOnEquity(
            cashFlowAfterTaxes,
            principleInvested
        )
    </code>
