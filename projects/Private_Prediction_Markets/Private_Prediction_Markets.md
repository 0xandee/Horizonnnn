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

**Validation Research Findings:**

⚠️ **ICP Hypothesis Partially Invalidated** (October 2025 research):
- Whale traders research shows sophisticated actors DON'T primarily want privacy—they use reputation and visible positions strategically
- Example: French whale "Theo" ($85M profit) motivated by mathematics, not privacy
- Top traders use leaderboard for credibility and to attract exit liquidity providers
- Existing privacy strategies: Multi-wallet tactics, graduated position building work adequately

**Revised Priority Personas (based on validation):**
1. **Institutional participants** (UPGRADED TO PRIMARY): Hedge funds, family offices, political campaigns needing compliance-grade privacy
2. **Informed insiders** (NEW): Campaign staff, corporate employees, researchers who can't bet due to doxxing/employment risk
3. **Retail manipulation victims** (UPGRADED): Traders losing money to whale copy-trading and front-running
4. ~~Whale traders~~ (DOWNGRADED): Only institutional whales with compliance requirements, NOT reputation-seeking retail whales

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
- **ICP mismatch (CRITICAL)**: Validation research shows primary assumed users (whales) don't want privacy—they want reputation. *Mitigation*: Pivot ICP to institutional players, informed insiders, and manipulation victims. Conduct 10+ institutional interviews to validate demand before MVP build. If institutional PMF is weak, consider pivoting to B2B privacy layer for Polymarket or prediction market insurance product.
- **Liquidity bootstrapping paradox**: Encrypted order books prevent market makers from seeing depth, leading to inefficient pricing and fragmented liquidity. *Mitigation*: Research Penumbra DEX and other privacy DEX approaches to liquidity. Consider hybrid model where aggregate order book depth is visible but individual positions remain private. May need liquidity mining incentives or institutional anchor users.
- **Regulatory scrutiny**: CFTC actively cracking down on U.S.-accessible prediction markets. Privacy features may attract money laundering concerns. *Mitigation*: Legal review before launch. Consider optional privacy-preserving KYC for compliance (zk-identity). May need to geo-block U.S. or partner with regulated entity like Kalshi for U.S. market access.
- **Oracle manipulation remains unsolved**: 24hr delay doesn't fix UMA-style governance attacks where dispute resolution itself is manipulated. *Mitigation*: Acknowledge that encrypted positions don't solve oracle trust—may need multi-oracle consensus from day one, not post-MVP. Consider oracle insurance or dispute insurance mechanism.
- **Settlement delay competitive disadvantage**: 24hr delay makes capital lockup worse than Polymarket, reducing attractiveness for time-sensitive markets. *Mitigation*: Accept tradeoff for privacy in MVP. Explore faster finality options with multi-oracle parallel verification. Consider premium for instant settlement with higher oracle requirements.

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

- **ICP validation**: Is institutional demand strong enough to sustain the platform? Should we abandon retail whale focus entirely? What minimum institutional commitment ($10M+? $50M+?) proves PMF before building MVP?
- **Pivot vs persist**: If institutional validation is weak, should we pivot to B2B privacy layer (partner with Polymarket) or prediction market insurance (compensate manipulation victims) instead of building standalone platform?
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
- **October 2025 status**: $200B+ cumulative volume, $2B weekly volume, 1.3M+ users, 58K daily active users
- Settled with CFTC ($1.4M fine, 2022), FBI investigation closed (2025)
- **Re-entering U.S. market** via QCX acquisition (regulated derivatives exchange)
- **Funding**: $9B valuation, $2B recent funding from ICE
- **Rumored POLY token launch** 2025
- Centralized platform—can censor users, freeze accounts, block jurisdictions.
- All positions are public—vulnerable to front-running, herding, and manipulation.
- **Documented manipulation**: UMA Zelensky suit market ($160M), Nobel Prize front-running ($68K), systematic copy-trading ecosystems
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

**Kalshi** (https://kalshi.com)
- U.S.-regulated prediction market (CFTC-approved derivatives exchange)
- **October 2025 status**: $5B valuation ($300M Series D)
- **Robinhood integration** capturing 60%+ market share (September 2025)
- Heavy KYC requirements (passport, SSN) for regulatory compliance
- Transparent positions like all traditional platforms
- *Difference*: We provide privacy that U.S. regulation prohibits, but may partner for compliant institutional access. Kalshi proves institutional demand exists if properly structured.

---

## 13) Validation Research Appendix

### Research Methodology
- **Period**: October 2025
- **Sources**: Polymarket user discussions, market data analysis, whale behavior research, Aztec technical assessment
- **Scope**: Privacy pain points, manipulation incidents, whale motivation, technical feasibility, competitive landscape

### Key Findings Summary

**Problem Validation: STRONG ✅**
- Privacy concerns are real and actively impacting Polymarket users
- Multiple documented manipulation incidents:
  - **UMA Zelensky market** (March 2025): Whale manipulated $7M Ukraine market via UMA governance attack
  - **Zelensky suit controversy** (July 2025): $160M market disputed after UMA token holders manipulated resolution
  - **Nobel Peace Prize front-running** (October 2025): Whale account @dirtycup placed $68K hours before announcement
  - **Systematic copy-trading**: Stand.trade built whale-watching Discord bot; traders making $10K+/month copying positions
  - **Tail-end manipulation**: Veteran trader "Fish" describes whales crashing prices 0.99→0.9 to trigger panic, then buying back
  - **Concentration risk**: 5 whale accounts controlled 50% of Trump "Yes" shares in 2024 election; one whale controlled 29.1%

**User Pain Points (from discussions):**
- **Doxxing/targeting**: Polymarket data collection (browser, device, OS, location) enables targeting. U.S. users face DOJ investigation risk
- **Front-running**: Public order books enable coordination. Wash trading common to inflate volumes
- **Manipulation**: 7+ documented examples. One trader lost $20K in single UMA manipulation incident
- **Copy-trading**: Traders explicitly state they watch real-time whale positions for "quick reaction"

**ICP Validation: WEAK ⚠️**
- **Whale traders DON'T want privacy** (invalidates primary persona):
  - French whale "Theo": $85M profit, 4+ accounts, motivated by "mathematics and odds more than politics"
  - Top traders use reputation as trading signal—"love the clout" of visible positions
  - Leaderboard provides credibility and attracts copycats who provide exit liquidity
  - Existing privacy tactics work: Multiple pseudonymous wallets, graduated position building, timing strategies
- **Revised target**: Institutional players, informed insiders, retail manipulation victims (NOT reputation-seeking whales)

**Technical Feasibility: MODERATE ⚠️**
- **Aztec network status**:
  - ✅ Adversarial Testnet launched May 2025 (15K+ nodes)
  - ✅ Mainnet targeting late 2025
  - ✅ 8+ years development, $100M raised (a16z-led)
  - ⚠️ "Fully private transactions have more data... we are fine with that... we never need to be as cheap as other L2s" (tradeoff acknowledged)
- **Critical challenges**:
  - **Oracle trust unsolved**: UMA manipulation showed dispute resolution is the vulnerability. 24hr delay doesn't fix governance attacks. Encrypted positions don't solve this.
  - **Liquidity bootstrapping**: Encrypted order books = blind market makers = inefficient pricing. Zero-knowledge DEXs face severe fragmentation.
  - **Settlement delay**: 24hr delay = worse UX than Polymarket's instant resolution = competitive disadvantage
  - **Sybil resistance**: Without KYC, one whale could create 1000 encrypted accounts (potentially worse manipulation)

**Market Size: MODERATE ✅**
- **Polymarket metrics** (October 2025):
  - $200B+ cumulative volume
  - $2B weekly volume (record high)
  - 1.3M+ total users, 58K daily active users
  - $358B+ open interest
  - Sports markets: $414.7M weekly volume
  - Politics markets: $322.6M weekly volume
  - Top 2 markets alone: $602M volume
- **Concentration**: Most volume in high-liquidity viral events (elections, sports) where whale watching is most prevalent
- **Implication**: Privacy concerns most acute in exact markets with most volume = strong product-market alignment

**Competitive Landscape:**
- **Polymarket moat**: CFTC settlement, re-entering U.S. via QCX, $9B valuation, rumored token launch
- **Kalshi alternative**: U.S.-regulated, $5B valuation, Robinhood integration, 60%+ market share Sept 2025
- **Regulatory environment**: CFTC actively cracking down. Polymarket paid $1.4M fine and still got raided. Privacy features = higher regulatory risk.

### Validation Recommendations

**CRITICAL DECISION POINT:**
Before proceeding to MVP build, validate institutional demand:
1. **Conduct 10+ institutional interviews** (hedge funds, family offices, political campaigns)
   - Target question: "Would you commit $10M+ to private prediction markets for hedging/research if compliant?"
   - Success threshold: 5+ institutions express strong interest
   - Timeline: 2-4 weeks

2. **Informed insider validation** (campaign staff, corporate employees, researchers)
   - Target question: "Does doxxing risk prevent you from using prediction markets?"
   - Success threshold: 15+ potential users confirm blocking factor
   - Timeline: 2-3 weeks

**IF VALIDATION WEAK → Consider pivots:**
- **B2B privacy layer**: Partner with Polymarket/Kalshi for institutional private pools (easier regulatory path)
- **Prediction market insurance**: Compensate manipulation victims using encrypted proofs (clearer value prop)
- **Privacy for creators, not traders**: Encrypt market creation, not positions (lower technical lift)

**IF VALIDATION STRONG → Proceed with revised strategy:**
- Primary ICP: Institutional players (not retail whales)
- Partnership approach: Don't compete with Polymarket, offer privacy as feature layer
- Regulatory: Legal review + privacy-preserving KYC for compliance
- Technical: Study Penumbra DEX liquidity solutions before building

### Sources
- Polymarket user discussions (X/Twitter, Reddit)
- Market manipulation incidents (Web3isgoinggreat, Coindesk, Bloomberg reports)
- Whale behavior research (news.polymarket.com, trader interviews)
- Aztec technical status (aztec.network blog, Coindesk technical coverage)
- Competitive landscape (funding announcements, regulatory filings, market data)
