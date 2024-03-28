# PraetorApp (Akash Provider Console) Product Strategy
Note: some of the initiatives outlined are contingent on Praetor joining the Akash Core Team (for which there is a proposal submitted in the discussion board)

The Overclock and Praetor teams have been working closely to align on a product strategy and roadmap and it should come as no surprise to anyone that the focus going forward, is going to be around two broad areas:

- Making PraetorApp part of a cohesive product experience that includes Console.Akash.Network (Akash Network’s primary deployment console). This includes rebranding and potentially integrating it better with Akash Console, to serve as a complimentary “Akash Provider Console”. It also includes open sourcing PraetorApp to align with Akash Network’s open source strategy.

- Building solutions to problems around onboarding, monitoring, updating/ upgrading and troubleshooting Akash providers of all sizes (1 node to 1000s of nodes). Specifically, the problems that the two teams will solve are ones that have been surfaced by the Praetor team and Akash community while onboarding hundreds of providers onto the network overall the last couple years. The next section summarizes these problems, and organizes them by themes that will lead to a feature roadmap.


## Key Problems and areas of work

### Telemetry 
Akash providers currently do not have enough visibility into software issues as well as resource issues happening in the underlying infrastructure - in many cases, providers cobble together solutions themselves. To this end, there is critical need to provide first class telemetry in terms of: 
 - Logging
 - Monitoring
 - Error Reporting
 - Provider config stats
 - Automated Testing (Liveliness Probing) by running small deployments continuously and reporting back success/ failure.
 - Grafana dashboard for visualizing all that data

### Kubernetes Cluster Management
Providing better tooling to allow providers to maintain their Kubernetes cluster and software packages installed on it
- Akash providers rely on Kubernetes underneath and must often make changes to that configuration. For example a provider may start as a single node (as they are “testing the waters” on Akash) and then (as demand increases) decide to add on more nodes. PraetorApp today isn’t able to accommodate easily transitioning from running a single node (that may have been set up using K3s) to multiple nodes (running full fledged K8s). Ability to scale number of nodes as the provider grows is crucial.
- Providers need to upgrade to new Kubernetes releases from time to time
- Providers may need to apply specific software packages like CUDA and upgrade those as new versions are released

### Provider specific RPC Nodes
Akash providers rely on RPC nodes (for bidding and communicating with tenants) and oftentimes the RPC nodes can be unreliable. While our documentation requires that providers setup their own RPC nodes, not all providers do that today. Making it easy for providers to install an RPC node during provider set up would alleviate this issue.

### Easier Provider Updates/ upgrades
Making it easy for providers managed by Praetor to check and update to the correct Helm Charts, particularly if there are multiple Helm Chart versions released per provider service release.

### Storage Setup and Configuration
Providers often have ephemeral (rootfs) storage setup with no redundancy (sometimes even with multiple disks - they don’t set them up to replicate data). Not having redundancy in ephemeral storage poses a risk because a disk failure can cause the deployments to be lost if there isn’t room to redeploy to another node. Making this easy to do (as a RAID1) as part of the provider setup, makes providers more reliable.
While PraetorApp supports setting up persistent storage at provider set up time, it does not support being able to add persistent storage after the provider has been set up (and did not include persistent storage to begin with).

### Notifications
Providers have a need to notify and be notified about things. Broadly this is in 3 ways:
- Notify tenants (who have subscribed to them) about any issues
- Get notified about network upgrades and provider releases
- Notify tenants about provider resource reclamation - this is specifically for cases where a provider is bringing on resources that they have a long-term contract on in some centralized public cloud and therefore can only offer the resources “part-time”

### Content Moderation
As Akash Network grows demand and reaches Web2 customers, there is a growing need to enable providers with tools to be able to moderate the type of content they host and prevent content that is harmful to their reputation or could harm them legally. The Praetor team has already been working with the Overclock Labs team on such tools and will continue this work.

### Open APIs
Praetor has and will continue to build a store of key provider data that may be useful for other deployment clients or customers/ partners integrating with Akash Network. Making this data available through Open APIs will enable Akash Network to grow faster.

### Documentation
Documenting various technical things related to setting up and managing a provider is crucial to growing the number of providers on the network. This will include:
- Video examples for set up
- Better documentation on SSH
- Documenting how to setup and configure port forwarding
- Documenting the common DNS pitfalls and how to fix them
- And more

### Provider revenue and profitability data
A stretch goal for PraetorApp (and there are other ecosystem projects that have tackled this problem that we will aim to integrate with) but as demand on the network grows, giving individual providers tools to understand how much revenue they have generated over time, visualizing trends and relating that to their costs will go a long way in helping providers realize the value of choosing to provide compute resources on Akash Network.
