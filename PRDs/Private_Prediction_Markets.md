# Private Prediction Markets

## 1) Vision and Value Proposition

**What it is**: A privacy-preserving prediction market platform built on Aztec that mirrors Polymarket's markets and resolution mechanism while keeping user positions completely encrypted. Users trade on real-world events with genuine price discovery while maintaining complete anonymity—positions remain private forever, even after market resolution.

**What it solves**
- Eliminates herding behavior caused by visible positions—traders express true conviction instead of following whales or majority sentiment.
- Prevents front-running and copy-trading by sophisticated actors who exploit public order flow.
- Stops market manipulation through hidden coordination—when resolution votes and stakes are public, whales can influence outcomes (as seen in the UMA Zelensky suit market flip).
- Protects high-conviction traders from being targeted, doxxed, or harassed based on their market positions.

**Expected customer outcome**
Higher quality information aggregation through honest participation, protection from surveillance and targeting, access to Polymarket's deep liquidity and trusted resolution while maintaining complete privacy, and fair market outcomes free from visible coordination or whale manipulation.

---

## 2) Target Users and Needs

**Primary personas**

1. **Whale traders**: Have high conviction on outcomes but don't want to move markets or attract copycats when placing large positions.
2. **Privacy-conscious individuals**: Want to participate in prediction markets without creating permanent public records of their beliefs and financial positions.
3. **Institutional participants**: Need position privacy for compliance, competitive, or reputational reasons when trading on sensitive topics.
4. **Crypto-native traders**: Already use Polymarket but want censorship resistance and privacy that centralized platforms can't provide.
5. **Contrarian traders**: Want to bet against the crowd without being visible targets for coordination or harassment.

**Jobs to be done**

- As a whale trader, I need to place large positions without revealing my size so that I don't move the market or attract front-runners.
- As a privacy advocate, I want to participate in prediction markets without creating a permanent public record of my beliefs.
- As an institutional trader, I need complete anonymity so I can trade on sensitive topics without reputational or regulatory exposure.
- As a contrarian, I want to bet against popular narratives without becoming a target for coordination or social pressure.

---

## 3) Core Use Cases

1. **Private whale trading**: Large trader places $100K position on political outcome without revealing position size or identity, avoids market impact and copycats.
2. **Sensitive topic participation**: User bets on controversial or politically sensitive markets without fear of doxxing or targeting based on their stance.
3. **Anti-herding conviction**: Trader takes contrarian position on popular market, hidden position prevents social pressure and allows genuine price discovery.
4. **Anonymous winnings**: Winner collects large payout from resolved market without revealing identity or creating linkable on-chain trail.
5. **Institutional research**: Fund uses prediction markets for information gathering without revealing trading strategy or research focus areas.

---

## 4) User Experience

### 4.1 Trader flow

1. **Browse markets**: View top 50 Polymarket markets by volume, see aggregate data (total volume, current odds, participant count) without individual positions.
2. **Connect wallet**: Connect Aztec-compatible wallet, deposit funds into privacy pool.
3. **Place encrypted bet**: Select outcome (Yes/No), enter stake amount, submit encrypted transaction to Aztec contract.
4. **Contract execution**: Aztec contract places bet on Polymarket on user's behalf—Polymarket sees only the contract address, not the individual user.
5. **Monitor position**: User views their own encrypted position in wallet, sees updated market odds and aggregate stats, but cannot see other traders' positions.
6. **Market resolution**: Polymarket resolves market → automated oracle reads on-chain outcome → oracle posts encrypted result to Aztec contract after 24hr safety delay.
7. **Claim winnings**: User initiates private withdrawal from Aztec contract, receives funds with complete anonymity, no public record of winnings.

### 4.2 Observer flow

- Browse available markets mirrored from Polymarket top 50 by volume.
- View aggregate market statistics: total volume staked, current probability distribution (e.g., "65% Yes, 35% No"), number of participants.
- See market metadata: question, resolution source, resolution date, categories.
- Cannot see individual positions, bet sizes, or trader identities at any point.

### 4.3 Oracle operator flow

1. **Monitor Polymarket**: Automated oracle watches Polymarket markets for resolution events.
2. **Read on-chain outcome**: When Polymarket market resolves, oracle reads outcome from UMA on Polygon.
3. **Safety delay**: Wait 24 hours to ensure resolution is final and no disputes are active.
4. **Post to Aztec**: Submit encrypted outcome to Aztec smart contract, triggering settlement phase.
5. **Settlement**: Contract enables encrypted payout claims for winners.

---

## 5) Product Features

**MVP**

- Binary (Yes/No) markets only, mirroring top 50 Polymarket markets by volume.
- Encrypted position submission—users place bets through Aztec contract which proxies to Polymarket.
- Privacy-preserving aggregation—show total volume, current odds, and participant count without revealing individuals.
- Automated oracle—reads Polymarket on-chain resolution from UMA, posts to Aztec after 24hr delay.
- Private claiming—winners withdraw funds anonymously, positions remain encrypted forever.
- Individual trade execution—contract places separate trade on Polymarket for each user (simple, no batching).
- No platform fees—prove concept first, monetization later.
- Platform subsidizes Polymarket (Polygon) gas, users pay Aztec gas fees.

**Later**

- Multi-outcome markets (not just binary Yes/No).
- Batched trade execution—combine multiple user bets into single large Polymarket trades for better privacy.
- Early exit mechanism—allow users to sell positions before market resolution at current Polymarket odds.
- Multi-oracle consensus—require 3+ oracles to agree on outcome before settlement.
- Platform fee—1-2% on winnings for sustainability.
- Liquidity buffer—enable instant bet placement and withdrawals without waiting for Polymarket execution.
- User-requested markets—allow users to request specific Polymarket markets outside top 50.
- Advanced privacy—batching, padding, and timing strategies to reduce correlation analysis.

**Not in scope now**

- Creating new markets (all markets are mirrors of Polymarket).
- Dispute resolution (trust Polymarket's UMA-based resolution).
- Limit orders or advanced trading features (MVP is simple bet placement only).
- Cross-chain support beyond Polygon (where Polymarket operates).
- Social features, comments, or discussion forums.

---

## 6) Privacy and Disclosure Policy

- **Private by default**: All individual positions, bet sizes, trader identities, and winnings are encrypted and never revealed publicly—not during trading, not at resolution, not ever.
- **Selective disclosure**: Users can optionally prove their position or winnings to third parties (e.g., for audits) using zero-knowledge proofs, but this is never required or default.
- **Aggregation first**: Only aggregate metrics are visible—total market volume, current probability distribution, and total participant count. These are computed using privacy-preserving aggregation techniques that don't leak individual data.
- **Anti-correlation**: The Aztec contract places individual trades on Polymarket, so Polymarket cannot correlate bet timing or size with specific users. Future versions will add batching, denomination padding, and timing delays to further reduce correlation risks.

---

## 7) Differentiators

- **True privacy for prediction markets**: First platform to offer completely private positions that remain encrypted forever, even after market resolution and payout.
- **Real Polymarket liquidity**: Users get access to Polymarket's deep liquidity, proven resolution mechanism, and high-quality markets without sacrificing privacy.
- **Anti-manipulation**: Hidden positions prevent herding, whale coordination, and the resolution manipulation seen in public markets (UMA dispute gaming).
- **Censorship resistance**: Fully permissionless on Aztec—no centralized operator can freeze accounts, block withdrawals, or censor participation like Polymarket can.
- **No front-running**: Encrypted positions eliminate copy-trading and front-running by sophisticated actors monitoring public mempools.
- **Genuine price discovery**: Removes reputation bias and social pressure—markets reflect true conviction, not visible coordination or following behavior.

---

## 8) Risks and Mitigations

- **Oracle trust**: Relying on single automated oracle to read Polymarket outcomes. *Mitigation*: 24hr delay before settlement allows time to detect and respond to issues; post-MVP add multi-oracle consensus and manual override capability.
- **Polymarket dependency**: Platform is only as reliable as Polymarket's uptime and resolution quality. *Mitigation*: Polymarket is battle-tested with proven UMA resolution; monitor for issues and communicate delays transparently; post-MVP add ability to switch to backup oracle sources.
- **Low initial liquidity**: Users may be hesitant to use platform without proven liquidity and track record. *Mitigation*: Start with top 50 markets by volume to ensure adequate Polymarket liquidity; run awareness campaign highlighting privacy benefits; consider liquidity mining incentives post-MVP.
- **User confusion**: Privacy model and Aztec interaction may be complex for mainstream users. *Mitigation*: Clear onboarding flow with educational content; simple UI that abstracts encryption complexity; tooltips explaining what data is private vs public at each step.
- **Front-running via timing**: User could monitor Polymarket, see odds moving, then quickly bet through privacy app. *Mitigation*: Accept risk for MVP as attack requires precise timing and Polymarket already has arbitrage bots; post-MVP add small time delays or minimum holding periods if abuse detected.
- **Gas cost volatility**: Platform subsidizes Polymarket gas, which could become expensive if Polygon fees spike. *Mitigation*: Monitor gas costs; implement circuit breaker to pause trading if gas exceeds threshold; transition to user-paid gas or fee model if subsidization becomes unsustainable.

---

## 9) MVP Scope

- **Markets**: Top 50 Polymarket markets by volume, binary (Yes/No) only, auto-synced daily.
- **User limit**: No artificial cap, but optimize for up to 1,000 concurrent users in MVP phase.
- **Trade execution**: Individual trades (no batching), placed immediately on Polymarket by contract.
- **Resolution**: Single automated oracle reading UMA on Polygon, 24hr delay before Aztec settlement.
- **Supported wallets**: Any Aztec-compatible wallet (e.g., Aztec Sandbox wallet).
- **Assets**: USDC or primary stablecoin supported on both Aztec and Polymarket.
- **UI**: Simple web interface showing market list, aggregate stats, bet placement form, position tracker, and withdrawal interface.
- **No fees**: Zero platform fees for MVP; users pay Aztec gas, platform covers Polymarket gas.
- **No early exit**: Users must wait until market resolution to claim winnings (no position selling before resolution).

---

## 10) Pricing and Commercial Model

**MVP**: No platform fees—focus on proving the privacy model works and building user trust.

**Post-MVP monetization**:
- Platform fee: 1-2% on profitable positions (only winners pay, similar to Polymarket).
- Potential premium tier: Enhanced privacy features (batching, padding) or priority trade execution for fee.
- Volume-based discounts: High-volume traders get reduced fees to incentivize liquidity.

**Cost structure**:
- Platform subsidizes Polygon gas for Polymarket trades during MVP.
- Users pay Aztec gas fees for all encrypted operations.
- Post-MVP: Transition to user-paid gas across both chains or build costs into platform fee.

---

## 11) Open Questions

- **Oracle decentralization timeline**: When should we add multi-oracle consensus vs keeping simple single oracle? What is the trust/complexity tradeoff for users?
- **Market selection criteria**: Should we stick with top 50 by volume, or add filters (e.g., only crypto markets, only politics)? How often should we refresh the mirror list?
- **Early exit pricing**: When we add position selling before resolution, should we match real-time Polymarket odds or add slippage buffer to prevent arbitrage?
- **Gas sustainability**: How long can we subsidize Polymarket gas? What usage level triggers transition to fees or user-paid model?
- **Batching strategy**: If we batch trades, what is optimal batch size and frequency to balance privacy gains vs trade execution delay?
- **KYC requirements**: Will any jurisdictions or market types require KYC? How do we implement privacy-preserving identity verification if needed?
- **Marketing positioning**: Lead with "private Polymarket" or "censorship-resistant prediction markets"? What resonates most with target users?

---

## 12) Competitive Landscape

**Polymarket** (https://polymarket.com)
- Market leader with deep liquidity and proven UMA resolution.
- Centralized platform—can censor users, freeze accounts, block jurisdictions.
- All positions are public—vulnerable to front-running, herding, and manipulation.
- *Difference*: We offer same markets and resolution but with complete privacy and censorship resistance via Aztec.

**Augur** (https://augur.net)
- Decentralized prediction market on Ethereum.
- Fully transparent—all positions and resolution votes are public on-chain.
- Complex dispute resolution mechanism.
- *Difference*: We provide privacy for positions and leverage Polymarket's simpler, proven resolution instead of complex dispute games.

**Gnosis Prediction Markets** (https://gnosis.io)
- Conditional token framework for prediction markets.
- Transparent on-chain positions.
- Requires market creators to configure resolution mechanism.
- *Difference*: We offer privacy by default and leverage Polymarket's established markets instead of requiring custom market creation.

**UMA Optimistic Oracle** (https://umaproject.org)
- Provides resolution layer for many prediction markets including Polymarket.
- Public dispute and voting system—vulnerable to coordination attacks (e.g., Zelensky market flip).
- *Difference*: We use UMA as data source but prevent visible coordination by encrypting positions and stakes throughout market lifecycle.

**Zeitgeist** (https://zeitgeist.pm)
- Decentralized prediction market protocol on Polkadot.
- Public positions and transparent resolution.
- Focus on creating custom markets.
- *Difference*: We prioritize privacy and leverage existing Polymarket liquidity rather than fragmenting into new market creation.

**Omen** (https://omen.eth.limo)
- Prediction market platform on Gnosis Chain.
- Transparent positions and outcomes.
- Lower liquidity than Polymarket.
- *Difference*: We combine Polymarket-level liquidity with Aztec privacy for best of both worlds.
