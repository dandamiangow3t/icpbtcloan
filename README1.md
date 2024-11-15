# icpbtcloan

An ICP canister serving as a BTCdeposit address for lenders to fund and manage loan offers in BTC.

## The solution includes

- handling BTC transactions
- updating balances
- enabling lenders to create custom loan offers, which can then be accepted by borrowers for instant loans

## Flows

1. Deposit Tracking and Balance Management:
    - The canister generates unique BTC deposit addresses for each lender.
    - Upon BTC deposit, the canister has a cron job that:
      - Monitors transactions to the deposit address.
      - Waits for transaction confirmations.
      - Handles cases where transactions are rejected or dropped from the
      mempool.

2. Loan Offer Creation:
    - Allows lenders to create multiple loan offers, each specifying:
      - Exact BTC amount per offer.
      - Specified number of runes (collateral).
      - Maximum Loan-to-Value (LTV) ratio they are willing to accept.
    - Each offer is linked to the lender’s balance and managed securely by the
    canister.
    - For example, if a lender deposits 1 BTC, they can make an infinite amount of
    1BTC offers.

3. Loan Activation and Signing:
    - When a borrower accepts an offer, the canister will:
      - Accept and decode the unsigned BTC transaction for validation.
      - Verify the borrower’s collateral meets the offer requirements.
      - Sign the loan transaction on behalf of the lender, initiating the loan and
      fulfilling BTC and rune requirements for both parties.
      - Simulate, broadcast, and track the loan initiation process.
      - Handle cases where a transaction is rejected or dropped from the
      network.