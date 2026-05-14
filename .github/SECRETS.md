# Workflow Secrets

This file documents the repository secrets the GitHub Actions workflows in
this repo depend on, and how to rotate them when they expire.

## `WORKFLOW_PAT`

**Used by:** [`akash-network-website-update.yml`](./workflows/akash-network-website-update.yml)

**Purpose:** Sends a `repository_dispatch` event to `akash-network/website`
when SIG / WG / committee group docs change here, so the website's
[`akash-community-groups.yml`](https://github.com/akash-network/website/blob/main/.github/workflows/akash-community-groups.yml)
workflow can pull the updated `README.md` files into its content collection.

**Why we need a PAT** (not the default `GITHUB_TOKEN`): the default
`GITHUB_TOKEN` is scoped to the current repository only. Cross-repo
`repository_dispatch` requires a PAT (or a GitHub App token) that has write
access to the **target** repository.

### Required scopes

Use a **fine-grained personal access token** owned by a service account or
a maintainer who has write access to `akash-network/website`. Configure it as:

- **Resource owner:** `akash-network`
- **Repository access:** *Only select repositories* → `akash-network/website`
- **Repository permissions:**
  - **Contents:** *Read and write*  *(required to dispatch events)*
  - **Metadata:** *Read-only*  *(auto-selected)*
- **Expiration:** maximum 1 year. Set a calendar reminder one week before
  expiry to rotate.

A classic PAT with the `repo` scope also works but is broader than necessary
and is discouraged.

### How to rotate

1. **Mint a new token**
   - Go to <https://github.com/settings/personal-access-tokens/new> while
     signed in as the service account (or your account if you own this).
   - Name it `akash-community → akash-website dispatch (YYYY-MM-DD)` so the
     rotation date is visible in the token list.
   - Apply the scopes listed above.
   - Copy the token value — it is only shown once.

2. **Update the secret**
   - Open
     <https://github.com/akash-network/community/settings/secrets/actions>.
   - Click `WORKFLOW_PAT` → *Update secret*.
   - Paste the new token value → *Update secret*.

3. **Verify**
   - Go to the *Actions* tab → *Trigger Groups Update* workflow.
   - Click *Run workflow* → run on `main`.
   - Confirm the run succeeds (~10s). On `akash-network/website`, the
     *Update Community Groups* workflow should fire shortly after.

4. **Revoke the old token**
   - Once the new token is verified, delete the old one from the token list
     so a leaked old token is not reusable.

### Symptoms of an expired token

- *Trigger Groups Update* runs fail in ~10s on the
  `peter-evans/repository-dispatch` step with `##[error]Bad credentials`.
- *Update Community Groups* on `akash-network/website` stops being triggered
  by pushes to this repo (its run history will only show
  `workflow_dispatch` runs, no `repository_dispatch` runs).
