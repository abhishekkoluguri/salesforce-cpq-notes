# Salesforce CPQ — Package Installation Methods (Reference)

This is reference documentation only. Our TechNova org already has CPQ
installed, so this file exists for future reference (new orgs, interview
questions, or helping someone else set up CPQ).

## Prerequisite (applies to all 3 methods)
Before installing, enable email deliverability so you receive install
status notifications:
**Setup → Quick Find → "Deliverability" → Access Level → set to "All Email" → Save**

Also decide **where** you're installing first — AppExchange experts
recommend testing in a Developer Edition org or sandbox before ever
installing into production.

---

## Method 1: Install via AppExchange Listing ("Get It Now")
This is the standard route for any Salesforce managed package, including CPQ.

1. Go to AppExchange (appexchange.salesforce.com) and search for
   "Salesforce CPQ", or go to Setup → Quick Find → "AppExchange" from
   inside your org.
2. Open the Salesforce CPQ listing and click **Get It Now**.
3. Log in with your Salesforce credentials if prompted.
4. Choose the target org from the **Connected Salesforce Accounts**
   picker — this is where you select Production, Sandbox, or your
   Developer org. **Double-check the username shown on the
   confirmation screen** before proceeding — installing into the
   wrong org is a common, hard-to-undo mistake.
5. Choose install option: **Install for All Users** (most common for
   learning/demo orgs) vs. Admins Only / Specific Profiles.
6. Click **Install**, then **Approve Third-Party Access → Continue**.
7. Installation runs in the background; you'll get an email when it
   completes (hence the deliverability prerequisite above).

**When to use:** General-purpose installs, most realistic to how it's
done in real client projects.

---

## Method 2: Install via a Direct Package Installation Link
Salesforce CPQ (and other managed packages) can also be installed via
a direct install URL rather than browsing AppExchange. This is common
when a Salesforce rep, partner, or training provider sends you a
specific link tied to a specific package version.

1. Open the provided installation link in your browser
   (format is typically `https://login.salesforce.com/packaging/installPackage.apexp?p0=<packageId>`,
   or historically `install.steelbrick.com` for older CPQ versions —
   Steelbrick was the company Salesforce acquired to create CPQ).
2. Log in to the target org.
3. On the Package Installation screen, review the components being
   installed, choose **Install for All Users**, click **Install**.
4. Approve third-party access if prompted → Continue.

**When to use:** When you're given a specific link (e.g., by a trainer,
partner, or a specific CPQ version/trial link) rather than browsing
the general AppExchange listing.

**Important:** Direct links are version-specific. Always confirm which
CPQ version the link installs — check with whoever provided it, don't
assume it's the latest.

---

## Method 3: Dedicated CPQ Trial/Trailhead Org Signup
For learning purposes specifically, Salesforce sometimes offers signup
links that provision a **new org with CPQ pre-installed**, skipping
manual installation entirely.

1. Use a provided CPQ trial signup link (these change over time —
   search "Salesforce CPQ free trial org" or check current Trailhead
   CPQ modules for an active link, since these links get retired and
   replaced).
2. Fill in the signup form (name, email, company).
3. You receive login credentials via email for a **new org that
   already has the CPQ package installed** — no manual install step.

**When to use:** Fastest path for pure learning/practice when you
don't already have a Developer org, or want a guaranteed-clean CPQ
environment. Not representative of a real implementation project,
since real projects install into an existing client org.

---

## How Our Org Was Set Up
We used a **Developer Edition org (signed up separately)** with CPQ
installed and confirmed. Exact method used ( direct link -steelvbrick).

## Interview Angle
A common interview question: *"How do you install Salesforce CPQ in a
new org?"* — the strong answer covers all three paths above, plus the
prerequisite about testing in sandbox/dev org before production, since
that shows implementation maturity, not just knowing steps.
