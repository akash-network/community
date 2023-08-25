# AkashJS common features (from Cloudmos Deploy and Akash Console)

One of the key elements of the [Cloudmos-Console cohesive product strategy](https://github.com/akash-network/community/blob/5bc4d0af07dbb4ea955e7ebed19393fabe69891b/product-strategy/cloudmos-console-product-strategy.md) was code reuse, by factoring out common features and functions ("Items") into common code repositories. The common repos we've identified for this are [AkashJS](https://github.com/akash-network/akashjs) and [Akash-API](https://github.com/akash-network/akash-api). To that end, this document lists out which common features will be available via AkashJS and Akash-API and also, which implementation (Cloudmos vs Console) is being adopted. This document will be updated if we identify new areas of commonality and as issues/ PRs get created for the work.

| Item                | Cloudmos              |   Console               |         Action                  | Issue or PR for tracking |
|           ---       |      ---              |    ---                  |          ---                    | --- |
| Manifest            | Uses Akash JS already | Uses AkashJS already    |  None (maintain as-is)          | | 
| protobufs           | Custom implementation | Custom implementation   | Both to update to use akash-api | |
| API                 | Uses AkashJS + ORM    | N/A (no public API)     | Console will decide if we want to use the same ORM or another | |
| SDL                 | Custom implementation | Custom implementation   | Add support in AkashJS and have both clients use it | 
| SDL Validation      | Custom implementation | Custom implementation   | Since Cloudmos' support is more extensive, Cloudmos implementation will be used for both (and ideally refactored out into AkashJS)  | |
| SDL Parameter Editor | Custom components    | Custom components | Likely nothing to do because we're ok with different look and feel |
| RPC request and proxying | Request part used from AkashJS, proxying is custom | Request part used from AkashJS, proxying is custom | proxying code to be implemented in AkashJS| |
| HTTP request and proxying (including comms with providers) | Custom, Currently gets data partly from RPC and and partly from Indexer | Custom | Cloudmos implementation to be ported to AkashJS and used by Console | |
| Wallet creation and handling | Uses Keplr implementation | Uses Keplr implementation | Nothing to port also Console 2.0 likely don't need to expose this to the user | |
| Certificate creation and handling | Uses Keplr implementation | Uses Keplr implementation | Nothing to port also Console 2.0 likely don't need to expose this to the user | |
