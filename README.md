# Remote Hustle – Infrastructure Repo

A production-grade static site deployment for Remote Hustle, built as part of
the Stage 2 DevOps & Infrastructure practical assessment.

---

## Quick Start (First-Time Setup)

### Prerequisites

- A GitHub account
- Git installed locally

### 1. Fork / clone this repo

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### 2. Enable GitHub Pages

1. Go to **Settings → Pages**
2. Set **Source** → **GitHub Actions**
3. Check **Enforce HTTPS**

### 3. Update CODEOWNERS

Open `.github/CODEOWNERS` and replace `@YOUR_GITHUB_USERNAME` with your actual
GitHub username.

### 4. Push to `main`

```bash
git add .
git commit -m "initial: deploy Remote Hustle site"
git push origin main
```

The deploy workflow runs automatically. Your site will be live at:

```
https://mbaiye.github.io/remoteHustle_task2/
```

---

## Workflows

| Workflow         | Trigger                    | Purpose                            |
|------------------|----------------------------|------------------------------------|
| `deploy.yml`     | Push to `main` / manual    | Deploy site to GitHub Pages        |
| `backup.yml`     | Daily 02:00 UTC / manual   | Back up `website/` to `backups` branch |
| `restore.yml`    | Manual only                | Restore a backup to production     |

### Triggering a manual restore

1. **Actions → Restore from Backup → Run workflow**
2. Enter a timestamp (e.g. `2026-03-18T02-00-00Z`) or leave blank for latest
3. The workflow verifies, extracts, and redeploys automatically

---

## Making Changes

```bash
# 1. Create a feature branch
git checkout -b feature/my-update

# 2. Edit website/index.html (or add assets)

# 3. Commit and push
git add website/
git commit -m "feat: update hero copy"
git push origin feature/my-update

# 4. Open a Pull Request on GitHub → review → merge
# Deploy runs automatically after merge
```

---

## Security

See [SECURITY.md](./SECURITY.md) for the full security policy, including:
- SSL/TLS configuration
- User roles and branch protection rules
- Safe login, update, and recovery procedures
- Incident response matrix

---

## Monitoring

See [docs/monitoring-setup.md](./docs/monitoring-setup.md) for UptimeRobot
configuration steps and dashboard access.

---

_Remote Hustle | Stage 2 DevOps – Candidate RHK-001_
