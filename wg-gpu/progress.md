# GPU development phases and progress

## API
**State** - InProgress

**NOTE** `proto` definitions will be moved from [node](https://github.com/akash-network/node) to a new API repo during this phase.
Repo link TBD by @troian

### Define v1beta3 blockchain API 
**State** - DONE

1. Define GPU resource unit
2. Extend `ResourceUnits` with GPU resource
3. Extend `ValidateBasic` for DeploymentCreate/Update transaction with validation of GPU resource

### Define v2beta2 Manifest
**State** - InProgress

1. Should be based on [v1beta3 api](#define-v1beta3-blockchain-api) 
2. Extend service with GPU parameters.
GPU workloads are finite living, i.e. when job is done both tenant and provider expect it to be close.
Service may include definition workload behavior.

### SDL
**State** - InProgress

1. Parse and validate GPU resource and it's attributes. If GPU is not present in SDL, units must default to `0`
    ```yaml
    resources:
      gpu:
        # quantity could be a better name for it
        units: 1 # mandatory if gpu is present.
        attributes: # optional
    ```
2. Extend tests with GPU parsing and validation
3. Service/Expose must be made optional as workloads with GPU may not need one
    ```yaml
    params:
      gpu:
        <TBD>
    ```

### Extend service parameters with GPU
**State** - InProgress

1. Should be based on [v2beta2 manifest](#define-v2beta2-manifest)


### Define provider attributes for the GPU resource
**State** - Discussion

## Provider
**State** - InProgress

### Node labels
**State** - DONE

Each node supplying GPU should be labeled with `akash.network/gpu: true` in order to be included in inventory.

### CRDs
**State** - DONE

Define `v2beta1` CRD based on [v2beta2 manifest](#define-v2beta2-manifest)

### Inventory service
**State** - DONE

Track counts of custom resource `nvidia.com/gpu` labeled with [gpu](#node-labels)

### Bidengine
**State** - [Blocked](#define-provider-attributes-for-the-gpu-resource)

### Development environment
**State** - DONE

Extend `_run` examples with `ssh` run configuration to allow configuring remove cluster with GPU resources

### Documentation
**State** - InProgress

