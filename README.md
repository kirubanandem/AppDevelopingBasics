# Android Application — Master Planning Checklist

A consolidated, ordered reference covering all modules, systems, and concerns required to plan a production-grade Android application for a real user base — from foundational infrastructure through release engineering and ongoing operations.

---

## 1. Core Infrastructure & Data Layer

### 1.1 Data Storage (Firebase / Firestore)
- Firestore database structure — collections, subcollections, denormalization strategy
- Security rules (role-based, field-level where needed)
- Composite indexes for all compound queries
- Firebase Hosting configured for deeplink domain (`assetlinks.json` / App Links verification)
- Separate Firebase projects for **dev / staging / production** (never share one project across environments)
- Firestore schema migration strategy — how the data model evolves without breaking older app versions
- Firebase usage & billing alerts (reads/writes/storage quota thresholds)

### 1.2 Media Storage
- Image/file uploading via API (e.g., Cloudinary)
- API credentials stored server-side (Firestore/Remote Config), **never** shipped in the APK — proxy uploads through Cloud Functions to avoid exposing keys client-side
- Media compression/resizing before upload
- Cloudinary (or equivalent) bandwidth/storage usage alerts

### 1.3 Offline & Sync
- Offline-first support — local cache (Room DB) with sync queue
- Conflict resolution strategy for offline edits vs. server state
- Network state handling — retry logic, offline banners/indicators
- Background sync via WorkManager (periodic jobs, cleanup tasks)

---

## 2. Authentication & Access Control

### 2.1 Login & Registration
- Login / registration flows (email, phone/OTP, social sign-in as needed)
- Session/token expiry and refresh handling
- Force logout from other devices (single-session enforcement, if required)
- Biometric or 2FA login option
- Rate limiting / abuse prevention on OTP and login attempts

### 2.2 Roles & Rights
- Role-based access control — implemented via **Firebase Auth custom claims**, not only Firestore rules (custom claims are needed for rule-level enforcement and to avoid client-trust issues)
- Admin console & Super Admin console with full user management
- Login / app-resume checks — validate session, role, rights, pending notifications and alerts via FCM on every resume

### 2.3 Profile
- Profile setup and edit flow
- Account/data deletion flow, user-initiated (required by Play Store policy when account creation exists)

---

## 3. Notifications & Communication

### 3.1 Alerts & Notifications
- Push notifications via FCM
- Notification channels (Android 8+) with per-user notification preferences
- Silent/data-only pushes for background sync vs. visible user-facing alerts
- Delivery and open-rate tracking

### 3.2 Broadcasting
- User-scoped broadcasting (targeted messages by role/segment/user)

### 3.3 Support
- In-app support chat
- Help & Manuals section (FAQs, guides, contextual help)
- In-app feedback / rating prompt

---

## 4. Navigation & Linking

- Deeplink URL handling (App Links, verified via Firebase Hosting `assetlinks.json`)
- App shortcuts / widgets, where relevant to the app's use case

---

## 5. Data Management

### 5.1 Import / Export
- Data import via CSV
- Reporting & exporting (PDF/CSV/Excel outputs as needed)

### 5.2 Backup & Compliance
- Backup of user data (scheduled + on-demand)
- User-initiated data export request (GDPR-style "download my data")
- Audit log — track key actions (admin changes, sensitive data edits, logins)

### 5.3 Legal
- Privacy Policy and Terms of Service, with a re-consent flow triggered when either is updated
- Accurate Play Store "Data Safety" section matching actual data practices

---

## 6. App Lifecycle Management

### 6.1 Version & Maintenance
- Version check and forced/optional update flow
- Maintenance mode, AMC (Annual Maintenance Contract) handling, and Grace Period logic for continued app usage
- Feature flags / A-B testing via Firebase Remote Config, decoupled from app version releases

### 6.2 Developer & Distribution
- Developer/publisher app store presence and listing management
- Staged rollout strategy — internal testing → closed testing → open testing → production
- CI/CD pipeline with code signing automation

---

## 7. Reliability & Monitoring

- Crash reporting (Firebase Crashlytics)
- Performance monitoring
- Centralized error/exception logging (separate from the audit log — this is technical/system logging, audit log is user-action logging)

---

## 8. User Experience

- Onboarding / tutorial flow for first-time users
- Search functionality across relevant app data
- Dark mode / theme support
- Localization and RTL support, if multi-region
- Accessibility support (TalkBack, content descriptions, contrast)

---

## 9. Monetization (if applicable)

- Google Play Billing integration
- Subscription/renewal handling
- Server-side receipt validation

---

## 10. Security (Cross-Cutting)

- Root/tamper detection (Play Integrity API) for sensitive apps
- API key and secret protection — no credentials in client code
- Rate limiting on sensitive endpoints
- Rules review — Firestore/Storage rules audited alongside custom claims, not treated as the only access control layer

---

## Quick Reference — Full Sorted List

| # | Item | Category |
|---|------|----------|
| 1 | Version check & update options | Lifecycle |
| 2 | Login / Registration | Auth |
| 3 | Session/token expiry & refresh, force logout other devices | Auth |
| 4 | Biometric / 2FA login | Auth |
| 5 | Rate limiting on login/OTP | Security |
| 6 | Admin console & Super Admin console with user management | Auth/Access |
| 7 | Role-based access control via Firebase custom claims | Auth/Access |
| 8 | Login/resume checks — session, rights, notifications via FCM | Auth/Access |
| 9 | Profile setup | Profile |
| 10 | Account/data deletion (user-initiated) | Compliance |
| 11 | Support chat | Communication |
| 12 | Help & Manuals | Communication |
| 13 | In-app feedback/rating prompt | UX |
| 14 | Alerts & notifications via FCM | Communication |
| 15 | Notification channels & preferences | Communication |
| 16 | Silent/data-only push for background sync | Communication |
| 17 | Notification delivery/open-rate tracking | Communication |
| 18 | User-scoped broadcasting | Communication |
| 19 | Deeplink URL handling | Navigation |
| 20 | App shortcuts/widgets | Navigation |
| 21 | Data import by CSV | Data |
| 22 | Reporting & exporting | Data |
| 23 | Backup user data | Data |
| 24 | User data export request (GDPR-style) | Compliance |
| 25 | Audit log | Data |
| 26 | Privacy Policy & Terms, with re-consent flow | Legal |
| 27 | Play Store Data Safety accuracy | Legal |
| 28 | Maintenance, AMC & Grace Period | Lifecycle |
| 29 | Remote Config feature flags / A-B testing | Lifecycle |
| 30 | Developer app store presence | Lifecycle |
| 31 | Staged rollout (internal/closed/open/prod) | Lifecycle |
| 32 | CI/CD pipeline with code signing | Lifecycle |
| 33 | Firestore data storage, rules, indexes, hosting for deeplink | Infrastructure |
| 34 | Separate dev/staging/prod Firebase projects | Infrastructure |
| 35 | Firestore schema migration strategy | Infrastructure |
| 36 | Firebase usage & billing alerts | Infrastructure |
| 37 | Image uploading via Cloudinary API, keys stored server-side | Infrastructure |
| 38 | Cloudinary usage/bandwidth alerts | Infrastructure |
| 39 | Offline-first support (Room DB, sync queue, conflict resolution) | Reliability |
| 40 | Network state handling, retries, offline banners | Reliability |
| 41 | Background sync via WorkManager | Reliability |
| 42 | Crash reporting (Crashlytics) | Reliability |
| 43 | Performance monitoring | Reliability |
| 44 | Centralized error/exception logging | Reliability |
| 45 | Onboarding/tutorial flow | UX |
| 46 | Search functionality | UX |
| 47 | Dark mode / theme support | UX |
| 48 | Localization / RTL support | UX |
| 49 | Accessibility support | UX |
| 50 | Google Play Billing, subscriptions, receipt validation | Monetization |
| 51 | Root/tamper detection (Play Integrity API) | Security |
| 52 | API key/secret protection, server-side proxying | Security |

---

## Notes on Interactions Between Items

- **Item 6 (Admin console)** and **Item 7 (custom claims)** should be designed together — Firestore rules alone (Item 33) cannot securely enforce roles without custom claims backing them.
- **Item 18 (login/resume checks)** naturally depends on Items 3, 8, and 14 — session validity, rights, and pending alerts should all be checked in a single resume-time routine.
- **Item 37 (Cloudinary uploads)** should route through a Cloud Function rather than calling the API directly from the app, so keys never live in client code (ties to Item 52).
- **Item 28 (Maintenance/AMC/Grace Period)** pairs with Item 1 (version check) — both are typically served from the same remote "app status" config document.
