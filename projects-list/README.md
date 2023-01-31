---
title: "Current Projects"
date: 2023-1-09T00:19:20-08:00
weight: 20
---

# Akash Network Projects

These are all the projects that are currently in some state ranging from "ideation" to "release". To understand the various states see the table at the bottom of this page.

**General guidelines for updating this table**

- Projects that are in some working state (ideation or beyond) should have a link to their specific sig or wg page (can even just be a github issue inside the repo for the sig) from the "Project Name"
- Projects that are in a working state should have a label specified here and linked to a filtered list of github issues for that label
- Projects that are in a working state should be assigned to a SIG or WG
- Projects that are not even in ideation (not in a working state) should have a name and a brief description

| Project Name | Label | Description | Community Group | State
| --- | --- | --- | --- | --- |
| Provider Services Microservices Refactor | provider-svc-split | Splitting Akash Provider Services into microservices so that we’re able to release and maintain software better | [sig-providers](..//sig-providers) | implementation |
| Certification Program | edu-cert-prgm | Define, build and finalize Akash Network Certification Program  | [sig-community](https://github.com/akash-network/community/tree/main/sig-community) | implementation |
| Console General Availability | console-ga | Releasing Console for General Availability | [sig-clients](https://github.com/akash-network/community/tree/main/sig-clients) | implementation |
| Docs site migration | docs-site-migration | Migrating the documentation site from gitbooks to something automatable (Hugo?) | [sig-docs](https://github.com/akash-network/community/tree/main/sig-documentation) | spec-definition |
| [Console Authorized Spend Support](../sig-clients/akash-console/prd-authorized-spend.md) | console-authz | Supporting Authorized Spend (AuthZ) in Akash Console | [sig-clients](https://github.com/akash-network/community/tree/main/sig-clients) | spec-definition |
| [Client Libraries](https://github.com/akash-network/community/blob/main/sig-clients/client-libraries/prd.md) | client-libs |  Libraries for deploying on Akash programmatically using various programming languages  | [sig-clients](https://github.com/akash-network/community/tree/main/sig-clients) | spec-definition |
| GPU Support | gpu | Everything related to supporting, launching and growing GPUs on Akash  | [wg-gpu](../wg-gpu) | spec-definition |
| Provider Attributes | provider-attr | Defining an attribute schema for providers and getting providers to incorporate it  | [wg-provider-attributes](../wg-provider-attributes/README.md) | spec-definition |
| Economics 2.0 | econ-2.0 | Redesigning Akash Network's economics model to have fine grained take rates to fund product development and sustainability of the chain  | [sig-economics](https://github.com/akash-network/community/tree/main/sig-economics) | spec-definition |
| Omnibus Maintenance | omnibus-maint | Building new reference SDLs and packages for new chains that we want to support. Building automated testing for the supported omnibus chains  | [sig-community](https://github.com/akash-network/community/tree/main/sig-community) | ideation |
| Content Moderation | content-mod | Tools and process for ensuring that providers have visibility into workloads running on them and controls to ensure they don’t violate their terms of service  | [sig-providers](../sig-providers) | ideation |
| Keeping up with Cosmos | cosmos-sync | Things we Akash needs to do to stay in sync with Cosmos (SDK changes etc)  | sig-network-upgrade  |  |
| Private Image Repository |  | Support for deploying  images hosted in private container registries |  |  |
| CI/ CD Workflows |  | Things necessary to support CI/ CD style deployments on Akash  | |  |
| Provider Attribute Auditing |  | Tooling for auditing provider attributes (like memory, CPU, bandwidth, storage and others) through automated testing before a provider is “officially signed” |  |  |
| Provider Monitoring |  | Hooks for being able to pull infrastructure metrics into tools like Prometheus and Grafana for monitoring and logging |  |  |
| Provider Analytics | | Analytics for providers to understand their profitability and ROI |  |  |
| Provider Onboarding | | Making onboarding of providers as self-service as possible so that we can scale the number of providers on the network into the 100s |  |  |
| Provider Pricing & Profitability | | Tools for providers to set pricing and calculate profitability before they decide to become an Akash provider |  |  |
| Stable payments & Settlement | | Ability for tenants to pay for deployments using other cryptocurrencies |  |  |
| Pricing Stability | |  Ensuring that the cost of deployments remains the same, even as the cost of the currency fluctuates up and down |  |  |
| Cloud Parity Foundational Features | | Cross Provider Deployments for High Availability (HA). Load balancers. State Management
  |  |  |
| Cloud Parity Reference Applications | |  Building reference applications that mirror the way apps are built in public clouds |  |  |
| StorJ Integration | | Spec and implement what's needed for users to use StorJ for persistent storage (like S3 or Akash persistent storage) |  |  |
| Log Retention for Tenants | | Support retaining tenant deployment logs for longer durations to allow better debugging |  |  |
| JWT Authentication | | Authentication using Java Web Tokens |  |  |
| Container Image Updater | | Ability to have a new version of a container image be redeployed when the registry image is updated |  |  |
| Event Planning 2023 | | Define purpose, lineups, and attendees (and weight of OCL presence) for events that Akash Network would attend |  |  |
| Reference Provider Setup | | Build & Operate a reference provider(s) for Akash Network in a colocation facility. |  |  |
| On-Chain Analytics | | Build data pipeline and analysis tool for onchain analytics  |  |  |

## Project States

A project may be in one of these states. Note that every project does NOT have to touch every one of these states and some projects may remain in a given state for a long time (like an idea that never gets any interest from the community to implement and remains in "ideation" for a long time).

| State | Description | Things needed |
| --- | --- | --- |
| ideation | A rough idea for a project has been proposed |
| spec-definition | Specification (typically a PRD or a ligher version of it in a github issue) is being worked on by a SIG or WIG and is in review |
| spec-approved | The specification for the project has been approved and it has been allocated to specific SIG(s) | |
| design | Technical Design is being worked on (typically by SIG(s) )
| implementation | Actual work to bring the thing to life is happening (code being written, event being organized, docs site being updated) | |
| beta | The project is in beta test phase (where/ when applicable) - typically for products/ features | |
| release | The product/ feature has been released to everyone (general availability) | |
| blocked | The project is blocked or stalled because of some reason (documented) | |
| abandoned | The project has been cancelled because no one is willing to shepherd it | |
