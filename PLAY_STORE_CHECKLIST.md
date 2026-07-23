# Google Play Store Publishing Checklist — Individual Developer (India)

Current as of **23 July 2026**. Covers everything an individual (Personal account) developer in India needs — account-level requirements and app-level requirements — before an app can go live on Google Play.

---

## Part A — Developer Account Requirements (Personal Account, India)

### A.1 Prerequisites
- [ ] Google account with **2-Step Verification** enabled (required before signup starts)
- [ ] Valid credit/debit card in your legal name (Visa, Mastercard, Amex — **no prepaid cards, no PayPal**)

### A.2 Registration
- [ ] Pay the one-time **US $25** registration fee (charged in INR equivalent + applicable GST/taxes)
- [ ] Choose account type: **Personal** (Organization only required for regulated categories — see A.6)
- [ ] Accept the Google Play Developer Distribution Agreement

### A.3 Identity Verification
- [ ] Indian government-issued photo ID (Aadhaar / PAN / passport / driving license)
- [ ] Proof of address document, issued within the last **90 days** (utility bill, bank/card statement, lease agreement) — must clearly show name **and** address
- [ ] Live selfie / face check (may be requested)
- [ ] **Critical:** legal name and address must match exactly across — ID document, proof of address, Google payment profile, and the card used for the $25 fee. Mismatches are the #1 rejection reason.

### A.4 Google Payments Profile
- [ ] Linked payments profile (required before account creation completes; this is where identity + the $25 fee are processed)

### A.5 Developer Profile
- [ ] Developer/trade name (public-facing, can be changed later)
- [ ] Verified email address (OTP-verified)
- [ ] Website URL starting with `https://` (basic landing page is sufficient)
- [ ] Brief statement on app-building experience
- [ ] Declaration of whether this is your only Play Console account (must disclose others if any)

### A.6 Organization Account (only if applicable)
- [ ] Only required if your app is in a regulated category: banking, lending, stock trading, crypto wallets/exchanges, etc.
- [ ] If required: D-U-N-S number (free from Dun & Bradstreet, can take up to 28 days — apply early) + business registration documents

### A.7 Mandatory Closed Testing (applies to all personal accounts created after 13 Nov 2023)
- [ ] Set up a **Closed Testing** track in Play Console
- [ ] Recruit **at least 12 opted-in testers** (real Google accounts, real devices — emulators/bots don't count)
- [ ] Maintain 12+ active testers continuously for **14 consecutive days**
- [ ] Note: dropping below 12 testers at any point resets the 14-day window
- [ ] Only after this passes can you apply for **Production access**

---

## Part B — Upcoming: Android Developer Verification (Not a Play requirement yet)

Separate from Play Store publishing — a device-level check for identity-verifying Android developers, including those sideloading outside Play.

- [ ] **Not required for India yet.** Enforcement starts **30 Sept 2026** in Brazil, Indonesia, Singapore, Thailand only.
- [ ] Global rollout (including India) expected in **2027** — track this if you plan to distribute APKs directly outside Play in the future.

---

## Part C — App-Level Requirements Before Publishing

### C.1 Technical Compliance
- [ ] App targets a current Android **API level** per Play's target level policy (checked at upload)
- [ ] App signed via **Play App Signing** (enroll during first release)
- [ ] Sensitive permissions (SMS, Call Log, Accessibility, etc.) declared with justification, if used

### C.2 Store Listing
- [ ] App title, short description, full description
- [ ] App icon
- [ ] Feature graphic
- [ ] Phone screenshots (minimum required set)
- [ ] Tablet screenshots, if supporting tablets

### C.3 Content & Policy Declarations
- [ ] Content rating questionnaire completed
- [ ] **Data Safety** section — must accurately reflect all data collected/shared (align this with your actual Firestore/Cloudinary/FCM data flows)
- [ ] Ads declaration (whether app shows ads)
- [ ] Target audience & content declaration
- [ ] Government app declaration (if applicable)
- [ ] News app declaration (if applicable)

### C.4 Privacy & Legal
- [ ] **Privacy Policy URL** — mandatory if app requests any permission or collects personal data (almost always required)
- [ ] Terms of Service, if applicable to your app's use case

### C.5 Reviewer Access
- [ ] **App access instructions** for reviewers — demo credentials or a documented path to test login-gated/admin-gated features, since this app has role-based login. Reviewers cannot test what they can't access.

### C.6 User Data Controls (Play policy requirement)
- [ ] **Account/data deletion** flow implemented and linked in Play Console, required whenever the app supports account creation

---

## Quick Order of Operations

1. Enable 2-Step Verification on your Google account
2. Prepare ID + address proof (verify name/address consistency first)
3. Register developer account, link payments profile, pay $25
4. Complete identity verification
5. Build app, complete store listing + all policy declarations
6. Set up Closed Testing, recruit 12 testers, run for 14 consecutive days
7. Apply for Production access
8. Publish
