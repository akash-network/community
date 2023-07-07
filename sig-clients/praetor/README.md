# Praetor - Web UI for Provider Onboarding

[Praetor](https://praetorapp.com) provides an easy way to become a cloud provider for Akash Network. You can become a provider using a simplified UI rather than Command-line Interface. Once you become a cloud provider, and if the deployers choose your provider to deploy their application, they pay you in AKT.
You can provide a single server or multiple servers using Praetor App. We support the following operating systems - Ubuntu, Debian, and CentOS.
If you have Kubernetes that you are not fully utilizing, you can also provide it to the Akash Network. The app can help you make your existing Kubernetes ready for Akash Network and spin up the Provider Service, which you need to accept the bids/manifests.

Praetor have created additional tools to help Akash community.

* [Provider Profitibility Calculator](https://akash.praetorapp.com/calculator)
Use this calculator to calculate how much you will earn if you provide your compute power to Akash.
We are using recent Osmosis price for AKT to USD calculation.
* [Akash Provider Real-Time Status Dashboard](https://akash.praetorapp.com/provider-status)
Use this status page to check an Akash Provider information and status.

## Meetings

Client Libraries will be discussed during the Clients SIG meetings, at least to start with.

## Lead(s)

Jigar Patel, Praetor Team (@jigar-arc10)

Deval Patel, Praetor Team (@devalpatel67)

## Contact
- [Praetor Akash Discord Channel](https://discord.com/channels/747885925232672829/1010267674045055148)
- [Praetor Discord](https://discord.gg/uzUCHTF93D)

## Roadmap

* Content Moderation & Lease Dashboard
    * Implement management API in the Akash provider service for content moderation
    * Implement management API in Praetor for content moderation
    * Implement a lease dashboard in Praetor
    * Help providers implement the moderation API in the Akash provider service.

* Helm Upgrade
    * Install a new provider with Helm.
    * Upgrade existing providers to Helm.
    * Provide Praetor functionalities to existing non-Praetor providers.

* Financial Dashboard
    * Create a financial dashboard for providers.
    * Show current month and upcoming projections based on leases
    * Show historic lease financial data
    * Process financial data securely using Airflow or integrate with indexers like Cloudmos.

* Existing Provider Feature
    * Integrate moderation API to allow providers to ban image-based leases
    * Add persistent storage for existing providers using the dashboard
    * Support existing EDU program participants and create new curriculums


### May 17 Update
* Become Akash provider using a newer and efficient helm method on a single server (New Providers)- Testing - early next week
* Become Akash provider using a newer and efficient helm method for K8S Kubernetes Build with multiple servers (New Providers) - Testing - early next week
* GPU support for testnet - In Development - Target Time - early next week
* Migration for existing praetor providers from custom provider service to helm chart - In Development
* PRDs for content moderation - In Development 


### PRDs
  * [Working Group - Content Moderation PRDs](../../wg-content-moderation/prd.md)
  * [Management API](../../wg-content-moderation/management-api.md)
  * [Moderation API](../../wg-content-moderation/moderation-api.md)
