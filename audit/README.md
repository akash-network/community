# Provider manual audit

**This is the only way to get your Akash provider audited.** Follow this guide: the audit is a **long-running benchmark** inside a deployment that serves a **web UI**. Reviewers use the **HTTPS URL** you give them (after everything passes).

**SDL to deploy:** [standalone-audit.sdl.yaml](https://github.com/akash-network/community/blob/main/audit/standalone-audit.sdl.yaml)

**Only open a [Provider Audit] GitHub issue after** the benchmark has finished **and all tests are passing** in the UI. Do not file while tests are still running or if anything failed—fix it, redeploy if needed, then submit.

## Prerequisites

Before you deploy the audit workload, your provider should be set up correctly.

### 1. Attributes and contact

- **Community** tier and valid **contact** (email, website) on-chain, plus the usual `host` / capability keys.
- Your **on-chain attributes must match every capability you offer**—for example **GPU**, **shared memory (SHM)**, **persistent storage**, and any other resource you advertise—so what reviewers see on-chain lines up with the audit workload and your SDL.
- Reference: [Provider attributes](https://akash.network/docs/providers/operations/provider-attributes/).

Example query:

```text
$ provider-services query provider get akash1<...> -o text
```

### 2. Ingress DNS

- **`*.ingress.<yourdomain>`** should resolve to your provider.
- Example check: `host <anything>.ingress.<yourdomain>`
- Configure DNS: [Provider installation — Step 7](https://akash.network/docs/providers/setup-and-installation/kubespray/provider-installation/#step-7---configure-dns).

### 3. Firewall / NAT

- Do not block Akash provider ports.
- Reference: [Provider installation — Step 12 (Verify firewall)](https://akash.network/docs/providers/setup-and-installation/kubespray/provider-installation/#step-12---verify-firewall).

### 4. Akash Discord (provider role) and email

- You must **be in the Akash Discord** and have the **Provider** role (or equivalent).
- When you request an audit, you will need your **Discord username** and a working **email** so reviewers can verify you and follow up.

---

## Deploy the SDL

1. Start from **[standalone-audit.sdl.yaml](https://github.com/akash-network/community/blob/main/audit/standalone-audit.sdl.yaml)**.
2. Set **`AUDIT_PROVIDER_ID`** to your **provider owner address** (or a clear label).
3. Adjust **CPU, memory, storage**, and—only if they match what you advertise—**GPU**, **persistent volume**, and **SHM** so the manifest fits your provider’s **capabilities**. You do not need to edit anything else in the file.

The deployment serves a **web UI** on **HTTPS port 80**; share that URL with reviewers when benchmarks are done.

---

## After the deployment is live

1. Open the **HTTPS URL** you get from the provider (port **80**).
2. The UI may show **running** until benchmarks finish; a full run is often on the order of **~1 hour**, depending on profile and GPU.
3. When complete, reviewers can use the dashboard (and raw JSON if needed).
4. **Keep the deployment running** until a reviewer confirms they are done.

---

## When tests have passed — request the audit

Open a **[Provider Audit]** issue in the **[Akash community GitHub](https://github.com/akash-network/community/issues)** and include:

- Your **provider owner address** and **HTTPS URL** of the audit deployment.
- **Discord username** and **email** (required) for verification and follow-up.
- **Name** (optional).

A reviewer will confirm results and follow up in the issue. If something fails, fix it, redeploy if needed, and update the thread.
