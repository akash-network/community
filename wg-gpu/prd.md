---
title: "PRD - GPU Marketplace on Akash"
date: 2023-1-27T00:21:46-08:00
---

# [WIP] PRD - GPU Marketplace on Akash Network

Product requirements to allow Akash Network tenants to lease GPU capacity for their deployments and for providers to offer GPU resources through the marketplace. This is a work in progress (WIP)

## Background & Context

Choosing GPU support as the next thing to focus on is primarily driven by 3 strategic goals:

- Growing the size of our addressable market for tenants by enabling new applications to be deployed on Akash, that have higher resource requirements. Examples include machine learning & AI workloads, video & image processing apps as well as crypto mining. The GPU-as-a-Service market is estimated to be \$2B in 2021 and is expected to grow to \$15B by 2030 according to GMI research and the GPU market as a whole is expected to grow by 10x from about \$25B in 2020 to \$245B by 2028 according to [statista](https://www.statista.com/statistics/1166028/gpu-market-size-worldwide/0).

- Becoming an attractive alternative for Proof-of-Work (PoW) miners to monetize the CapEx cost they have already incurred, now that Ethereum has transitioned to Proof-of-Stake (PoS) based consensus, by becoming Akash providers.

- Aligning with our future strategy to become the platform of choice for all types of High Performance Computing (HPC) workloads.


In addition to the above strategic goals, Akash Network and its community have seen a tremendous amount of organic demand from its users for GPUs.


## Problem Statement
In order for Akash to offer support for GPUs on its marketplace, the following questions need to be answered (decisions need to be made):

### Provider specific questions/ decisions:

1. What will the provider set up look like?

2. Do we need to limit to just NVIDIA GPUs to start with or can we be neutral (can support Intel, AMD, Xilinx FPGAs, Google TPUs etc?)

3. Will we limit to certain types (models) of GPUs to start with?

4. What attributes of the GPU can/ will we expose?

5. How will they be priced?

6. What are the limitations of scheduling GPUs via Kubernetes and how does this impact our ability to offer a great user experience?

7. Do we need to worry about figuring out bandwidth pricing before we offer GPU support?

8. Others?

### Tenant specific questions/ decisions:

1. How will tenants request GPU resources? Will we use similar stanzas as our current SDL or different ones (kubernetes base ones)?

2. Should we worry about supporting private container registries for container images before we offer GPU support?

3. Tenants (developers) we polled have asked for CUDA and PYtorch support, is there anything special we have to do to ensure this is available?

4. What other features would we need to support before tenants will use GPUs for running their workloads

5. Others?



## User Personas

There are four main user personas that we have to pay attention to, when working on adding support for GPUs - two provider personas and two tenant personas

### Provider User Personas

#### Proof-of-Work Miners 
While our primary intention is not to support compute intensive mining on our GPUs, our strategy is to demonstrate to (former) PoW miners that they can be more profitable by becoming Akash providers. Ideally, the way we do this is by making it easy for them to become an Akash provider (without having to give up mining) first, then compare the profitability of being a provider for general applications vs. mining rewards.

Existing crypto miners would see value in becoming Akash providers if they’re able to utilize the hardware and software they already have to drive additional revenue. This additional revenue will come from offering infrastructure to both, crypto mining users (tenants) as well as non-crypto (AI/ ML/ image processing…) users. 

The key to attracting these users is to make the transition as easy as possible. While more user research and validation is pending, one likely requirement is to work with the software environment they already have running on their infrastructure. Most professional miners run mining-optimized Linux variants. Some of the popular “Mining-OSes” are: [HiveOS](https://hiveon.com/), [Simple Mining OS](https://simplemining.net/), [ethOS](http://ethosdistro.com/), [RaveOS](https://raveos.com/) & [MinerOS](https://mineros.info/). Ideally we would want to ensure that our provider is capable of running on these OSes or provide an easy path for the miners to migrae to our provider software.

#### Traditional Providers

These are data center providers that are NOT interested in crypto but have GPU capacity available that they would like to lease out. These users would be fine with installing any version of software we ask them to install, in order to become an Akash provider.

### Tenant User Personas 

#### ML & AI Users

There are mutiple subsegments when it comes to users building ML & AI applications

1. **Users training their own AI models**: These users will typically require very high performance GPUs that will be hard to source and typically they are part of large enough organizations (like OpenAI or Tesla or Google) and are unlikely to use Akash GPUs for training. This is NOT a user segment we want to target (at least initially).
2. **Users tuning an existing (trained) AI model**: This *may* be a user segment we can target, depending on what the GPU types they need.
3. **Users runing inference using a previously trained AI model**: This is going to be our primary user segment since the resource requirements for inference are going to be relatively low.

The key to building a solution that works for the above users, is adding inventory for the most commmonly used GPUs (as new an NVIDIA GPU as possible, ideally A100s) and supporting the necessary toolkits & libraries (like CUDA).


#### Crypto Mining Users
We don't intend to actively pursue this segment of users or optimize workflows for them but will not prevent from them from using our GPUs, if they choose to.

The segment of users interested in mining cryptocurrencies on Proof-of-Work (PoW) blockchains that require GPUs for computation. Our hope is that eventually this will represent a diminishing set of users on our platform, but in order for us to incentivize crypto miners to move their GPU resources to Akash, we have to show them that we have made it easy for their target users to deploy through Akash. We need to ensure that there are SDL templates built for the most common chains and these templates are built into the deployment tool (Console, Cloudmos etc) as well. 

## Product Requirements

### Tenant Requirements

- Tenants should be able to request GPU resources via SDLs. 
  
- The GPUs would be requested as part of the resources declaration (similar to CPU, memory and storage).

- GPU resources should be requestable alongside CPU resources. For example, a single deployment could include multiple services, some of which should be scheduled on CPUs while others on GPUs.

- They should ideally be able to specify attributes they would like on the GPUs they are requesting and have providers that meet them bid on the request. There are some generic/ common attributes and some vendor specific ones:
  - Generic/ common attributes
    - Vendor Name (e.g nvidia, amd)
    - Specific Model Name (e.g tesla-k80, tesla-v100)
    - VRAM (?)
    - Number of units
  - Vendor Specific Attributes
    - Nvidia: TBD
    - AMD: TBD
- Tenants should be prevented from being able to request fractional units of a GPU resource (see k8s limitations section above for why)

### Tenant Deployment SDL

- **To-Do**: Define SDL for tenant deployments (after we have figured out provider attributes spec)

### Provider Requirements
- **Installation**
  - Needs to be installable via the [Akash/ Helm way](https://docs.akash.network/providers/build-a-cloud-provider/akash-cloud-provider-build-with-helm-charts).
  - Need to be installable via the [Praetor way](https://praetorapp.com/).
  - **To-Do**: Research if the [Nvidia GPU Operator](https://github.com/NVIDIA/gpu-operator) can be leveraged for this.

- **Configuration**
  - Must include instructions for configuring attributes using k8s Node Labels and Selectors (detailed in the next section of this document).
- **Provider Attributes**
  - These will be documented in the provider attributes spec that [community/wg-provider-attributes](../wg-provider-attributes/README.md) us working on.

### Private Container Registry Support

Today Akash does not support deplpoying container images that are stored in provate registries (they need to be publicly accessible). If our primary user segment is ML & AI application developers then this is likely a requirement that we need to satisfy. This effort will be handled by a separate community work group (WG).

### Bandwidth Pricing

ML & AI applications generally require a large data set transfer which seems to indicate the need to support bandwidth pricing in Akash providers. That said, based on a survey of several DC operators, it seems like most of them offer unmetered bandwidth (unlike AWS), so the thinking is that this is not likely to be a blocker for adoption.

## Go-To-Market (GTM) Plan
The GTM plan for GPUs will need to include:
1. Partnerships with DC operators for GPU inventory
2. Enagement with the PoW miner community for testing on mining OSes and sourcing GPU inventory
3. Partnershup with developer tool companies that make it easy to create a dev environment on GPU hardware (e.g https://brev.dev/)
4. Parnerships with application developers to understand developer experience and drive adoption

## Execution Phases

This is a starting poing that needs to be fleshed more:

1. Verify that we can deploy a workload to a "plan vanilla" k8s cluster containing GPU instances
2. Complete the provider attribute spec (wg-provider-attributes) and include GPU attributes in it
3. Define SDL (once provider attributes are known)
4. Modify provider and SDL code to accommodate GPU attributes
5. Test SDL deployment to a Akash provider running the new (GPU capable) provider software
6. Open up to beta testers (including minin OS users)
7. Work on private container registry support (wg-private-containers)


## Kubernetes (and GPU vendor specific) Context

This is additional research that is helpful to undertstand how we came up with the approach outlined in the initial part of this document

Since our providers are essentially Kubernetes clusters and tenant workloads are Kubernetes deployments, it is important to understand the current state of GPU support in Kubernetes and its limitations, because we will essentially be inheriting those limitations in our GPU solution.

Supporting GPUs in k8s is a challenge because:
- GPUs require vendor specific drivers to be installed, before applications can interact with them

- GPU applications utilize libraries from the vendor (the kind that come with the NVIDIA CUDA toolkit for example) - which need to be installed before an application container can run.
- The drivers, libraries and kernel modules need to be compatible (typically be the same version) for things to work.
- Kubernetes principles require that the containers be portable, so the user cannot bundle the drivers and/ or the libraries as part of the container.

### Kubernetes Limitations

- Kubernetes support for scheduling GPUs is currently in BETA with v1.10: https://kubernetes.io/docs/tasks/manage-gpus/scheduling-gpus/

- It only has support for NVIDIA and AMD at this time (so, for example, we cannot 

- It requires that the administrator install GPU drivers from the corresponding vendor. 

- Containers (and Pods) cannot share GPUs so a provider cannot overcommit GPUs - only one container per GPU.

- A container cannot request a fraction of a GPU - it is all or nothing. This is particularly important to note because in case of Akash, a provider’s resources are “held up” while a lease is pending. In case of GPUs, this would be the whole GPU.
  - TBD: Can a provider submit multiple bids but not honor the lease once it has accepted a lease elsewhere? Can potentially overcome this limitation by polling and updating the frontend.


### Current Kubernetes Implementation

K8s resolves the conflict between trying to be vendor neutral and keeping containers portable, while offering users the ability to request and configure vendor specific settings, through the use of ***Device Plugins*** and ***Node Selectors***.


#### Device Plugins

The way that k8s handles the driver and library issues is through the use of Device Plugins which need to be configured by the administrator (provider in the Akash context). The device plugin sends the device’s capabilities to the kubelet, which advertises it to the API server, during its status updates. This allows the user to then be able to request devices as part of the pod spec as follows:

```

---

apiVersion: v1

kind: Pod

metadata:

 name: demo-pod

spec:

 containers:

   - name: demo-container-1

     image: k8s.gcr.io/pause:2.0

     resources:

       limits:

         hardware-vendor.example/foo: 2

#

# This Pod needs 2 of the hardware-vendor.example/foo devices

# and can only schedule onto a Node that's able to satisfy

# that need.

#

# If the Node has more than 2 of those devices available, the

# remainder would be available for other Pods to use.

```

In the above spec:

**hardware-vendor.example/foo** may be nvidia.com/gpu or amd.com/gpu


#### Node Labels and Selectors

If a k8s cluster has nodes with a mix of GPU vendors (some AMD, some NVIDIA), the kubernetes admin can use Node Labels and Node Selectors to expose those attributes to the user.

```
# Label your nodes with the accelerator type they have.


kubectl label nodes <node-with-k80> accelerator=nvidia-tesla-k80


kubectl label nodes <node-with-p100> accelerator=nvidia-tesla-p100
```

#### Tested Kubernetes deployment with GPUs

An overclock labs dev (Avi) tested and documented a sample k8s deployment, including requests and limits for CPU and GPU. The GPU part, which is new is highlighted below

```
spec:
  containers:
  - name: app
    image: images.my-company.example/app:v4
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
        nvidia.com/gpu: 2  # ←—- GPU addition
```

The above deployment spec requests 2 NVIDIA GPUs. Note that it does not specify what class or type of GPU is requested. The type selection may be done using a nodeSelector as shown below (this spec requests 2 NVIDIA GPUs of type "Tesla K80")

```
spec:
  containers:
  - name: app
    image: images.my-company.example/app:v4
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
        nvidia.com/gpu: 2  # ←—- GPU addition
    nodeSelector:
      accelerator: nvidia-tesla-k80  # ←—- GPU addition
```
### Available Vendor & Ecosystem Tools

#### AMD

AMD has a [Device Plugin](https://github.com/RadeonOpenCompute/k8s-device-plugin) for Kubernetes and also has a [Node Labeller](https://github.com/RadeonOpenCompute/k8s-device-plugin/tree/master/cmd/k8s-node-labeller) Kubernetes controller that automatically labels nodes in a cluster with device properties for their GPU devices.

#### NVIDIA

There are two device plugin implementations available for NVIDIA:
1. The [NVIDIA official device plugin](https://github.com/NVIDIA/k8s-device-plugin): 
   - Requires that the nodes be preinstalled with NVIDIA drivers
   - Only works with the nvidia-docker runtime 
2. The [Google Cloud NVIDIA device plugin](https://github.com/GoogleCloudPlatform/container-engine-accelerators/tree/master/cmd/nvidia_gpu): 
   - Installs NVIDIA drivers as a daemonset
   - Can work with any container runtime that is compatible with Kubernetes Container Runtime Interface (CRI)

In addition to the device plugins, NVIDIA has also built a [Kubernetes Operator for GPUs](https://github.com/NVIDIA/gpu-operator)

Nvidia has also introduced Multi-Instance-GPUs (MIGs) that allow partitioning of GPUs into up to 7 instances that can run parallel processes with isolated memory & compute resources - which could overcome the limitation that a single GPU can only run one container. See this blog for details: http://www.pattersonconsultingtn.com/blog/introduction_to_nvidia_mig.html

#### MicroVMs (Kontain et al)
Micro-VMs (such as those offered by [Kontain](https://kontain.app/) ) could be an alternative option for overcoming the challenges of running containers while ensuring the GPU dependencies are taken care of. For now we do not think we need to pursue this part given the native support in k8s for containers but worth keeping in mind.
