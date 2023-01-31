# PRD - Content Moderation

## Background & Context

Anyone with a Keplr wallet can deploy workloads on akash and there is currently no information collected about the tenants. This poses a risk to the providers as well as to the reputation of Akash network. 

Content moderation aims to reduce this risk by giving Akash providers the tools necessary to be able to inspect and (if necessary) remove inappropriate content and/or block workloads or tenants from deploying on to their infrastructure.

## Problem Statement

Akash Providers today do not have any first class support to be able to query information about the leases and workloads running on them and they also lack any tools for being able to close running leases or block deployments from specific tenants. Akash Network also does not support KYC/B, so there is no knowledge of who a specific tenant is.

## Roadmap

While the ideal end state is one where Akash Network supports KYC/B and this data is made available to the providers, this will take a considerable effort. So for the immediate term, we intend to offer something less than ideal that will provide some level of visibility and control to the providers:

### Phase-1: Management and Moderation APIs
In the first phase, we will implement a set of "Management APIs" that will let Akash providers gain visibility into the types of workloads and content running on the provider as well as a set of "Moderation APIs" that will allow them to take action, based on the data they get from the "Management APIs"

The Management API will allow the provider to query one or more or all the leases running and be able to see details of the leases, including endpoint URLs and image names. 

The Moderation API will be able to enforce a policy based on a published allow/ deny list of wallets and/ or image names.

  * [Management API](management-api.md)
  * [Moderation API](moderation-api.md)

### Phase-2: Crowdwourced Allow/ Deny & KYC/B
In the second phase, we will consider either a crowdsourced approach to building the allow/ deny lists and/ or implement KYC/ B and make that data available to the providers
