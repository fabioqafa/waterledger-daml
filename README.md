# DAML Smart Contracts

This system was built as a proof of concept using DAML. There are a number of reasons for this.

- They are related to state workflow changes where DAML excels
- They relate to a created liability, again a strong point for DAML. Ethereum excels at tokenisation, but DAML has rich features for financial instruments 
- The details of the transaction are inherently private, and don’t require public visibility

## Workflow

The flow for this process is to create the `TradeProposal` on the matching of a buyer and seller. This contract is created by a watcher in the WaterLedger API that watches for the Add History event in the Solidity History Smart Contract. 

The implementation of a `TradeProposal` rather than just creating a `NewTrade` directly is due to DAML’s model that a Party cannot have an obligation placed on it without it approving it. Once the `TradeProposal` exists the buyer can exercise the `AcceptTradeIssuance` choice.

Note that the seller does not need to provide any approval as no liability is created on their part. They are listed as an `observer` only, as they have an interest, but they are a beneficiary rather than incurring a liability.

**Note that this is explicitly not desired in production. It is a proof of concept.**

Further features will be added over time, including more robust testing, and potentially the entire OrderBook and matching process.

