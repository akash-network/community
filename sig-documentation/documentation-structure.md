# **Requirements Specification**

## **Version 1.0**

## January 20, 2023

Requirements for the Akash Documentation Structure

# Executive Summary

## Project Overview

...

## Purpose and Scope of this Specification

Requirements specification for Akash Documentation Structure. This specification focuses mostly on developer-oriented documentation.

### In scope

In-depth blockchain concepts.


### Out of Scope

...

## Product/Service Description

The documentation serves an important role as a support for existing users of the Akash Network but is also extremely important as a gate to new users.


### Product Context

...

## User Characteristics

General customer profiles for each type of user who will be using the documentation are:

* First time users
* Frequent users
* Developers

## Assumptions

We assume first time users are not familiar with Akash Network and cryptocurrencies.
It's also assumed a limited knowledge of cloud/software technologies.

Frequent users are assumed to be looking for quick copy/paste examples and/or quick reference.

Developers are assumed to be looking for client documentation (Java, Go, ...) and/or general documentation.
## Dependencies

* A working Akash wallet with AKT

# Requirements

## Functional Requirements

The following table is a tabulation for the requirements.

|Req#|Requirement|Comments|Priority|Date Rvwd|SME Reviewed / Approved|
|----|-----------|--------|--------|---------|-----------------------|
|R_01|Documentation must be available in English|||||

The proposed structure is as follows:
1. Getting Started
    * Setting up the Environment
    * Your First Deployment
2. Concepts
    * Akash Network
    * Providers
    * Deployments
    * Bids & Leases
    * DSEQ, GSEQ & OSEQ
    * Validator Nodes
    * SDL
3. Architecture
    * Overview
    * Kubernetes & Containers
    * Akash Node
    * Akash Provider
4. Guides
    * Deploy using the CLI
    * Deploying using Cloudmos
    * Deploying using Terraform
5. Developers
    * _This is the scope of the client libraries documentation_

## Usability

### Learnability

The first chapter should allow users to have a running deployment in less than 5 minutes.
It should also permanently setup the user's environment so that the development environment still works on a full restart.
This can be achieved by changing the respective environment variables.