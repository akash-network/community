### Stable payment and take rate

Stable payments aim to assuage resource planning concerns around a volatile alternative asset, making the experiences for both providers and tenants on Akash Network more consistent and accessible. This will clear the path for more tenants to deploy more workloads to Akash Network and make the value proposition for providers clearer while lowering the barrier to entry for both. Supporting native USDC will enable greater access across the board for both sides of the marketplace.

### Phase 1 - MVP
This should be the absolute minimum viable build we need to get this off the ground and implemented as rapidly as possible. This phase should only include:
1. USDC support natively. 
   - Payment and settlement will be in the same currency. USDC -> USDC or AKT -> AKT. No swapping.
2. Basic and simplest form of the take rate: deduct 20% from the provider’s settlement. Providers will just have to price their bids higher to accommodate.
3. Module account with no multi-sig distribution and only governance control. Not sure if this is needed for phase 1 or if it can be held back for later if it increases speed.
4. USDC transactions will still use AKT for gas. 

### Final Specification [Draft]
This spec outlines the features and details for phase 1 of the stable payments enhancement set, which includes: stable payments, settlements, and take rate. This is an MVP with further phases to follow that will be defined and scoped shortly after the completion of this spec.

#### USDC implementation
1. Only Axelar USDC on Osmosis will be the stable currency supported on Akash Network to start. 
    
    <img width="254" alt="image" src="https://user-images.githubusercontent.com/68354230/228345109-ab3d4ecc-2325-453a-8d03-54da6005cf3a.png">
    
    _Versions to be left for future discussions: Axelar USDC directly on Akash Network, Gravity USDC, issuance chain USDC._  
2. We also benefit from the Kado onramp Osmosis already supports:
    
    <img width="347" alt="image" src="https://user-images.githubusercontent.com/68354230/228345384-2bcfa102-8b0a-469b-8a8b-cde10cfe40f3.png">
3. Wallet support (Keplr). Akash Network’s implementation of USDC should mirror what is currently supported by Keplr for Osmosis, which includes the ability to view, send, and receive USDC with gas paid in the native coin.
4. Create a table of supported currencies and their respective take rates that can be updated by governance proposals. The table should look like this for phase 1 of this implementation. 
    | Currency | Take Rate |
    | --- | --- | 
    | AKT | 4% |
    | Axelar USDC (Osmosis) | 20% |

#### Take rate 
1. Initial USDC take rate is set to 20%. 
2. To be executed only upon withdrawal of funds by providers.
3. Take rates should be unique to each currency (see table above) and should be adjustable by governance independent of each other. 

#### SDL & Escrow
1. Currency selection to be enabled in the SDL where the tenant can designate a specific currency like AKT, USDC, or ALL.
2. Tenants should be able to query for providers based on currency parameters (USDC or AKT). 
3. Escrow accounts should be able to house and interact properly with USDC.
4. Escrow minimum amounts need to be defined for each new currency. AKT is uAKT, what’s needed for USDC?
5. Providers should be able to bid on leases based on currency. If a provider only wants to bid on jobs paid in USDC, they can filter out AKT jobs.
7. Enabling provider settlement in USDC from escrow. This is probably redundant with a previous point, but calling out for completeness. 

#### Module account update (community pool)
1. Ensure support for Osmosis’ version of Axelar USDC. This means the ability to hold and interact (send and receive) this version of USDC. 
2. USDC balances, transactions, and history should be visible on block explorers. 

#### Network Upgrade 
1. Required because of state change.
2. Testnet(s): probably requires two testnets per Artur (one for Akash and one for Osmosis)  

#### Education
1. Providers need to be educated about the take rate and how they should incorporate this added cost to their pricing methodologies. 
2. Tenants might need to be educated that there are potential cost benefits to paying for jobs in AKT vs USDC b/c providers will charge more to compensate for the take rate applied to their revenue.
3. Ecosystem partners: praetor, cloudmos, spheron, etc should be educated.
4. Once a spec is finalized and posted on our GH, we can open up a simultaneous discussion thread on GH and discord to answer any questions, receive ideas and feedback, and address concerns.
5. Vanguards and insiders should be educated and equipped to help answer questions.
6. Documentation. Updated documentation for this is probably necessary. 

#### Marketing GTM
1. Once the spec is live on Github, create Twitter thread laying out the high-level details with a link to the spec on Github.
2. Cross-post the thread to all of Akash’s other social channels (Telegram, Reddit, Discord).
3. Host a community-led AMA discussing the mechanics of the features, potential use-cases, and impact on the network.
4. Condense AMA content into a blog post, which will be posted to akash.network and amplified on social.
