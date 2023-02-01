# Akash Network Economics 2.0 Proposal

## Purpose

This proposal is intended to be a starting point for discussion in the [sig-economics][sig-economics] to propose a working group to complete the design and implementation of ideas presented in this proposal after a rigourous review and feedback from the community. The proposal is not intended to be a final version of the Akash Network Economics 2.0, but rather a starting point.

## Motivation

The initial version of [Akash Economics][akt-economics-1] introduced AKT as the native token, used to secure and pay for the usage of the Akash Network. Although this version was effective for bootstrapping, certain limitations require addressing to ensure sustainability and scalability for the network.

Limitations of the first version of Akash economics:

* The Akash Network requires AKT to pay for hosting, and the price is determined by agreement between the provider and tenant when they begin the lease. This can be a problem if a workload like a website needs to run for a long time because AKT prices could differ significantly over its duration, leaving either the tenant or the provider paying too much or too little compared to what was initially agreed upon.

* Akash Network is in its infancy with early Product Market Fit where with a growing demand but not yet suffcient for providers to commit large amounts of compute. 
* The community fund is too small to incentivize the growth of the Akash Network.
* The AKT token needs to accrue value beyond incentives to ensure the security of the network.

## Network Security is proportional to AKT value

The Akash Network is secured through its Proof-of-Stake consensus, which requires stakers to use the AKT token as a stake. The more AKT that is staked, the greater the security of the network. The value of AKT is driven by demand, so as the network's usage increases, its value must also increase to guarantee maximum security for all participants.

As proposed in the original economics [paper][akt-economics-1], the initial supply of AKT at genesis, $t=0$, is defined as $M_0 = 10^8$ with the maximum supply of AKT computed at $M_{max}\approx3.89 M_0$ and $M_{max} - M_0$ tokens distributed to AKT stakers throughout the network's lifetime as a reward for securing the network. The reward is distributed in each block with the amount is determined by network parameters defined in [Cosmos SDK `x/mint` module][cosmos-sdk-x-mint].

These network parameters are set through on-chain governance and adhere to a decay function that reduces the inflation rate over time. As the reward amount reduces over time, it becomes less attractive to AKT holders to lock up their tokens by staking, thus reducing the security of the network.

## Take and Make Fees

Since the value of AKT is driven by demand, we propose that the network tax the hosting fees paid by tenants to the providers and allocate it to the security budget of the network. This ensures a direct alignment between the usage and security of the Akash Network.

Akash is a decentralized exchange where the health of the marketplace depends on the liquidy of the commodity its trading — compute. We propose that Tenant pay a take fee when _taking_ liquidity from the marketplace and a **_make fee_** that a Provider pays when _making_ liquidity available to the marketplace. The take fee is deducted from the Order when created and `Make Fee` is set by the network through on-chain governance. 

We anticipate AKT holders will choose a fee that is high enough to ensure the security of the network and not too high which impedes the network's usage and growth along with it.

The fees collected are then placed in `Incentive Distribution Pool` to be distributed in a manner described later in this proposal.

## Stable Payment and Settlement with Multi-Currency Support

We propose that the Akash Network implement a multi-token settlement mechanism to allow for using stable tokens to pay for hosting to allow users to predict the cost of hosting upfront. Whitelisting of tokens could be done through on-chain governance.

Additionally, each whitelisted currency is assigned a `Fee Discount Rate`, $R_d$ that is set by the network through on-chain governance. The discount is applied to the `Take Fee` and `Make Fee` during payment or settlement. Since it is in the best interest of AKT holders to encourage the use of AKT for payment and settlement, we expect the discount to be attractive when using AKT. When set to 100%, the network charges no fees for AKT users.

## Incentive Distribution Pool

The Incentive Distribution Pool contains a basket of whitelisted currencies and AKT that is distributed to the network participants as a reward for their contributions to the network. This pool is funded by the fees collected from the `Take Fee` and `Make Fee` as described above and inflationary rewards.

The pool is distributed to the below set of participants. The portions of the pool allocated to each participant is determined by the network through on-chain governance.

![IDP](https://raw.githubusercontent.com/gosuri/akt20/main/akt20.drawio.svg)

### Provider Subsidies

Early on in the network's lifecycle, the network will need to subsidize providers to ensure the network has enough computing power to offer attractive prices to tenants.

There are numerous ways to subsidize providers, some considerations are:

* Cover cost of the operational and amortized cost of the hardware for a period of time.
* Incentivize based on amount wokload they host, similar to [Filecoin Plus][filecoin-plus] Program.
* Use an "exponential discount model" described in Evolution of the Akash Network Token Economics [blog post][akt-evolution].

### Developer Fund

We propose a portion of the Tokens from the `Incentive Distribution Pool` be allocated to the Developer Fund to incentivize the growth of the Akash Network. The Developer Fund is a pool of AKT that is distributed to developers who build applications on the Akash Network. The Developer Fund is distributed through on-chain governance.

The mechanism for distributing the Developer Fund will be determined by the [Steering Committee][streeing-committee].

### Stakers

A portion of the fees collected is distributed to AKT stakers as a reward for securing the network.

### Community Pool

We propose a portion of the fees collected is distributed to the community pool to be distributed through on-chain governance to grow the community.

### Burn Remaining Tokens

All the fees denominated in non-AKT tokens are traded for AKT using a decentralized exchange, like [Osmosis][osmosis], and burned along with the AKT in the pool. 

TODO: Gas fees and slippage are not accounted for in this proposal. We need to determine how to account for these fees.

## Calculations

We define $F_t$ as the `Take Fees` collected by the network for the deployment and can be expressed as:

$F_t = \digamma_0 \cdot R_t \cdot (1 - R_d)$

And, $F_m$ as the `Make Fees` collected by the network for the deployment, can be expressed as:

$F_m = \digamma_0 \cdot R_m \cdot (1 - R_d)$, where,  

$\digamma_0$ is the `Hosting Fee` amount offered by Tenant for the deployment

$R_t$ is `Take Fee Rate`, set by the network through on-chain governance,

$R_m$ is the `Make Fee Rate`, set by the network through on-chain governance, and, 

$R_d$ is `Fee Discount Rate` for the Token, set by the network through on-chain governance. where,

$R_t, R_m, R_d \in [0, 1]$. 

Then, the Fees collected by the network for the deployment is

$F_n = \digamma_0 \cdot (1 - R_d) \cdot (R_t + R_m)$

The fees on the order offered to the Provider is $F_p = \digamma_0 - F_t$ , or:

$F_p = \digamma_0 \cdot (1 - R_t \cdot (1 - R_d))$

[akt-economics-1]: https://ipfs.io/ipfs/QmdV52bF7j4utynJ6L11RgG93FuJiUmBH1i7pRD6NjUt6B
[cosmos-sdk-x-mint]: https://docs.cosmos.network/main/modules/mint
[osmosis]: https://osmosis.zone/
[streeing-committee]: https://github.com/akash-network/community/tree/main/committee-steering
[sig-economics]: https://github.com/akash-network/community/tree/main/sig-economics
[akt-evolution]: https://akash.network/blog/an-evolution-of-akash-network-token-economics/
[filecoin-plus]: https://docs.filecoin.io/store/filecoin-plus/overview/