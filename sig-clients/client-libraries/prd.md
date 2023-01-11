# **Requirements Specification**

## **Version 1.0**

## October 25, 2022

Requirements for Akash Network Client Libraries

# Executive Summary

## Project Overview
Client libraries allow developers to interact with remote services through a defined interface using their preferred programming languages. They can also help abstract the complexity associated with communication protocols used by those remote services. Client libraries work as enablers for developers to build on existing systems while maintaining a common interface across clients.

For Akash, having client libraries would make building in the ecosystem more accessible and simple. By providing the same interface across implementations developers wouldn’t need to relearn concepts to interact with the network while still being able to develop in different programming languages.
 
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
Client libraries for the Akash Network will enable developers to build on top of Akash with their favorite developer programming stacks, including but not limited to;

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
* Every library implementation must provide observability mechanisms such as transaction signing similar to Akash Terraform Provider’s observability mechanism.

## Maintenance
The API must be modular for ease of management. All client libraries should follow the same interface with divergence where standards and patterns are stronger.

The API must employ good design practices and follow SOLID principles.

Documentation should be provided for every supported language and hosted together. A framework should be set to allow contributions from the open source community.

## System Interface/Integration

### Systems Interfaces

#### 1. Client-to-Akash Interface
    The client will perform requests to the Akash Network through a REST API and RPC. RPC will be used for everything related to transactions (tx) and the REST API for queries (query).

### User Scenarios/Use Cases
A development team wants to create a system that integrates with the Akash Network, such as the Akash Terraform Provider, a new CLI or an automatic deployment tool. That team will use one of the provided client libraries that works for their technology stack and integrate their solution with the Akash Network. Their system will now be an Akash-native system when running on Akash.

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