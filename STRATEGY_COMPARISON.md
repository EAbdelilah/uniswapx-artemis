# Strategy Comparison: UniswapX Atomic Filler vs. Cross-DEX MEV Bot

This document compares the current **UniswapX Atomic Filler** with the **Ethereum-BNB MEV Bot** strategy described [here](https://github.com/sorasuzukidev/ethereum-bnb-mev-bot/blob/master/docs/STRATEGY.md).

## Comparison at a Glance

| Feature | UniswapX Atomic Filler (Current Bot) | Traditional Cross-DEX MEV Bot |
| :--- | :--- | :--- |
| **Strategy Type** | Intent Fulfillment (Filler) | Cross-DEX Arbitrage |
| **Opportunity Source** | Off-chain API (UniswapX Orders) | On-chain Mempool / State changes |
| **Execution** | Atomic Fill via Reactor | Atomic Flashloan + Multiple Swaps |
| **Competition** | Intent fillers (Professional Market Makers) | Arbitrage bots (MEV Searchers) |
| **Capital Requirement** | High (for inventory) or Flashloans | Low (Flashloans are central) |
| **Risk Profile** | Low (Atomic transaction) | Low (Atomic transaction) |

---

## Detailed Profitability Analysis

### 1. UniswapX Atomic Filler (Current)
This bot profits by filling **off-chain user intents**.
- **Edge**: You are acting as a "filler" for Uniswap users. You profit when the price a user is willing to pay (their signature) is higher than the current on-chain price (Uniswap v2/v3).
- **Profitability Factor**: Highly dependent on the "decay" of the Dutch auction. As time passes, the user's price becomes more favorable for the filler.
- **Competition**: Extremely high. You are competing against professional market makers (like Wintermute, etc.) who have highly optimized solvers.

### 2. Traditional Cross-DEX MEV Bot
This bot profits by exploiting **on-chain price discrepancies** between different exchanges (e.g., Uniswap vs. SushiSwap).
- **Edge**: You profit from market inefficiencies. If someone makes a large trade on Uniswap and moves the price, you buy on SushiSwap and sell on Uniswap to rebalance the market.
- **Profitability Factor**: Dependent on high-frequency monitoring and low-latency execution. Profit scales with market volatility and trading volume across DEXes.
- **Competition**: Saturated. Thousands of bots monitor every block for these exact opportunities.

---

## Which one is more profitable?

### Short Answer:
**The UniswapX Atomic Filler generally has access to higher volume, but the Traditional MEV Bot is "simpler" to get started with for small-scale opportunities.**

### Long Answer:
1. **Scalability**: The **UniswapX Filler** is more scalable for professional shops because UniswapX handles a massive percentage of Uniswap's total volume. The opportunities are "guaranteed" to exist as long as people use UniswapX.
2. **Barrier to Entry**: The **Traditional MEV Bot** is more accessible to individual developers because it doesn't require complex "solver" logic or high-tier integration with the UniswapX ecosystem—just standard on-chain monitoring.
3. **Execution Speed**: In the MEV bot scenario, speed is everything. In UniswapX, "solving" (finding the best route) and having the reputation/infrastructure to be an exclusive filler (for certain order types) is more important.

### Conclusion
If you have **highly optimized routing and gas logic**, the **UniswapX Atomic Filler** is likely more profitable due to the sheer volume of "intents" being posted. If you are looking for **"low-hanging fruit"** and have very low-latency RPC access, a **Traditional Cross-DEX Bot** might find small, niche inefficiencies that larger players ignore.
