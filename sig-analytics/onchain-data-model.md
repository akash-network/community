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
| Order       | 1a, 1b                                 |
| Leases      | 1c, 1d                                 |
| Providers   | 2(a-h)                                 |
| Resources   | 3i                                     |
| Tenants     | 2j                                     |


### Tables Details

#### Bids

The *Bids table* stores data pertaining to bids places on an order by providers of Akash Network.

| Field        | Description        | Data Type                | Example               |
| ------------ | ------------------ | ------------------------ | --------------------- |    
| id           | PK                 | int                      | 1                     |
| tenant_id    | FK                 | int                      | 1                     |
| lease_id     | FK                 | int                      | 1                     |
| provider_id  | FK                 | int                      | 1                     |
| amount       | provider bid price | numeric                  | 5                     |
| denomination | uakt or akt        | varchar(50)              | uakt                  |  
| created_at   | data creation time | timestamp with time zone | '2021-08-09 13:57:40' |

#### Blocks

The *Blocks table* stores data on the blocks being created on the Akash Network blockchain

| Field           | Description        | Data Type                | Example               |
| --------------- | ------------------ | ------------------------ | --------------------- |
| id              | PK                 | int                      | 1                     |
| block_height    | height of block    | int                      | 1                     |
| block_timestamp | timestamp of block | timestamp with time zone | '2021-08-09 13:57:40' |
| created_at      | data creation time | timestamp with time zone | '2021-08-09 13:57:40' |

#### Orders

The *Orders table* stores information about [MsgCreateDeployment](https://github.com/akash-network/node/blob/11756fd27c3abd88d6f527250b6bfbc8170028cd/x/deployment/types/v1beta2/deploymentmsg.pb.go#L28)

The difference of volume in orders and leases shows how many people began a deployment, but did not accept a bid.

| Field     | Description | Data Type | Example |
| --------- | ----------- | --------- | ------- |
| id        | PK          | int       | 1       |
| tenant_id | FK          | int       | 1       |
| dseq      |             | int       | 327236  |
| gseq      |             | int       | 1       |
| oseq      |             | int       | 1       |

#### Leases

The *Leases table* maintains a list of all leases on the Akash Network

| Field         | Description                     | Data Type                | Example               |
|  ------------ | ------------------------------- | ------------------------ | --------------------- |
| id            | PK                              | int                      | 1                     |
| tenant_id     | FK                              | int                      | 1                     |
| provider_id   | FK                              | int                      | 1                     |
| dseq          |                                 | int                      | 342743                |
| gseq          |                                 | int                      | 1                     |
| oseq          |                                 | int                      | 1                     |
| start_height  | start height of lease           | int                      | 743829                |
| stop_height   | stop height of lease (NULLABLE) | int                      | 834297                |
| amount        | accepted bid price              | numeric                  | 5                     |
| denomination  | uakt or akt                     | varchar(50)              | uakt                  |
| created_at    | data creation time              | timestamp with time zone | '2021-08-09 13:57:40' |
| updated_at    | time data is updated            | timestamp with time zone | '2021-08-09 13:57:40' |
    

#### Providers

The *Providers table* contains information relating to all providers (active and inactive) and their attributes

| Field            | Description                | Data Type                | Example                                      |
| ---------------- | -------------------------- | ------------------------ | -------------------------------------------- |
| id               | PK                         | int                      | 1                                            |
| prodiver_address | wallet address of provider | varchar(50)              | akash1qvsus5qg8yhre7k2c78xkkw4nvqqgev7gv6gj6 |
| created_at       | data creation time         | timestamp with time zone | '2021-08-09 13:57:40'                        |

#### Resources

The *Resources table* stores information about the resources (compute, memory, storage etc) used by a given lease or requested by a given order.

| Field         | Description                     | Data Type                | Example               |
| ------------- | ------------------------------- | ------------------------ | --------------------- |
| id            | PK                              | int                      | 1                     |
| lease_id      | FK                              | int                      | 1                     |
| units_cpu     | cpu units requested             | numeric                  | 6                     |
| unit_memory   | memory requested (bytes)        | numeric                  | 1000                  |
| units_storage | storage requested (bytes)       | numeric                  | 1000                  |
| created_at    | data creation time              | timestamp with time zone | '2021-08-09 13:57:40' |

#### Tenants

The *Tenants table* stores data pertaining to [tenants](http://eng-docs.akash.pub/overview/akash/) on Akash Network.

| Field          | Description           | Data Type                | Example                                      |
| -------------- | --------------------- | ------------------------ | -------------------------------------------- |
| id             | PK                    | int                      | 1                                            |
| tenant_address | tenant wallet address | varchar(50)              | akash1lxh0u07haj646pt9e0l2l4qc3d8htfx5u55rh8 |
| created_at     | data creation time    | timestamp with time zone | '2021-08-09 13:57:40'                        |
