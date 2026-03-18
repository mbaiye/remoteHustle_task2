# Security Policy – Remote Hustle Infrastructure

## Overview

This document describes the security measures in place for the Remote Hustle
GitHub Pages deployment. It covers SSL/TLS, access control (user roles),
firewall-equivalent protections, and safe operational procedures.

---

## 1. SSL / TLS Certificate

**Provider:** GitHub Pages built-in SSL (powered by Let's Encrypt)

- HTTPS is **enforced by default** on all GitHub Pages sites.
- The certificate auto-renews every 90 days — no manual action required.
- To verify: go to **Repository Settings → Pages** and confirm
  "Enforce HTTPS" is ticked.

---

## 2. User Roles & Access Control

GitHub's built-in role system is used to enforce least-privilege access:

| Role          | Who                        | Permissions                                      |
|---------------|----------------------------|--------------------------------------------------|
| **Owner**     | Repository owner (admin)   | Full access: settings, secrets, branch rules     |
| **Maintainer**| Senior DevOps team member  | Push to `main`, manage Actions, read secrets     |
| **Developer** | General contributors       | Push to feature branches only, open PRs          |
| **Read**      | QA / reviewers             | Clone & read only, no write access               |

### Enforcement rules (Branch Protection on `main`)

- Require pull request reviews before merging (minimum 1 reviewer)
- Require status checks to pass (CI/CD deploy workflow must succeed)
- Restrict who can push directly to `main` — Owner and Maintainer only
- Do not allow force pushes or branch deletion

---

## 3. Firewall & Hosting Security

GitHub Pages is a managed hosting platform. The following controls apply:

| Control                         | Implementation                                               |
|---------------------------------|--------------------------------------------------------------|
| DDoS protection                 | GitHub / Fastly CDN absorbs volumetric attacks automatically |
| HTTPS-only traffic              | HTTP requests are redirected to HTTPS by GitHub Pages        |
| No server-side code execution   | Pure static site — no attack surface for code injection      |
| Dependency pinning              | All GitHub Actions use SHA-pinned or major-version-pinned    |
| Secret management               | API keys / tokens stored only in GitHub Encrypted Secrets    |
| Backup branch protection        | `backups` branch has push restricted to `github-actions[bot]`|

---

## 4. Safe Login, Update & Recovery Procedures

### Logging In (GitHub Account)
1. Use a **strong, unique password** (min 20 characters, mixed case + symbols).
2. Enable **two-factor authentication (2FA)** — preferably a hardware key (YubiKey)
   or TOTP app (e.g., Authy, Google Authenticator). SMS 2FA is discouraged.
3. Never share your GitHub credentials. Use **Personal Access Tokens (PAT)**
   scoped to minimal permissions for CLI/API access.

### Updating the Site
1. Create a feature branch: `git checkout -b fix/your-change`
2. Make your changes to files inside `website/`
3. Push the branch and open a Pull Request against `main`
4. Wait for the CI check to pass and at least one peer review
5. Merge — the deploy workflow will automatically publish to GitHub Pages

### Recovery Procedure
1. Identify the backup timestamp to restore from the `backups` branch
2. Go to **Actions → Restore from Backup → Run workflow**
3. Enter the timestamp (or leave blank for latest backup)
4. The workflow will verify the SHA-256 checksum, extract, and push restored
   files to `main`; the deploy workflow then re-publishes the site automatically
5. Verify the live site URL after the deploy completes

---

## 5. Incident Response

| Severity | Example                          | Action                                                  |
|----------|----------------------------------|---------------------------------------------------------|
| Critical | Site defaced / data exfiltrated  | Revoke all tokens, rotate secrets, restore from backup  |
| High     | Unauthorized merge to `main`     | Revert commit, review audit log, notify Owner           |
| Medium   | Failed backup / deploy           | Re-run workflow manually, investigate Actions logs      |
| Low      | Dependency version warning       | Open PR to update pinned versions                       |

---

_Last updated: 2026-03-18 | Candidate: RHK-001_
