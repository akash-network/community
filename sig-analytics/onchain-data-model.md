# [WIP] Data Model for on Chain Data (Akash Network) Analysis

The goal of this document is to summarizes data requirements for on-chain data, pulled from the Akash Network blockchain, to help answer many of the questions called out in the [PRD](prd.md). There is no specific reference to data store here, as that will be an implementation decision.

This is a work-in-progress [WIP] that will be fleshed out more as we think through the schema.

## Tables 

### Tables Summary

The following tables have been identified at this time and connected to the [specific metrics](prd.md) they will provide data for. The next section goes into the structure (schema) of these tables.

| Table Name  | Metrics Provided ( ref: [prd](prd.md) )|
|   --        |       --                               |
| Bids        | 2i                                     |
| Blocks      | 2j                                     |
| Deployments | 1a, 1b                                 |
| Leases      | 1c, 1d                                 |
| Orders      | 3(a-d)                                 |
| Providers   | 2(a-h)                                 |
| Resources   | 3i                                     |
| Transactions| 2j                                     |


### Tables Details

#### Bids

The *Bids table* stores data pertaining to bids places on an order by providers of Akash Network.

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |


#### Blocks

The *Blocks table* stores data on the blocks being created on the Akash Network blockchain

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |

#### Deployments

The *Deployments table* stores information about deployments started and closed by tenants

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |

#### Leases

The *Leases table* maintains a list of all leases active on the Akash Network

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |

#### Orders

The *Orders table* contains data on all orders placed on the Akash Network

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |

#### Providers

The *Providers table* contains information relating to all providers (active and inactive) and their attributes

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |

#### Resources

The *Resources* table stores information about the resources (compute, memory, storage etc) used by a given lease.

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |

#### Transactions

The Bids table stores data pertaining to bids places on an order by providers of Akash Network.

| Field | Description | Data Type | Example |
|  --   |     --      |     --    |   --    |
