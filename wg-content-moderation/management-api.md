# Akash Network: Provider Management API

Provider tooling support

* introspection (lease status)
* administration (close lease)

## Overview

Provider management APIs will provide additional control on running leases on their provider. For example, the provider will able to see what kind of workloads are running into their provider and will able to close lease/deployment if found inappropriate.

## Use-Cases

* find the URL of the deployments running on their provider
* find the port number of the deployments if running other than 80/443 port.
* close lease/deployment if find inappropriate content

## Specification

### Lease list (Return array of leases hosted in provider)
#### `/api/v1/provider/lease/list (Lease List)`
Return list of lease hosted in the provider

Note: We may need pagination here
Return fields
|Field|Description|
|---|---|
|`dseq`| DSEQ |
|`gseq`|GSEQ|
|`oseq`|oseq|
|`image_name`|image name for deniel request|
|`escrow_account.balance` | Escrow account balance|
|`escrow_account.transferred` | Escrow account transferred|
|`escrow_account.settled_at` | Escrow account settled at block number|
|`lease.created_at` | Deployment created at block number|
|`lease.state` | Deployment current state |
|`lease.urls` | If deployed on port 80 return urls |
|`lease.ports` | If deployed on port other than 80 or 443, return host and provider ports |
|`lease.owner` | Lease owner wallet address |
|`lease.amount` | Lease price per block |

Response will contain `array` of leases of above reponse fields


### Lease status
#### `/api/v1/provider/lease/status/?dseq=&gseq= (Lease Status)`
Find perticular lease status

Return fields
|Field|Description|
|---|---|
|`dseq`| DSEQ |
|`gseq`|GSEQ|
|`oseq`|oseq|
|`image_name`|image name for deniel request|
|`escrow_account.balance` | Escrow account balance|
|`escrow_account.transferred` | Escrow account transferred|
|`escrow_account.settled_at` | Escrow account settled at block number|
|`deployment.created_at` | Deployment created at block number|
|`deployment.state` | Deployment current state |
|`deployment.urls` | if deployed on port 80 return urls |
|`deployment.ports` | if deployed on port other than 80 or 443, return host and provider ports |
|`owner` | lease owner wallet address |
|`lease.amount` | Lease price per block |

Response will contain above reponse fields for lease

### Close Lease
#### `/api/v1/provider/lease/close/?dseq=&gseq= (Lease List)`
This API will close lease on request of provider and settle AKTs.