# PIP Revenue Share Reporting

Public transparency reporting for the **PIP Spot and Reservation Revenue Share** program, as authorized by Akash Network [Governance Proposal #329](https://www.mintscan.io/akash/proposals/329) (passed June 25, 2026).

This repository houses the periodic reports that Overclock Labs (OCL) committed to publishing under the proposal: gross revenue, management fees retained, net remittance to the Akash Community Pool, and capacity utilization for PIP3.5-funded GPU compute.

## Background

The amendment was drafted and discussed publicly in [akash-network discussion #1408](https://github.com/orgs/akash-network/discussions/1408) (opened by `isaac9905` on June 3, 2026 in the Economics category) before going on-chain as Proposal #329.

It sits within the lineage of prior Provider Incentive Pilots — the original [PIP](https://www.mintscan.io/akash/proposals/246), extended by [PIP02](https://www.mintscan.io/akash/proposals/273), [PIP03](https://www.mintscan.io/akash/proposals/303), and [PIP3.5](https://www.mintscan.io/akash/proposals/315) — under which program revenue was returned to the Community Pool "net of expenses." This amendment replaces that open-ended expense deduction with a calibrated, transparent rate while leaving unchanged OCL's Provider Performance Administrator (PPA) designation, its scope of responsibility, the underlying capital allocation, and the Community Pool's status as primary beneficiary.

Proposal #329 amends PIP3.5 by replacing the prior open-ended "net of expenses" treatment with a fixed two-tier management fee applied to gross revenue collected from leases settled against PIP3.5 capacity:

| Revenue type | OCL management fee | Community Pool net remittance |
|---|---|---|
| **Spot** | 10% | 90% |
| **Reservation** | 30% | 70% |

**Spot revenue** comes from leases settled through the open Akash marketplace without prior commitment. **Reservation revenue** comes from leases backed by a forward capacity commitment — reserved instance contracts, committed compute arrangements, and capacity sold through a direct commercial channel. All reserved contracts are managed on-chain.

### Fee composition

**Spot — 10% of gross**

| Component | % of gross |
|---|---|
| Fiat processing fees | 4% |
| Trading fees and spread (USD→AKT conversion) | 1% |
| Price exposure risk for managed deployments and other fees | 5% |
| **Total** | **10%** |

**Reservation — 30% of gross**

| Component | % of gross |
|---|---|
| Fiat processing fees | 4% |
| Trading fees and spread (USD→AKT conversion) | 1% |
| Price exposure risk for managed deployments and other fees | 5% |
| Demand sourcing and direct sales | 10% |
| Counterparty risk compensation (SLAs) | 10% |
| **Total** | **30%** |

### What the fees compensate

The management fees recognize OCL's commercial role alongside its administrative role. Per the discussion, sustaining near-full utilization in a supply-constrained market requires:

- **Demand matching** — direct sales for reservation deals, tenant relationship management, and extended supply sourcing.
- **USD-to-AKT settlement** — absorbing processing costs, conversion spread, and timing so tenants can transact in dollars without ever holding AKT. All network spend drives open-market purchases of AKT, which are burned to mint ACT; OCL bridges fiat processing and AKT/ACT conversion for managed deployments.
- **Counterparty risk** — forward capacity commitments under reservation contracts expose OCL to default, reallocation, and SLA-enforcement risk that does not exist for spot.

## Program performance

Since PIP3.5 was authorized, demand-sourcing work has materially expanded both pricing and utilization on PIP3.5 capacity relative to the program's original assumptions.

**Per-GPU pricing** — PIP3.5 assumed spot pricing at OCL's operating cost per GPU; current market spot pricing is materially higher:

| GPU | PIP3.5 launch ($/hr) | Current Akash market ($/hr) | Change |
|---|---|---|---|
| H100 | $1.50 | $2.69 | +79% |
| H200 | $2.00 | $3.59 | +80% |
| A100 | $0.82 | $1.34 | +63% |

**Utilization** — climbing across GPU classes into June 2026:

| GPU | PIP3.5 stated | May actual | June projected |
|---|---|---|---|
| H100 | 59.30% | 78.31% | 80% |
| H200 | 57.34% | 78.97% | 80% |
| A100 | 61.61% | 49.40% | 100% |
| RTX 5090 | — | 85.69% | 85% |

**Aggregate revenue impact** — comparing PIP3.5 launch to now:

| Metric | Daily avg. Feb 2026 | Daily avg. May 2026 | June 2026 projected |
|---|---|---|---|
| Weighted avg. utilization | 58.87% | 72.10% | 85.00% |
| Daily network gross revenue | $2,296.73 | $4,949.70 | $7,500\* |
| Annualized network gross revenue | $838,306 | $1,806,641 | $2,737,500 |
| % increase from Feb 2026 | — | 115.1% | 226.6% |

<sub>\* Based on full A100 utilization and projections from a May 28, 2026 daily spend of $7,130.</sub>

## Reporting commitments

Under the proposal, OCL publishes:

- **Monthly settlement** — the management fee is applied and the net remittance is sent to the Community Pool monthly, denominated in AKT.
- **Quarterly reports** — published within 30 days of quarter-end, covering gross revenues, management fees retained, net remittance to the Community Pool, aggregate capacity utilization, and any classification or settlement notes for the period.
- **June 2026 report** — an additional standalone report for June 2026, published within 60 days of on-chain approval.

The first standard reporting period is **Q3 2026**, with reports published here as they are released.

## Verification

All flows are verifiable on-chain. Funds received and funds returned to the Community Pool can be tracked via the program wallet:

```
akash177gvgfknw3g99xqyjczpygjmqphw924dnk6zdz
```

## Scope and duration

- **Scope:** revenue collected from PIP-funded GPUs through on-chain leases.
- **Effective:** the first day of the calendar month following on-chain approval, with the framework initiated retroactively as of **June 1, 2026**.
- **Duration:** remains in effect indefinitely until amended or terminated by a subsequent governance proposal.
- The management fee replaces the open-ended expense deduction in prior PIPs for the duration of this amendment.

## Repository structure

```
reports/
  2026/
    q3/            # quarterly reports
    june-2026/     # standalone June 2026 report
data/              # supporting datasets (revenue, utilization, remittances)
```

## References

- Governance Proposal #329 — [Mintscan](https://www.mintscan.io/akash/proposals/329)
- Discussion — [akash-network GitHub discussion #1408](https://github.com/orgs/akash-network/discussions/1408)

---

*Maintained by Overclock Labs (OCL). This repository is a public record of program reporting and does not modify the terms set by on-chain governance.*
