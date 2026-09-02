# Salesforce CPQ Org Setup
This document contains the setup and configuration details of the
Salesforce environment used for the CPQ learning and implementation project.

---

# 1. Org Information
| Item | Details |
|---|---|
| Org Type | Developer Edition (signed up separately, not a Trailhead Playground) |
| Org Name | TBD — Setup → Company Information → "Organization Name" |
| Org ID | TBD — Setup → Company Information → "Salesforce Organization ID" (18-char ID) |
| My Domain | TBD — Setup → Quick Find → "My Domain" → copy the domain shown (e.g. `yourdomain.develop.my.salesforce.com`) |
| Environment | Development / Learning (non-production) |
| Salesforce Edition | Developer Edition |
| Currency | English (United States) - USD |
| Time Zone | (GMT-07:00) Pacific Daylight Time (America/Los_Angeles) |
> Update these details after the Salesforce org is ready.

---

# 2. Salesforce CPQ Installation
## CPQ Package
- [x] Salesforce CPQ package installed
- [x] CPQ package version documented
- [ ] CPQ permissions configured — **not confirmed, see Issue 1**
- [ ] CPQ application accessible — **pending permission set fix**
- [ ] CPQ configuration verified — not yet started

### Package Information
Package Name:
Salesforce CPQ

Version:
262.0 (1GP, namespace SBQQ)

Installation Date:
9/2/2026, 1:41 AM

Additional details: Status = Active, License = Unlimited, Expiration = Does Not Expire, installed via a direct package installation link.

---

# 3. Users
The project will simulate different users involved in a real CPQ
sales process.

| User | Responsibility |
|---|---|
| Sales Representative | Creates opportunities and quotes |
| CPQ User | Configures products and quotes |
| Sales Manager | Reviews discounts and approvals |
| System Administrator | Maintains CPQ configuration |

**Current actual users in org:** 1 (self — Abhishek Koluguri). All four
roles above will initially be simulated by this single user until/unless
additional users are added.

---

# 4. Permissions
Document the permission sets and permissions required for the
project.

### Permission Sets
Currently assigned to primary user (confirmed via screenshot):
- Data Cloud Architect
- Agentforce Default Admin
- Prompt Template Manager
- Agentforce Service Agent Configuration
- Service Cloud User
- (list may include more — not fully visible; recheck full list)

**Missing:** No CPQ-specific permission set (e.g. "SBQQ User" /
"Salesforce CPQ User") confirmed as assigned. This needs to be located
in Setup → Permission Sets and assigned before CPQ functionality can
be reliably used.

### Additional Permissions
- TBD — once CPQ permission set is assigned, verify field-level access
  to `SBQQ__Quote__c` and related objects if any issues arise.

---

# 5. Initial CPQ Configuration
The following configuration will be reviewed before starting
the implementation.

- [ ] CPQ settings
- [ ] Quote configuration
- [ ] Product configuration
- [ ] Price books — Standard Price Book existence/active status not yet confirmed
- [x] Currency — confirmed USD
- [ ] Tax configuration
- [ ] Discount configuration
- [ ] Contract configuration
- [ ] Renewal configuration
- [ ] Approval configuration

---

# 6. Org Validation
Before starting the project, verify:

- [x] Can access Salesforce
- [ ] Can access CPQ functionality — blocked pending permission set
- [ ] Can create products
- [ ] Can create opportunities
- [ ] Can create quotes
- [ ] Can add products to quotes
- [ ] Can calculate quote pricing

---

# 7. Screenshots
Screenshots of the org setup will be added here.

### Salesforce Org
Company Information page — captured.

### CPQ Application
Installed Packages page (showing version 262.0, Active status) — captured.

### CPQ Configuration
_To be added._

### Permission Configuration
Permission Set Assignments page — captured (revealed missing CPQ
permission set).

---

# 8. Setup Issues
Document any issues encountered during setup.

## Issue 1
### Problem
No CPQ-specific permission set (e.g. "SBQQ User") is confirmed as
assigned to the primary user, even though the Salesforce CPQ package
shows as Active/Installed.

### Root Cause
TBD — likely the package installer does not auto-assign the
CPQ-related permission set to all users; it usually must be manually
located in Setup → Permission Sets and assigned.

### Solution
TBD — pending: locate the CPQ permission set in Setup → Permission
Sets, assign it to the user, then verify the Quote tab/object becomes
accessible via App Launcher.

### Lesson Learned
Package "Installed" and "Active" status only confirms the package
exists in the org — it does not confirm the current user has
permission to use its features. Permission sets must be checked
separately.

---

# 9. Setup Completion
| Setup Item | Status |
|---|---|
| Salesforce Org | ✅ |
| CPQ Package | ✅ |
| Users | 🟡 (single user only so far) |
| Permissions | ⬜ (CPQ permission set gap — see Issue 1) |
| CPQ Settings | ⬜ |
| Price Book | ⬜ |
| Quote Configuration | ⬜ |
| Org Validation | ⬜ |

---

# 10. Final Notes
This org will be used as the hands-on environment for the
continuous Salesforce CPQ implementation project.
All major configuration changes will be documented in this repository.
