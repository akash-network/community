# Akash Network: Provider Moderation API

Akash Providers currently have limited methods of controlling
which workloads they host.  As discussed in [PRD](prd.md),
a more powerful toolset for modering hosted workloads will
make becoming an Akash provider much more attractive.

This document proposes a provider service that is
responsible for deciding whether or not a given
workload should be allowed to run.  It contains
methods for configuring workload filters
and an API for other components to query
whether or not a workload is acceptable.

## Overview

The Moderation Service is a standalone server with a minimal interface.
It is meant to run alongside and be used by other provider services.

### Configuration

Configuration is persisted as a Kubernetes CRD, and can be edited
directly.

Configuration consists of lists of filters.  Each filter has a `Priority` field
that controls the filter evaluation order.  The lists are "default allow";
if a list is empty then the workload will be allowed.

### Order Filters

These filters are able to be evaluated before a bid is created.

#### `TenantAddress`

Filters orders by tenant address.

|Field|Description|
|---|---|
|`Priority`| Filter Priority. |
|`Address`|Address to evaluate.  `""` matches all addresses.|
|`Allow`|Whether or not the given address is acceptable.|

### Manifest Filters

#### `Hostname`

Filters orders by manifest Hostname.

|Field|Description|
|---|---|
|`Priority`| Filter Priority.|
|`Pattern`|Regex pattern to match a hostname.|
|`Allow`|Whether or not the given hostname is acceptable.|

#### `Image`

Filters orders by manifest Hostname.

|Field|Description|
|---|---|
|`Priority`| Filter Priority.|
|`Pattern`|Regex pattern to match a Docker image name.|
|`Allow`|Whether or not the given image is acceptable.|

### Configuration API

#### `FilterList()`

Return current filters in a paginated response.

#### `FilterAdd(Filter)`

Adds the given filter to the ruleset.

#### `FilterRemove(Filter)`

Removes the given filter from the ruleset.

### Filter API

#### `AcceptOrder(Order)`

`AcceptOrder()` can be called by the Bid Service before
placing a bid. It returns `true` if the given order passes all filters,
otherwise returns `false`.

#### `AcceptManifest(Lease,Manifest)`

`AcceptManifest()` can be called by the Manifest Service before
placing executing a workload. It returns `true` if the given manifest passes all filters,
otherwise returns `false`.
