# PadelRanks — Privacy Policy

**Effective date:** 22 May 2026
**Provider:** PadelRanks — Juliancilea@gmail.com

PadelRanks is an iOS and Android app that gives padel players access to national federation rankings, international pro rankings, tournaments, club information and a Danish "Find a Match" community. The app's federation-backed ranking and tournament data covers **18 countries**:

- **Rankedin-backed (13):** Denmark, Sweden, Germany, Austria, Croatia, Norway, Romania, Slovenia, Moldova, Hungary, Finland, Ukraine, Estonia.
- **FIP-backed (5):** Spain, Mexico, Argentina, Italy, France.

For Denmark specifically, the underlying ranking data is owned and maintained by the **Dansk Padel Forbund (DPF)** — the Danish Padel Federation — and hosted on the Rankedin platform. We access this data through Rankedin's public API but the data controller for the ranking records themselves is DPF, not Rankedin or us.

In addition, an **optional Playtomic Liga mode** in the Tournaments tab lets you switch to amateur club-tournament listings from Playtomic, covering **60+ additional countries** (you toggle this manually from "Choose Liga"; the default is Rankedin/FIP).

We take your privacy seriously and only process the data strictly required for the app to function.

## 1. Data we process

### 1.1 Location data
If you grant permission, PadelRanks uses your location **on your device** to calculate the distance between you and padel tournaments / clubs, and to verify that you are physically located in Denmark when you sign in to the Find a Match feature (see §1.6). Your location is never sent to our own servers as a stored record. Outgoing requests to third-party tournament providers (see §3) only include coordinates when you explicitly run a location-based search — and only as anonymous latitude/longitude, never your identity. If you deny the location permission, the rankings and tournament parts of the app still work — distance simply isn't shown — but the Find a Match feature is unavailable because we cannot confirm you are in Denmark.

### 1.2 No federation login
The rankings, tournament and club parts of PadelRanks are entirely read-only and require no Rankedin or FIP account. You can browse all 18 countries without signing in to anything. We do not store federation credentials and there is no login form for Rankedin or FIP in the app.

You can optionally "claim" your own player profile by searching for your name in the Rankedin or FIP public player database — this selection is stored only on your device and contains no credentials.

### 1.3 Third-party API data (rankings, tournaments, clubs, profiles)
The app fetches data from the public APIs listed in §3 to display rankings, tournament results and club information. This data is stored only temporarily in the app's on-device cache (AsyncStorage) to make the app faster; it is never forwarded anywhere.

### 1.4 Player profile photos displayed in the app
Profile photos of other players shown in rankings and profile screens are sourced from the public APIs of Rankedin and the International Padel Federation (FIP) — they are not hosted by us. Photo availability varies by player and by country; where a photo is not available we display a generated avatar with the player's initials. The image URLs themselves are requested directly from the third-party CDN by your device and are cached on-device for performance; no personal identifier is attached to those requests.

### 1.5 Find a Match account and content (Apple / Google sign-in, posts, comments)
The "Find a Match" feature requires you to sign in with Apple or Google. When you do, PadelRanks receives and stores the following on our backend (Supabase — see §3):

- A **Supabase user id** (random UUID) — used to identify your account.
- The **email address** returned by Apple or Google. Apple users may choose to share a relay email instead of their real address; we accept whichever form Apple returns.
- Your **chosen display name** — the name shown on your posts. You set this on first sign-in. You can edit it later.
- Your **chosen Danish postal code** — used to scope which posts you see and to attach a postcode to posts you create.
- The **content of any post or comment you create** — the message text, your selected level range, your match date, the number of players you need, and the optional time text.
- Your **"I'm in" joins** on other users' posts.
- A **rough one-time location check** at sign-in confirming you are in Denmark. We do not store your exact GPS coordinates — only the boolean result of the country check is associated with your account, and only at sign-in time.

We do **not** receive or store your Apple or Google password — the sign-in itself happens on Apple's / Google's servers, and we only receive the resulting identity token.

The Find a Match feature is currently restricted to users physically located in Denmark.

### 1.6 Push notifications (optional)
If you opt in to notifications, we collect:

- An **Expo push token** — an opaque per-device identifier issued by Expo's push service. We store it in our Supabase backend together with your current notification preferences (mode, postal code, level window) so the server can deliver notifications when the app is closed. The Expo push token is used **only** for the Find a Match feature (§1.5).
- The token is bound to your account; you can revoke it by signing out, switching off notifications in the app's bell-icon sheet, or revoking permission in the OS settings.

Push delivery for Find a Match is fanned out via Expo's push service to Apple's APNs and Google's FCM. Expo doesn't see the message content beyond what we send (notification title + body). We don't share the push token with anyone else.

#### 1.6.1 Notifications about players you follow (local, on-device)
Separately from the Expo push token above, if you have followed any player(s) and have OS-level notification permission granted, PadelRanks may send you **local push notifications about that player's competitive activity**:

- **Pre-match reminders** — 24 hours and 2 hours before the start of a tournament a followed Rankedin-backed player is registered in.
- **Post-match results** — once a followed player's match result is published by the federation (score, opponent, tournament).
- **Rank-change notifications** — when a followed player's national or world ranking position has moved meaningfully (≥3 positions or across a top-10/25/50/100/250/500/1000 milestone).

These notifications are **generated locally on your device** by a 30-minute polling task that reads the same public federation APIs the rest of the app uses (Rankedin's `GetLastEventsPlayedAsync` and `/matchlist` endpoints, FIP's `/wp-json/fip/v1/circuit-stats` endpoint, and FIP's live-results widget — see §3.1). The list of players you follow, the dedup state and the per-player mute toggles are **stored only on your device** (AsyncStorage); we do not send the list of who you follow to our own servers, and the anonymous follower-count rows in §1.7 are aggregate-only and separate from this notification path.

You can mute notifications **per followed player** from the in-app notifications screen, switch off the category entirely from the settings sheet, or revoke notification permission at the OS level.

**If you are a player whose name may appear in these notifications:** the data behind the notifications is federation-published material already publicly displayed on `rankedin.com`, `padelfip.com` and `matchscorerlive.com`. If you would nonetheless prefer that your name not be surfaced via PadelRanks notifications, you can request removal by writing to **Juliancilea@gmail.com** (see §5 — Right to object).

### 1.7 Follower counts (anonymous)
PadelRanks shows a small follower count next to each player in the rankings, search results, player profile and "Following" list — a number indicating how many other PadelRanks users follow that player. To compute this count we store one row per follow on our backend (Supabase — see §3) with:

- The **player id** being followed (an opaque identifier from the federation: Rankedin or FIP).
- An **anonymous device identifier** — a random UUID v4 generated on your device on first launch and persisted locally. It is **not derived from your name, email, Apple ID, Google ID, location, IP address or any other personal information**. It exists only so the same device cannot inflate a player's count and so you can unfollow later.
- A **timestamp** of when the follow was created.

The anonymous device identifier is **never returned to any client** — only the aggregate count (e.g. "134 followers") is visible to other users, and is the only value the server's public API ever emits. Row-level security blocks any direct read of the underlying table.

If you uninstall and reinstall the app your device receives a new anonymous identifier; your previous follows orphan in the database and continue to contribute to counts until removed (see §5 Erasure).

The follower-count feature works for both Rankedin- and FIP-backed players across all 18 countries and does not require sign-in.

### 1.8 Legal basis for processing (GDPR Article 6)

The lawful bases under GDPR Article 6(1) that we rely on are:

- **Federation rankings, tournament results and public player profiles** — Article 6(1)(f) **legitimate interests.** Our legitimate interest is to make padel rankings, tournament results and federation-published player profiles searchable in a single mobile app for the Danish and international padel community. We have weighed this interest against the rights of the data subjects: the source data is already published by the national federations (DPF, FIP) and their hosting platforms (Rankedin, padelfip.com) on publicly accessible web pages; players who register with these federations are informed by the federations that their rankings will be public; and the data we surface is limited to what those federations themselves display. You can object to this processing at any time by writing to the contact email below — see §5 (Right to object / erasure).
- **Find a Match account, posts, comments and "I'm in" joins** — Article 6(1)(b) **performance of a contract.** When you sign in via Apple or Google to use Find a Match, you create an account with us and we process your account record, your posts and your interactions in order to provide that service to you.
- **Push notifications (Find a Match, §1.6)** — Article 6(1)(a) **consent.** Push delivery for Find a Match notifications only happens after you have explicitly opted in via the in-app notification settings. You can withdraw this consent at any time by switching off notifications.
- **Followed-player notifications (§1.6.1)** — Article 6(1)(a) **consent** for delivery to you (you opt in by both granting OS-level notification permission and explicitly following a player), and Article 6(1)(f) **legitimate interests** for the processing of the third-party player's federation-published data used to compose the notification. Our legitimate interest is to let users of a padel app keep track of the competitive activity of players they care about — a feature widely expected in sports apps. We have weighed this interest against the rights of the data subjects: the underlying data is federation-published material already on public display at `rankedin.com`, `padelfip.com` and `matchscorerlive.com`; PadelRanks does not republish, sell or share that data; the notification is generated on the user's own device by a local polling task; the list of followed players is stored only on the user's device, not on our backend; and any player whose name appears in such notifications can request removal by contacting us (see §5). We recognise that this basis is more constrained for amateur (non-public-figure) players than for professional players whose competition schedules are publicly published — see §9 (Changes) for the direction of travel on this point.
- **Location-based distance / Denmark presence check** — Article 6(1)(a) **consent.** Location is only accessed after you have granted the OS-level permission. The Denmark presence check at Find a Match sign-in stores only the boolean result, never your coordinates.
- **Follower counts (anonymous)** — Article 6(1)(f) **legitimate interests.** Our legitimate interest is to give padel players a lightweight social signal (how many other users in the community follow each player) — a feature widely expected in modern sports apps. We have weighed this interest against the rights of the data subjects: the device identifier is anonymous and not derivable from any PII; the underlying table is invisible to clients (only aggregate counts are exposed, via a SECURITY DEFINER RPC); follow events do not target identified natural persons (they reference public federation player IDs that we do not own); and you can request deletion of your device's follow records at any time — see §5.
- **Security, abuse-prevention and account-deletion auditing** — Article 6(1)(f) **legitimate interests** (preventing abuse of the Find a Match feature, retaining minimal logs to respond to deletion requests).

A documented legitimate-interest balancing test is available on request to **Juliancilea@gmail.com**.

## 2. Data we do **not** collect

- We have no analytics (no Google Analytics, Firebase, Facebook SDK, Mixpanel, etc.).
- We show no ads.
- We do not sell or share data with any third party.
- We do not track you across apps or websites.
- Outside of the optional Find a Match sign-in, we do not require an account to use the app.

## 3. Third-party data sources and processors

PadelRanks communicates with the following services. When you use the app, requests are sent directly from your device — not through any server we operate, except for Supabase (see below).

### 3.1 Read-only data sources (rankings, tournaments, clubs)
- **Dansk Padel Forbund (DPF)** — the Danish Padel Federation. DPF is the **controller** of the Danish ranking records, tournament results and player registrations we display for Denmark. The data is published by DPF on the Rankedin platform (see next bullet). DPF website: https://dansk-padel.dk
- **Rankedin** — Rankedin is DPF's technology provider and also hosts national rankings, tournaments and player profiles for the other 12 Rankedin-backed countries listed in the introduction. We read via the public endpoints on `api.rankedin.com` and the Azure Front Door CDN that serves profile thumbnails (`rankedin-prod-cdn-adavg8d3dwfegkbd.z01.azurefd.net`). Rankedin privacy policy: https://www.rankedin.com/privacy
- **FIP (Federación Internacional de Pádel)** — global pro rankings, international tournament calendar and player profile pages for Spain, Mexico, Argentina, Italy and France. FIP is the **controller** of these records. We access FIP data via a combination of (1) FIP's public WordPress REST API at `padelfip.com/wp-json/fip/v1/...` (including the `circuit-stats` endpoint that exposes recent finals per player), (2) FIP's own live-scoring widget (see Crionet entry below), and (3) lightweight HTML scraping of FIP's public player profile pages at `padelfip.com/player/{slug}/` for fields that aren't exposed by the REST API. We only read endpoints that are publicly accessible without authentication. FIP privacy policy: https://www.padelfip.com/privacy
- **Crionet S.p.A. (matchscorerlive.com)** — FIP's live-score widget provider. Used to display in-progress and recently-completed match scores during FIP tournaments. PadelRanks reads results from the widget endpoint by anonymous public GET requests — practically this is HTML scraping of a public live-results page, no API key or user identity is required, and no user data leaves your device. The scraped data is the same competitor names + scores that the widget displays publicly on padelfip.com. Operator: Crionet S.p.A. (Italy).
- **Playtomic** — amateur club-tournament discovery covering **60+ countries** worldwide. Used **only** when you opt in by switching the Tournaments tab to "Playtomic" mode from the "Choose Liga" picker. The app queries Playtomic's public `api.playtomic.io/v1/tournaments` endpoint with the coordinates you (optionally) provide for distance sorting — no account or identity is sent. Playtomic privacy policy: https://playtomic.io/privacy

Profile photos specifically come from:
- Rankedin's Azure Front Door CDN (`rankedin-prod-cdn-adavg8d3dwfegkbd.z01.azurefd.net/images/upload/player/{id}thumb.png`) for the 13 Rankedin-backed countries;
- FIP's WordPress Media library (`padelfip.com/wp-content/uploads/...`) for the 5 FIP-backed countries.

### 3.2 Backend / data processor (Find a Match feature only)
- **Supabase** (Supabase Inc., hosted in Frankfurt, Germany — EU region) acts as our **data processor** for the Find a Match feature **and for anonymous follower-count tracking (§1.7)**. Supabase stores your account record, posts, comments, "I'm in" joins, push subscription and the anonymous follow rows inside a Postgres database hosted in the EU and is contractually bound by GDPR-compliant data-processing terms. Supabase privacy policy: https://supabase.com/privacy
- **Apple Sign-In** (Apple Inc.) — only used for authentication. Apple's privacy policy: https://www.apple.com/legal/privacy/
- **Google Sign-In** (Google LLC) — only used for authentication. Google's privacy policy: https://policies.google.com/privacy
- **Expo Push Service** (650 Industries, Inc.) — delivers push notifications to APNs / FCM on our behalf. Expo privacy policy: https://expo.dev/privacy

We do not run our own application servers. All Find a Match data lives in Supabase; all read-only padel data lives at the third-party providers listed above.

No crash reporting, analytics or telemetry SDK is currently integrated into the app. Should we later enable crash reporting (via Sentry), only anonymised technical details (stack trace, device model, OS version) would be sent — never personal data, location or credentials — and this section of the policy will be updated before such a change takes effect.

## 4. Retention

- **On-device cache** (rankings, tournaments, clubs, photos): cleared on uninstall, or whenever the app's normal cache-eviction logic decides. You can also clear it by reinstalling.
- **Find a Match posts and comments**: each post automatically expires **7 days** after it is created and is deleted from the database. Comments and "I'm in" joins on a post are deleted together with the post.
- **Find a Match account record** (display name, postal code, user id, email, push token): retained until you delete your account (see §5).
- **Follower-tracking rows** (anonymous device id + player id + timestamp): retained indefinitely so global follower counts remain stable across sessions. You can request deletion of your device's follow records — see §5 (Erasure).

## 5. Your rights (GDPR + UK GDPR + Swiss DPA)

You have the following rights under the GDPR. Article references are to the EU GDPR; equivalent rights exist under the UK GDPR and Swiss DPA.

- **Access** — Article 15. For the on-device parts of the app, all your data lives on your device. For the Find a Match feature, write to Juliancilea@gmail.com and we will provide a copy of the data associated with your account.
- **Rectification** — Article 16. You can edit your display name and postal code in the app at any time.
- **Erasure ("right to be forgotten")** — Article 17.
  - **On-device data:** uninstall the app and all local data is wiped.
  - **Find a Match account and content:** you can delete your account and all posts/comments inside the app (Find a Match → bell icon → "Delete account"), or by writing to Juliancilea@gmail.com. Deletion is final — your Find a Match user record, posts, comments, "I'm in" joins and push subscription are removed from Supabase, as is the corresponding entry in `auth.audit_log_entries`.
  - **Removal of your public player profile:** PadelRanks displays read-only data published by the federations themselves (DPF / Rankedin / FIP / Playtomic). We do not store or republish that data — we fetch it live from their public APIs. To have your player profile removed from PadelRanks you must request deletion at the source: contact Rankedin (`info@rankedin.no`) or your national federation directly. Once the federation deletes your record, PadelRanks stops returning it on the next data refresh (≤ 7 days depending on the cached endpoint, or immediately on pull-to-refresh).
  - **Anonymous follower records (§1.7):** because the device identifier is not tied to any personal account, the in-app path is to unfollow individual players (each unfollow removes the corresponding row immediately). To delete ALL follow records originating from your device, write to **Juliancilea@gmail.com** and include your anonymous device id from Settings → Privacy → "Your anonymous device id". We will delete the matching rows from Supabase within 30 days of receipt.
- **Restriction** — Article 18. You can ask us to restrict processing of your Find a Match account while a dispute is investigated.
- **Portability** — Article 20. You can export your Rankedin data directly from rankedin.com. For Find a Match data, write to Juliancilea@gmail.com for a JSON export.
- **Object** — Article 21. You can object at any time to our processing of your data on the basis of legitimate interests (§1.8). For PadelRanks-side processing (your Find a Match account or anonymous follower-tracking rows), write to Juliancilea@gmail.com. For federation-published data we surface, see the "Removal of your public player profile" point above — the federations are the source controllers.
- **Withdraw consent** — Article 7(3). You can sign out of the Find a Match feature at any time from the bell-icon settings sheet. You can also revoke Apple / Google's authorisation in your Apple ID / Google Account settings. Switching off notifications in-app revokes your push consent.
- **Complaint** — Article 77. You can file a complaint with your national Data Protection Authority (e.g. Datatilsynet in Denmark, IMY in Sweden, BfDI in Germany, DSB in Austria, AEPD in Spain, Garante in Italy, CNIL in France, ICO in the UK) if you believe your rights have been infringed.

## 6. Children (GDPR Article 8)

PadelRanks's **Find a Match** feature is **not directed at and may not be used by children under the age of 16**. At Find a Match sign-up we require an explicit in-app confirmation that the user is 16 years of age or older. This is higher than the Danish digital-consent age of 13 (GDPR Article 8(1)) and is set deliberately to avoid processing the personal data of younger users without parental consent. Apple's and Google's sign-in flows additionally enforce platform-level minimum age requirements.

We do not knowingly collect data from children under 16 via Find a Match. If you believe a child under 16 has created a Find a Match account, please contact us at Juliancilea@gmail.com and we will delete the account and associated content.

The **non-Find-a-Match parts** of the app (rankings, tournaments, clubs) do not collect any personal data from any user, of any age — they are a read-only display of data already published by the national padel federations (DPF, FIP, etc.) on their own public web pages. The federations are the controllers of that data and are responsible for any age-related publication decisions about their members.

## 7. Security

Communication with all third-party APIs and with Supabase is encrypted with TLS. Find a Match data inside Supabase is protected by row-level security (RLS) — you can only read and write your own posts, comments, joins and push subscriptions, and the database refuses any operation that violates this. Follower-tracking rows (§1.7) are protected by the same row-level security mechanism — the underlying table is fully blocked from direct client reads, and only the aggregate count is exposed via a SECURITY DEFINER RPC, so no client (including signed-in users) can enumerate which devices follow which players. We rely on Supabase's underlying security measures (encryption at rest, secure key management, regular backups) for the database itself.

## 8. International transfers

Supabase hosts the Find a Match database in **Frankfurt, Germany** — inside the EU. Apple, Google and Expo may process authentication and push-delivery data outside the EU under their own GDPR-compliant transfer mechanisms.

## 9. Changes

Changes to this policy will be published on this page together with an updated effective date. Material changes (e.g. new categories of data, new processors) will be announced in the app before they take effect.

**Planned narrowing of followed-player notifications (§1.6.1).** In a future release we intend to scope the pre-match, post-match and rank-change notification path so that it covers (a) the user's **own** federation profile (where the user has linked it via the Apple/Google sign-in) and (b) **FIP-listed professional players**, whose competition schedules are publicly published by Premier Padel. The anonymous follower-count feature (§1.7) and the in-app "Following" bookmark list are unaffected by this planned change. This policy will be updated again before the change takes effect.

## 10. Contact

Questions, deletion requests, or data exports? Write to **Juliancilea@gmail.com**.
