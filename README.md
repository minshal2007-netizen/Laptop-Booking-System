# EF101-P11: Computer Hardware Inventory and Maintenance System

A web application for managing computing assets in a lab, department or small company, with maintenance and fault tracking.

**Course:** EF-101 Fall 2026 | **Group size:** 3 | **Submission:** 9 November 2026

## Run it
- **Online:** open the GitHub Pages link: `https://<username>.github.io/<repo-name>/`
- **Offline:** download or clone this repo and double-click `index.html`. No install, server or internet needed.

## Features
- Add, edit, search and retire/reactivate assets
- 30 demo asset records and 26 demo maintenance events
- Record fault events (date, description, action, technician, cost)
- Maintenance history for each asset
- Search and filter by CPU family, RAM, storage type, location, status and warranty
- Dashboard: total, operational, faulty, out-of-warranty and needs-attention assets
- Hardware distribution charts (RAM, storage type, fault category)
- Most frequently failing asset and fault category
- CSV export of inventory or maintenance data (copy or download)
- Dark mode and mobile-friendly layout

## Architecture
Three layers, all running in the browser:
1. **Interface:** HTML + CSS
2. **Logic:** JavaScript (validation, filtering, calculations)
3. **Storage:** `localStorage` holding JSON

## Database design
Two entities in a one-to-many relationship:

| ASSET | MAINTENANCE_EVENT |
|---|---|
| **id (PK)**, make, model, cpu, ram, stype, scap, gpu, os, ip, loc, purchase, warranty, status | **id (PK)**, **asset (FK -> ASSET.id)**, date, cat, fault, action, tech, cost |

One asset has many maintenance events; each event belongs to one asset.

- **Soft delete:** retiring sets `status = "Retired"`, so history is kept.
- **Cascade update:** renaming an asset ID updates its events.
- **Derived data:** warranty status, CPU family and "needs attention" are calculated, not stored.
- **Validation:** required fields, positive RAM, unique asset ID.

Equivalent SQL: `SELECT ram, COUNT(*) FROM asset GROUP BY ram` (RAM chart); `SELECT asset, COUNT(*) FROM event GROUP BY asset ORDER BY 2 DESC LIMIT 1` (most failing asset).

## Limitations
- Single user, single browser; data is lost if browser storage is cleared
- About 5 MB storage limit
- No login or roles
- No enforced foreign keys, indexes or transactions
- Specifications entered manually

## Future work
SQLite/PostgreSQL backend with an API, user accounts, QR asset labels, maintenance reminders, depreciation dashboard.

## Team
- Inshal Iqbal
- Huzaifa Ahmed
- Isfaryab Jameel
