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

### `LeaseStatus`

Request: LeaseStatus API should accept DSEQ/GSEQ/OSEQ
Note: the only provider of that deployment can call this API

Response:

```
{
 uris: [
    .. // array of urls
 ]
 port: '',
// need to find other lease/deployment details
}
```

### `CloseLease`

CloseLease API will accept DSEQ/GSEQ/OSEQ and close the lease/deployment from their provider. Note: Only provider's hosted leases/deployments will be closed.

Request: DSEQ/GSEQ/OSEQ

Response:
```
{
    success: true
}
```