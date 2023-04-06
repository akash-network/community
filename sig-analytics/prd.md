# PRD - Growth Analytics for Akash Network

## Background & Context

Growth of Akash Network is driven by a combination of growth in deployments, growth in providers on the network and growth in the community (including contributions to our OSS repositories). In order to understand this growth better, we need to define the metrics that are important to track and build systems that enable us to track and report on those metrics over time.

## Problem Statement

To build & track the right metrics we have to start with the questions we would like answered, figure out a data model that helps us answer those questions and then work on extracting the data according to the schema in the data model, before we can query and report on it.

Broadly the questions we seek answer to can be organized into 4 buckets (reference: [Discussion Thread](https://github.com/orgs/akash-network/discussions/54)):

- Network Usage Metrics
- Provider Network State and Growth Metrics
- User Acquisition, Activation, Retention & Monetization Metrics
- Community (and OSS) growth metrics

These are expanded in the next section of this document

Note that a subset of Provider Metrics will be specifically pertinent to operational aspects (like monitoring uptime and coming up with an SLA). These are out of scope of this document and will be discussed and worked on in [wg-provider-monitoring](../wg-provider-monitoring/README.md)

## Desired Metrics (Question they answer)

### 1. Network Usage Metrics

- **1a**. How many deployments have occurred over time?
- **1b**. How much AKT was spent on deployments over time?
- **1c**. How many leases are created over time?
- **1d**. How many leases are active at a given time?

### 2. Provider Network State & Growth Metrics

- **2a**. How many active providers are in the network over time?
- **2b**. How many total providers (active + inactive) spun up over time?
- **2c**. How much compute capacity was added over time?
- **2d**. How much memory capacity was added over time?
- **2e**. How much storage capacity was added over time?
- **2f**. What was the average up time for the providers on the network?
- **2g**. How often do providers draw funds out of escrow? (understand provider behavior, so we  can figure out how to inform providers about funds so they can avoid volatility)
- **2h**. Number of providers supporting special features - like IP leases, persistent storage, special type of memory, GPUs etc.
- **2i**. How many providers bids are received by tenants on average?
- **2j**. Milestones that the network achieves in terms of blocks created (10M, 100M, 1B etc)

### 3. User Acquisition, Activation, Retention & Monetization Metrics

Leaving out monetization for now.

- **3a**. How many new users (new accounts) did the network see over a specific period of time?
- **3b**. How many users started a deployment but never completed?
- **3c**. How many successfully deployed for the first time?
- **3d**. On average how many times does a user deploy per week, month? (are there tiers within this?)
- **3e**. What clients are users using to deploy on to akash (percentage breakdown)?
- **3f**. How many users (wallets) were connected to akash deployments as a result of a marketing campaign (i.e attribution)?
- **3g**. What is the average amount of spend per lease, so that we can try to characterize the types of users (“kicking the tires” vs “using in production”)?
- **3h**. How many times was a given type of "special feature" requested by tenants deploying on the providers? (ip leases, persistent storage etc)
- **3i**. What was the average size of resource requested (memory, cpu, storage etc)?
- **3j**. What types of workloads are running on the providers? (understand our target user segments. Do they tend to be compute heavy or memory heavy? What type of providers should we get?)

### 4. Community & OSS Metrics

- **4a**. How many contributors did we get to all our Open-Source-Software (OSS) repositories over time?
- **4b**. Contributions by repository
- **4c**. Total issues created, progressed, closed.
- **4d**. Stars, forks, watch count over time
- **4e**. Growth in discord users over time

## Sources of data

The data for these metrics will come from:
- [On-Chain data](onchain-data-model.md)
- [Provider Status & Attributes](../wg-provider-attributes/README.md)
- User engagement data tracked by the various [deployment clients](../sig-clients/README.md)
- [Github stats](https://docs.github.com/en/rest/metrics/statistics?apiVersion=2022-11-28)
- [Discord Server Insights](https://support.discord.com/hc/en-us/articles/360032807371-Server-Insights-FAQ)

## Visualizing the data

Ideally we will want to pull all the metrics into a single interface, so potentially we will store the onchain metrics in bigquery or a time-series DB and then pull other metrics using their API into a common reporting interface like grafana or build our own. To start with, even having each data source reported to a separate interface would be fine.