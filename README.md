# AP SYSTEM prototype

A mobile-first Solo Leveling-inspired workout quest tracker.

## What's working in this prototype
- Dark electric-blue System-style UI
- Four-day rotating mixed training plan (strength, legs/core, cardio, full body)
- Tap-to-complete daily exercise quests and 25 XP per task
- Daily quest completion grants 100 XP and records history
- Levels, E-to-S-style ranks, streaks and STR/END/CON attributes
- Progression review after 7 calendar days when at least 3 sessions have been completed in the recent week
- Local persistence in browser localStorage
- Export progress to JSON
- Basic installable-web-app shell and service-worker cache

## Important prototype limitations
The email/password screen is **demo-only**. It does not authenticate an email, securely store a password, or sync across devices. It uses the email as a local profile key and stores progress only in that browser/device. Do not enter a real password. To make this production-ready, configure Supabase Auth with email/password, create a `profiles` and `workout_history` schema, enable Row Level Security, and store each user's records keyed to `auth.uid()`. Never put a Supabase service-role key in frontend code.

The progression logic is a prototype, not medical guidance. The current example progression tier changes after the app has seen at least 3 completed sessions within the recent week and the user is at least 7 days into the plan. Before real use, add explicit deload/recovery handling, injury/pain guidance, and more robust date/timezone logic. Exercise choices and reps should be adapted to the user's current capacity and available weights.

## Deploy at no recurring cost (subject to provider limits)
1. Create a free GitHub account/repository, or use another static hosting provider.
2. Upload `index.html`, `manifest.json`, and `sw.js` to the repository.
3. Enable GitHub Pages for the repository (Settings -> Pages -> deploy from branch), or deploy the folder to another free static host. The app must be served over HTTPS for service workers and installable web-app behavior.
4. Open the HTTPS URL in Safari on iPhone. Tap Share -> Add to Home Screen -> enable Open as Web App -> Add.
5. Test quest completion, close/reopen, history, JSON export, and resetting progress.

## Add real email login and cloud sync
1. Create a Supabase project on the free tier. Check current quotas and inactivity-pausing rules before relying on it.
2. Enable email/password authentication and set the site's allowed redirect URLs to the deployed HTTPS domain.
3. Create user-scoped tables for profiles and workout history. Enable Row Level Security and policies that limit each user to their own rows.
4. Replace the demo login and local save/load functions with Supabase Auth and database calls. Keep public/anon keys in client config only with correct RLS; never expose a service-role key.
5. Test sign-up, email verification, password reset, logout, account switching, and cross-device history.
6. For production, add an accessible privacy policy and a way to export/delete account data.

Supabase free projects currently have usage limits and can pause after inactivity; this means “free” is not the same as a guaranteed always-on service.
