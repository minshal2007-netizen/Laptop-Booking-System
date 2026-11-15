# EF101-P11: Computer Hardware Inventory and Maintenance System

A web application for managing computing assets in a lab, department or small company, with fault and maintenance tracking.

**Course:** EF-101 Fall 2026 | **Group size:** 3 students | **Submission:** 9 November 2026

**Live version:** https://minshal2007-netizen.github.io/Laptop-Booking-System/
**Repository:** https://github.com/minshal2007-netizen/Laptop-Booking-System

---

## How to Run the Project (Step by Step)

No installation, server or internet connection is needed. The whole system is one file: `index.html`.

### Option A: Run online (fastest)
1. Open this link in any browser (Chrome, Edge, Firefox, Safari):
   https://minshal2007-netizen.github.io/Laptop-Booking-System/
2. The Dashboard loads with 30 demo assets. Done.

### Option B: Run on your computer (offline)
1. Go to the repository page on GitHub.
2. Click the green **Code** button, then **Download ZIP**.
3. Open your Downloads folder, right-click the ZIP file and choose **Extract All** (on Mac, double-click it).
4. Open the extracted folder.
5. Double-click **index.html**. It opens in your default browser.
6. The Dashboard loads with 30 demo assets. Done.

### Option C: Run from a Git clone
1. Install Git from https://git-scm.com.
2. Open a terminal in the folder where you want the project.
3. Run: `git clone https://github.com/minshal2007-netizen/Laptop-Booking-System.git`
4. Open the new folder and double-click **index.html**.

### Requirements
- Any modern web browser
- JavaScript enabled (it is by default)
- Do not use private/incognito mode if you want your changes to be saved

---

## How to Use the System

1. **Dashboard:** view total, operational, faulty and out-of-warranty assets, charts, and assets requiring attention.
2. **Assets tab:**
   - Tap **+ Add asset**, fill in the form, tap **Save asset**.
   - Use the search box and dropdown filters (CPU family, RAM, storage, location, status, warranty).
   - Tap **Edit**, **History**, **Log fault** or **Retire** on any asset card.
3. **Maintenance tab:** tap **+ Record event** to log a fault (asset, date, description, action, technician, cost).
4. **Export:** tap **Export inventory** or **Export maintenance**, then **Download .csv** or **Copy CSV**.
5. **Field guide tab (in the explainer) / Reset:** the **Field guide** tab explains the hardware terms, and **Reset demo data** restores the original 30 assets.

---

## Features
- Add, edit, search and retire/reactivate assets
- 30 demo asset records and 26 demo maintenance events
- Maintenance events with date, fault description, action, technician and cost
- Maintenance history for each asset
- Filter by CPU family, RAM size, storage type, location, status and warranty
- Dashboard with total, operational, faulty, out-of-warranty and attention-needed assets
- Charts: RAM size, storage type, fault category
- Most frequently failing asset and fault category
- CSV export of inventory and maintenance data
- Dark mode and mobile-friendly layout

## Architecture
Three layers, all running in the browser:
1. **Interface:** HTML and CSS
2. **Logic:** JavaScript (validation, filtering, calculations)
3. **Storage:** localStorage holding JSON

## Database Design
Two entities in a one-to-many relationship:

| ASSET | MAINTENANCE_EVENT |
|---|---|
| **id (PK)**, make, model, cpu, ram, stype, scap, gpu, os, ip, loc, purchase, warranty, status | **id (PK)**, **asset (FK -> ASSET.id)**, date, cat, fault, action, tech, cost |

One asset has many maintenance events; each event belongs to one asset.

- **Soft delete:** retiring sets `status = "Retired"`, so history is kept.
- **Cascade update:** renaming an asset ID updates its events.
- **Derived data:** warranty status, CPU family and "needs attention" are calculated, not stored.
- **Validation:** required fields, positive RAM, unique asset ID.

## Troubleshooting
- **Page is blank or looks plain:** use a modern browser and make sure `index.html` was fully extracted from the ZIP, not opened from inside it.
- **Data disappeared:** browser storage was cleared or you used private mode. Open **Help/Reset demo data** to reload the demo set.
- **Download button does nothing:** use **Copy CSV** and paste into a text file saved as `.csv`.

## Limitations
- Single user, single browser; data is lost if browser storage is cleared
- About 5 MB storage limit
- No login or roles
- No enforced foreign keys, indexes or transactions
- Specifications entered manually

## Future Work
SQLite/PostgreSQL backend with an API, user accounts, QR asset labels, maintenance reminders, depreciation dashboard.

## Team
- Inshal Iqbal
- Huzaifa
- Isfaryaab





