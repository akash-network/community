# **Requirements Specification**

## **Version 1.1-RC**

## January 11, 2023

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
<table>
  <thead>
    <tr>
      <td>Error</td>
      <td>Code</td>
      <td>Description</td>
      <td>Should Retry</td>
      <td>Mapped to</td>
    </tr>
  </thead>
  <tr>
    <td>errInternal</td>
    <td>1</td>
    <td>Internal - not supposed to happen</td>
    <td>Yes</td>
    <td>AkashNetworkError</td>
  </tr>
  <tr>
    <td>ErrTxDecode</td>
    <td>2</td>
    <td>tx parse error</td>
    <td>Yes</td>
    <td>AkashNetworkError</td>
  </tr>
  <tr>
    <td>ErrInvalidSequence</td>
    <td>3</td>
    <td>invalid sequence</td>
    <td>Yes</td>
    <td>?? what is a sequence ??</td>

  </tr>
  <tr>
    <td>ErrUnauthorized</td>
    <td>4</td>
    <td>unauthorized</td>
    <td>No</td>
    <td>AuthError</td>
  </tr>
  <tr>
    <td>ErrInsufficientFunds</td>
    <td>5</td>
    <td>Not enough funds</td>
    <td>No</td>
    <td>StateError</td>
  </tr>

  <tr>
    <td>ErrUnknownRequest</td>
    <td>6</td>
    <td>unkown request</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>RootCodespace</td>
    <td>7</td>
    <td>invalid address</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrInvalidPubKey</td>
    <td>8</td>
    <td>invalid pubkey</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrUnknownAddress</td>
    <td>9</td>
    <td>unknown address</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrInvalidCoins</td>
    <td>10</td>
    <td>invalid coins</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrOutOfGas</td>
    <td>11</td>
    <td>out of gas</td>
    <td>No</td>
    <td>StateError</td>
  </tr>
  <tr>
    <td>ErrMemoTooLarge</td>
    <td>12</td>
    <td>memo too large</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrInsufficientFee</td>
    <td>13</td>
    <td>insufficient fee</td>
    <td>No</td>
    <td>StateError</td>
  </tr>
  <tr>
    <td>ErrTooManySignatures</td>
    <td>14</td>
    <td>maximum number of signatures exceeded</td>
    <td>No</td>
    <td>??</td>
  </tr>
  <tr>
    <td>ErrNoSignatures</td>
    <td>15</td>
    <td>no signatures supplied</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrJSONMarshal</td>
    <td>16</td>
    <td>failed to marshal JSON bytes</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrJSONUnmarshal</td>
    <td>17</td>
    <td>failed to unmarshal JSON bytes</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrInvalidRequest</td>
    <td>18</td>
    <td>invalid request</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrTxInMempoolCache</td>
    <td>19</td>
    <td>tx already in mempool</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrMempoolIsFull</td>
    <td>20</td>
    <td>mempool is full</td>
    <td>Yes ??</td>
    <td>AkashNetworkError ?? </td>
  </tr>
  <tr>
    <td>ErrTxTooLarge</td>
    <td>21</td>
    <td>tx too large</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrKeyNotFound</td>
    <td>22</td>
    <td>key not found</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrWrongPassword</td>
    <td>23</td>
    <td>invalid account password</td>
    <td>No</td>
    <td>AuthError</td>
  </tr>
  <tr>
    <td>ErrorInvalidSigner</td>
    <td>24</td>
    <td>tx intended signer does not match the given signer</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrorInvalidGasAdjustment</td>
    <td>25</td>
    <td>invalid gas adjustment</td>
    <td>No</td>
    <td>StateError</td>
  </tr>
  <tr>
    <td>ErrInvalidHeight</td>
    <td>26</td>
    <td>--</td>
    <td>No</td>
    <td>BadRequest ?? </td>
  </tr>
  <tr>
    <td>ErrInvalidVersion</td>
    <td>27</td>
    <td>invalid version</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrInvalidChainID</td>
    <td>28</td>
    <td>invalid chain-id</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrInvalidType</td>
    <td>29</td>
    <td>invalid type</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrTxTimeoutHeight</td>
    <td>30</td>
    <td>tx timeout height</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrUnknownExtensionOptions</td>
    <td>31</td>
    <td>Unknown extension options</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrWrongSequence</td>
    <td>32</td>
    <td>incorrect account sequence</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrPackAny</td>
    <td>33</td>
    <td>failed packing protobuf message to Any</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrUnpackAny</td>
    <td>34</td>
    <td>failed unpacking protobuf message from Any</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrLogic</td>
    <td>35</td>
    <td>internal logic error</td>
    <td>No</td>
    <td>AkashNetworkError</td>
  </tr>
  <tr>
    <td>ErrConflict</td>
    <td>36</td>
    <td>conflict</td>
    <td>Yes ??</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrNotSupported</td>
    <td>37</td>
    <td>feature not supported</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrNotFound</td>
    <td>38</td>
    <td>not found</td>
    <td>No</td>
    <td>BadRequest</td>
  </tr>
  <tr>
    <td>ErrIO</td>
    <td>39</td>
    <td>Internal IO error</td>
    <td>Yes</td>
    <td>AkashNetworkError</td>
  </tr>  
  <tr>
    <td>ErrAppConfig</td>
    <td>40</td>
    <td>error in app.toml</td>
    <td>??</td>
    <td>??</td>
  </tr>
  <tr>
    <td>ErrPanic</td>
    <td>111222</td>
    <td>panic</td>
    <td>Yes</td>
    <td>AkashNetworkError</td>
  </tr>

</table>

[Source code with error reference](https://github.com/cosmos/cosmos-sdk/blob/v0.45.9/types/errors/errors.go)

### Retry Policies and circuit breaker
Client library has deep knowledge of the error types/models and which one of those are good candidates for
retries. That close bound, also empowers the library to be better positioned to make opinionated decisions on
how long to retry and when a circuit breaker should be open/closed.

## **Version 1.0**

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

<table>
  <tr>
   <td><strong>Req#</strong>
   </td>
   <td><strong>Requirement</strong>
   </td>
   <td><strong>Comments</strong>
   </td>
   <td><strong>Priority</strong>
   </td>
   <td><strong>Date Rvwd</strong>
   </td>
   <td><strong>SME Reviewed / Approved</strong>
   </td>
  </tr>
  <tr>
   <td>R_01
   </td>
   <td>Create deployment
   </td>
   <td>Create a deployment based on an SDL file. Request through RPC.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_02
   </td>
   <td>Close deployment
   </td>
   <td>Close a deployment. Request through RPC
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_03
   </td>
   <td>List deployments
   </td>
   <td>List all deployments matching the filters with consideration for page limits. Request through REST.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_04
   </td>
   <td>Get deployment
   </td>
   <td>Request through REST.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_05
   </td>
   <td>List bids
   </td>
   <td>Get the list of bids based on a set of filters. Request through REST.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_06
   </td>
   <td>Create lease
   </td>
   <td>Request through RPC.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_07
   </td>
   <td>Get lease
   </td>
   <td>Get information regarding a lease such as its status. Request through REST.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td>R_08
   </td>
   <td>Send manifest
   </td>
   <td>Request through RPC.
   </td>
   <td>1
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
</table>

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

<table>
  <tr>
   <td><strong>Req#</strong>
   </td>
   <td><strong>Business Requirement</strong>
   </td>
   <td><strong>Status</strong>
   </td>
   <td><strong>Comments</strong>
   </td>
   <td><strong>Pri</strong>
   </td>
   <td><strong>Date Rvwd</strong>
   </td>
   <td><strong>SME Reviewed /Approved</strong>
   </td>
  </tr>
</table>

## Requirements Confirmation/Stakeholder sign-off

Include documentation of the approval or confirmation of the requirements here. For example:

<table>
  <tr>
   <td><strong>Meeting Date</strong>
   </td>
   <td><strong>Attendees (name and role)</strong>
   </td>
   <td><strong>Comments</strong>
   </td>
  </tr>
</table>

# APPENDIX

## Definitions, Acronyms, and Abbreviations

Define all terms, acronyms, and abbreviations used in this document.

None

## References

List all the documents and other materials referenced in this document.

None

## Requirements Traceability Matrix

N/A
