# Uptime Monitoring Setup – UptimeRobot

This guide documents how uptime monitoring was configured for the Remote Hustle
GitHub Pages site.

---

## Tool: UptimeRobot (Free Tier)

**URL:** https://uptimerobot.com  
**Plan:** Free (50 monitors, 5-minute check interval)

---

## Setup Steps

### 1. Create a free UptimeRobot account

1. Go to https://uptimerobot.com and click **Register for FREE**.
2. Confirm your email address.

### 2. Add a new monitor

1. Click **+ Add New Monitor**.
2. Set the following values:

   | Field            | Value                                               |
   |------------------|-----------------------------------------------------|
   | Monitor Type     | HTTP(s)                                             |
   | Friendly Name    | Remote Hustle – Production                          |
   | URL              | `https://<your-username>.github.io/<repo-name>/`   |
   | Monitoring Interval | Every 5 minutes                                 |
   | Alert Contacts   | Your email address                                  |

3. Click **Create Monitor**.

### 3. Set up alert contacts

1. Go to **My Settings → Alert Contacts**.
2. Add your email (or Slack webhook / SMS if on paid plan).
3. UptimeRobot will notify you within minutes of a downtime event.

---

## What is Monitored

| Check          | Details                                          |
|----------------|--------------------------------------------------|
| HTTP status    | Expects `200 OK` from the site URL               |
| Response time  | Tracked per check — visible in dashboard graphs  |
| SSL expiry     | UptimeRobot free tier includes SSL expiry alerts |
| Downtime alert | Email sent if site is down for > 5 minutes       |

---

## Uptime Dashboard

UptimeRobot provides a **free public status page** you can share with
stakeholders:

1. Go to **Public Status Pages** in your dashboard.
2. Click **Create Status Page**.
3. Add your Remote Hustle monitor.
4. Share the generated URL (e.g., `https://stats.uptimerobot.com/xxxxx`).

---

## Interpreting the Results

- **Green (Up):** Site responding normally.
- **Yellow (Seems Down):** First failed check — UptimeRobot re-verifies
  before alerting.
- **Red (Down):** Confirmed outage — check GitHub Actions deploy logs and
  GitHub's status page (https://githubstatus.com).

---

_Last updated: 2026-03-18 | Candidate: RHK-001_
