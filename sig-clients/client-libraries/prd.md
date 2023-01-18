# **Requirements Specification**

## **Version 1.1**

## October 25, 2022

Requirements for Akash Network Client Libraries

# Executive Summary

## Project Overview

Client libraries allow developers to interact with remote services through a defined interface using their preferred
programming languages. They can also help abstract the complexity associated with communication protocols used by those
remote services. Client libraries work as enablers for developers to build on existing systems while maintaining a
common interface across clients.

For Akash, having client libraries would make building in the ecosystem more accessible and simple. By providing the
same interface across implementations developers wouldn’t need to relearn concepts to interact with the network while
still being able to develop in different programming languages.

## Purpose and Scope of this Specification

Requirements specification for Akash Network Client Libraries:

### In scope

This document addresses requirements related to Akash Network Client Libraries:

* Create deployments
* Update deployments
* Close deployments
* List/read deployments
* List bids
* Create leases
* Send manifest

These requirements are for each of these supported programming languages:

* Javascript
* Go
* Python
* Java
* C#

### Out of Scope

All the other programming languages

## Product/Service Description

Client libraries for the Akash Network will enable developers to build on top of Akash with their favorite developer
programming stacks, including but not limited to;

* Javascript
* Go
* Python
* Java
* C#

### Product Context

The client libraries will be used by developers to build new tools that integrate with the Akash Network.

## User Characteristics

General customer profiles for each type of user who will be using the libraries are:

* Developer - Develop systems and applications using the client libraries

## Assumptions

Operating systems agnostic, this assumes the developer has access to the Internet.

It is also assumed the developer has access to a valid and funded wallet for development.

## Dependencies

* A working Akash wallet with AKT
* The dependencies related to the specific programming language to be used.

# Requirements

## Functional Requirements

The following table is a tabulation for the requirements.

|Req#|Requirement|Comments|Priority|Date Rvwd|SME Reviewed / Approved|
|----|-----------|--------|--------|---------|-----------------------|
|R_01|Create deployment|Create a deployment based on an SDL file. Request through RPC.|1|||
|R_02|Close deployment|Close a deployment. Request through RPC|1|||
|R_03|List deployments|List all deployments matching the filters with consideration for page limits. Request through REST.|1|||
|R_04|Get deployment|Request through REST.|1|||
|R_05|List bids|Get the list of bids based on a set of filters. Request through REST.|1|||
|R_06|Create lease|Request through RPC.|1|||
|R_07|Get lease|Get information regarding a lease such as its status. Request through REST.|1|||
|R_08|Send manifest|Request through RPC.|1|||
|R_09|Update deployment|Update a deployment based on an SDL file. Request through RPC.|1|||

Extending requirements for Akash Network Client Libraries.
Requirements stated bellow is an addendum to version 1.0.

## Resilience and error handling

### Error Types
Cosmos SDK defines a set of errors that can happen when calling endpoints.
Those "errors" can be treated as exceptional behaviours, or part of the normal flow of invocation, 
where an action/operation can both result in success or failure.

The decision over using or not exceptions as control flow should be done by each client implementors,
since each language can be biased towards one or the other.
The following list aims to be a spec for both. 

Error/Exception/ErrorResult should be prepended according the chosen approach. 

1. AkashNetwork*Error*
Internal errors of akash network itself. They might be eligible for retries.
2. Auth*Error*
Provided authorization/authentication is not valid for the desired action. This kind of error should not be retried.
3. BadRequest*Error* 
Send data is invalid/illegal. This kind of error should not be retried.
4. State*Error*
Current state doesn't allow the operation. This kind of error should not be retried.


### Error model

From the current akash SDK, those are the expected errors:

|Error|Code|Description|Should Retry|Mapped to|
|-----|----|-----------|------------|---------|
|errInternal|1|Internal - not supposed to happen|Yes|AkashNetworkError|
|ErrTxDecode|2|tx parse error|Yes|AkashNetworkError|
|ErrInvalidSequence|3|invalid sequence|Yes|?? what is a sequence ??|
|ErrUnauthorized|4|unauthorized|No|AuthError|
|ErrInsufficientFunds|5|Not enough funds|No|StateError|
|ErrUnknownRequest|6|unkown request|No|BadRequest|
|RootCodespace|7|invalid address|No|BadRequest|
|ErrInvalidPubKey|8|invalid pubkey|No|BadRequest|
|ErrUnknownAddress|9|unknown address|No|BadRequest|
|ErrInvalidCoins|10|invalid coins|No|BadRequest|
|ErrOutOfGas|11|out of gas|No|StateError|
|ErrMemoTooLarge|12|memo too large|No|BadRequest|
|ErrInsufficientFee|13|insufficient fee|No|StateError|
|ErrTooManySignatures|14|maximum number of signatures exceeded|No|??|
|ErrNoSignatures|15|no signatures supplied|No|BadRequest|
|ErrJSONMarshal|16|failed to marshal JSON bytes|No|BadRequest|
|ErrJSONUnmarshal|17|failed to unmarshal JSON bytes|No|BadRequest|
|ErrInvalidRequest|18|invalid request|No|BadRequest|
|ErrTxInMempoolCache|19|tx already in mempool|No|BadRequest|
|ErrMempoolIsFull|20|mempool is full|Yes ??|AkashNetworkError ??|
|ErrTxTooLarge|21|tx too large|No|BadRequest|
|ErrKeyNotFound|22|key not found|No|BadRequest|
|ErrWrongPassword|23|invalid account password|No|AuthError|
|ErrorInvalidSigner|24|tx intended signer does not match the given signer|No|BadRequest|
|ErrorInvalidGasAdjustment|25|invalid gas adjustment|No|StateError|
|ErrInvalidHeight|26|--|No|BadRequest ??|
|ErrInvalidVersion|27|invalid version|No|BadRequest|
|ErrInvalidChainID|28|invalid chain-id|No|BadRequest|
|ErrInvalidType|29|invalid type|No|BadRequest|
|ErrTxTimeoutHeight|30|tx timeout height|No|BadRequest|
|ErrUnknownExtensionOptions|31|Unknown extension options|No|BadRequest|
|ErrWrongSequence|32|incorrect account sequence|No|BadRequest|
|ErrPackAny|33|failed packing protobuf message to Any|No|BadRequest|
|ErrUnpackAny|34|failed unpacking protobuf message from Any|No|BadRequest|
|ErrLogic|35|internal logic error|No|AkashNetworkError|
|ErrConflict|36|conflict|Yes ??|BadRequest|
|ErrNotSupported|37|feature not supported|No|BadRequest|
|ErrNotFound|38|not found|No|BadRequest|
|ErrIO|39|Internal IO error|Yes|AkashNetworkError|
|ErrAppConfig|40|error in app.toml|??|??|
|ErrPanic|111222|panic|Yes|AkashNetworkError|
[Source code with error reference](https://github.com/cosmos/cosmos-sdk/blob/v0.45.9/types/errors/errors.go)



### Retry Policies and circuit breaker
Client library has deep knowledge of the error types/models and which one of those are good candidates for
retries. That close bound, also empowers the library to be better positioned to make opinionated decisions on
how long to retry and when a circuit breaker should be open/closed.

## Usability

### Learnability

* The source code **must** include comments and be understandable
* The user documentation, How it Works, FAQ and help should be **complete**
* The interface should be common across programming languages. It will be defined and published as documentation.

### Performance

* The API must provide a synchronous interface.
* The maximum page size is 1000 entities per request. The default is 100.

### Latency

Service request posting must be **real time**.

## Manageability/Maintainability

## Observability

* Every library implementation must provide observability mechanisms such as transaction signing similar to Akash
  Terraform Provider’s observability mechanism.

## Maintenance

The API must be modular for ease of management. All client libraries should follow the same interface with divergence
where standards and patterns are stronger.

The API must employ good design practices and follow SOLID principles.

Documentation should be provided for every supported language and hosted together. A framework should be set to allow
contributions from the open source community.

## System Interface/Integration

### Systems Interfaces

#### 1. Client-to-Akash Interface

The client will perform requests to the Akash Network through a REST API and RPC. RPC will be used for everything related to transactions (tx) and the REST API for queries (query).

### User Scenarios/Use Cases

A development team wants to create a system that integrates with the Akash Network, such as the Akash Terraform
Provider, a new CLI or an automatic deployment tool. That team will use one of the provided client libraries that works
for their technology stack and integrate their solution with the Akash Network. Their system will now be an Akash-native
system when running on Akash.

## Deleted or Deferred Requirements

Other requirements that have been deleted or delayed until future phases of the system:

|Req#|Business Requirement|Status|Comments|Pri|Date Rvwd|SME Reviewed /Approved|
|----|--------------------|------|--------|---|---------|----------------------|
## Requirements Confirmation/Stakeholder sign-off

Include documentation of the approval or confirmation of the requirements here. For example:

|Meeting Date|Attendees (name and role)|Comments|

# APPENDIX

## Definitions, Acronyms, and Abbreviations

Define all terms, acronyms, and abbreviations used in this document.

None

## References

List all the documents and other materials referenced in this document.

None

## Requirements Traceability Matrix

N/A
