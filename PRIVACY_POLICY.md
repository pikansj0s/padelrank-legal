# PadelRank — Privacy Policy

**Effective date:** 10 May 2026
**Provider:** PadelRank — Juliancilea@gmail.com

PadelRank is an iOS and Android app that gives padel players access to national federation rankings, international pro rankings, tournaments, club information and a Danish "Find a match" community. The app currently covers **18 countries**:

- **Rankedin-backed (13):** Denmark, Sweden, Germany, Austria, Croatia, Norway, Romania, Slovenia, Moldova, Hungary, Finland, Ukraine, Estonia.
- **FIP-backed (5):** Spain, Mexico, Argentina, Italy, France.

We take your privacy seriously and only process the data strictly required for the app to function.

## 1. Data we process

### 1.1 Location data
If you grant permission, PadelRank uses your location **on your device** to calculate the distance between you and padel tournaments / clubs, and to verify that you are physically located in Denmark when you sign in to the Community feature (see §1.6). Your location is never sent to our own servers as a stored record. Outgoing requests to third-party tournament providers (see §3) only include coordinates when you explicitly run a location-based search — and only as anonymous latitude/longitude, never your identity. If you deny the location permission, the rankings and tournament parts of the app still work — distance simply isn't shown — but the Community feature is unavailable because we cannot confirm you are in Denmark.

### 1.2 Rankedin credentials (email + password)
If you choose to log in with your rankedin.com account:
- Credentials are sent directly from your device to rankedin.com over encrypted HTTPS.
- They are stored only in iOS Keychain / Android Keystore on your device (if you enable Face ID / fingerprint login).
- We run no servers that receive your Rankedin credentials.
- You can delete them at any time in the app's settings or by uninstalling the app.

PadelRank does not support logging in to FIP accounts — that back-end is used only for public read-only data.

### 1.3 Third-party API data (rankings, tournaments, clubs, profiles)
The app fetches data from the public APIs listed in §3 to display rankings, tournament results and club information. This data is stored only temporarily in the app's on-device cache (AsyncStorage) to make the app faster; it is never forwarded anywhere.

### 1.4 Profile picture (optional)
If you choose to add a profile picture from your camera or photo library, it is stored only locally on your device. The Community feature uses initials-based avatars — your local photo is never uploaded to the Community backend.

### 1.5 Player profile photos displayed in the app
Profile photos of other players shown in rankings and profile screens are sourced from the public APIs of Rankedin and the International Padel Federation (FIP) — they are not hosted by us. Photo availability varies by player and by country; where a photo is not available we display a generated avatar with the player's initials. The image URLs themselves are requested directly from the third-party CDN by your device and are cached on-device for performance; no personal identifier is attached to those requests.

### 1.6 Community account and content (Apple / Google sign-in, posts, comments)
The "Find a match" Community feature requires you to sign in with Apple or Google. When you do, PadelRank receives and stores the following on our backend (Supabase — see §3):

- A **Supabase user id** (random UUID) — used to identify your account.
- The **email address** returned by Apple or Google. Apple users may choose to share a relay email instead of their real address; we accept whichever form Apple returns.
- Your **chosen display name** — the name shown on your posts. You set this on first sign-in. You can edit it later.
- Your **chosen Danish postal code** — used to scope which posts you see and to attach a postcode to posts you create.
- The **content of any post or comment you create** — the message text, your selected level range, your match date, and the optional time text.
- Your **"I'm in" joins** on other users' posts.
- A **rough one-time location check** at sign-in confirming you are in Denmark. We do not store your exact GPS coordinates — only the boolean result of the country check is associated with your account, and only at sign-in time.

We do **not** receive or store your Apple or Google password — the sign-in itself happens on Apple's / Google's servers, and we only receive the resulting identity token.

The Community feature is currently restricted to users physically located in Denmark.

### 1.7 Push notifications (optional)
If you opt in, the app schedules **on-device** notifications for tournaments you follow and for new community posts in your selected postcode. These are local notifications scheduled by the OS — no push token is sent to our servers and no third-party push provider (FCM / APNs cloud, OneSignal, etc.) is involved.

## 2. Data we do **not** collect

- We have no analytics (no Google Analytics, Firebase, Facebook SDK, Mixpanel, etc.).
- We show no ads.
- We do not sell or share data with any third party.
- We do not track you across apps or websites.
- Outside of the optional Community sign-in, we do not require an account to use the app.

## 3. Third-party data sources and processors

PadelRank communicates with the following services. When you use the app, requests are sent directly from your device — not through any server we operate, except for Supabase (see below).

### 3.1 Read-only data sources (rankings, tournaments, clubs)
- **Rankedin** — national rankings, tournaments, player profiles and (optional) user login for the 13 Rankedin-backed countries. Public endpoints on `api.rankedin.com` and the Azure Front Door CDN that serves profile thumbnails (`rankedin-prod-cdn-adavg8d3dwfegkbd.z01.azurefd.net`). Rankedin privacy policy: https://www.rankedin.com/privacy
- **FIP (Federación Internacional de Pádel)** — global pro rankings, international tournament calendar and player profile pages for Spain, Mexico, Argentina, Italy and France. Public WordPress REST API at `padelfip.com/wp-json/fip/v1/...` plus direct HTML scraping of public player pages at `padelfip.com/player/{slug}/`. FIP privacy policy: https://www.padelfip.com/privacy

Profile photos specifically come from:
- Rankedin's Azure Front Door CDN (`rankedin-prod-cdn-adavg8d3dwfegkbd.z01.azurefd.net/images/upload/player/{id}thumb.png`) for the 13 Rankedin-backed countries;
- FIP's WordPress Media library (`padelfip.com/wp-content/uploads/...`) for the 5 FIP-backed countries.

### 3.2 Backend / data processor (Community feature only)
- **Supabase** (Supabase Inc., hosted in Frankfurt, Germany — EU region) acts as our **data processor** for the Community feature. Supabase stores your account record, posts, comments and "I'm in" joins inside a Postgres database hosted in the EU and is contractually bound by GDPR-compliant data-processing terms. Supabase privacy policy: https://supabase.com/privacy
- **Apple Sign-In** (Apple Inc.) — only used for authentication. Apple's privacy policy: https://www.apple.com/legal/privacy/
- **Google Sign-In** (Google LLC) — only used for authentication. Google's privacy policy: https://policies.google.com/privacy

We do not run our own application servers. All Community data lives in Supabase; all read-only padel data lives at the third-party providers listed above.

No crash reporting, analytics or telemetry SDK is currently integrated into the app. Should we later enable crash reporting (via Sentry), only anonymised technical details (stack trace, device model, OS version) would be sent — never personal data, location or credentials — and this section of the policy will be updated before such a change takes effect.

## 4. Retention

- **On-device cache** (rankings, tournaments, clubs, photos): cleared on uninstall, or whenever the app's normal cache-eviction logic decides. You can also clear it by reinstalling.
- **Community posts and comments**: each post automatically expires **7 days** after it is created and is deleted from the database. Comments and "I'm in" joins on a post are deleted together with the post.
- **Community account record** (display name, postal code, user id, email): retained until you delete your account (see §5). Inactive accounts are not auto-purged at this time, but we may introduce inactivity-based deletion in the future and will update this section if we do.

## 5. Your rights (GDPR + UK GDPR + Swiss DPA)

You have the right to:
- **Access** — for the on-device parts of the app, all your data lives on your device. For the Community feature, write to Juliancilea@gmail.com and we will provide a copy of the data associated with your account.
- **Rectification** — you can edit your display name and postal code in the app at any time.
- **Deletion** —
  - On-device data: uninstall the app and all local data is wiped.
  - Community account and content: you can delete your account and all posts/comments inside the app (Community → bell icon → "Delete account"), or by writing to Juliancilea@gmail.com. Deletion is final — your Community user record, posts, comments and "I'm in" joins are removed from Supabase.
- **Portability** — you can export your Rankedin data directly from rankedin.com. For Community data, write to Juliancilea@gmail.com for a JSON export.
- **Withdraw consent** — you can sign out of the Community feature at any time from the bell-icon settings sheet. You can also revoke Apple / Google's authorisation in your Apple ID / Google Account settings.
- **Complaint** — you can file a complaint with your national Data Protection Authority (e.g. Datatilsynet in Denmark, IMY in Sweden, BfDI in Germany, DSB in Austria, AEPD in Spain, Garante in Italy, CNIL in France, ICO in the UK) if you believe your rights have been infringed.

## 6. Children

PadelRank's Community feature is **not directed at and may not be used by children under the age of 13**. Apple and Google sign-in flows enforce minimum age requirements at the operating-system level. We do not knowingly collect data from children under 13. If you believe a child under 13 has created a Community account, please contact us at Juliancilea@gmail.com and we will delete the account and associated content.

The non-Community parts of the app (rankings, tournaments, clubs) do not collect any personal data from any user, of any age.

## 7. Security

Communication with all third-party APIs and with Supabase is encrypted with TLS. Community data inside Supabase is protected by row-level security (RLS) — you can only read and write your own posts, comments and joins, and the database refuses any operation that violates this. We rely on Supabase's underlying security measures (encryption at rest, secure key management, regular backups) for the database itself.

## 8. International transfers

Supabase hosts the Community database in **Frankfurt, Germany** — inside the EU. Apple and Google may process authentication data outside the EU under their own GDPR-compliant transfer mechanisms.

## 9. Changes

Changes to this policy will be published on this page together with an updated effective date. Material changes (e.g. new categories of data, new processors) will be announced in the app before they take effect.

## 10. Contact

Questions, deletion requests, or data exports? Write to **Juliancilea@gmail.com**.
