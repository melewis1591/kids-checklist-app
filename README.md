# Morning Missions — setup guide

A free-to-start, private family checklist web app for a parent, Norah (iPad), and Vinny (iPhone). Includes a 7:15 a.m. countdown in Eastern Time, daily resets, task stars, XP, weekday streaks, parent task management, and real-time syncing through Supabase.

## 1. Create a free Supabase project

1. Visit https://supabase.com/dashboard and create an account and new project on the free plan.
2. In **SQL Editor**, create a query, paste all of `database.sql`, and run it **once**. If the tables/policies already exist, do not run the whole script again.
3. Under **Authentication → Providers → Email**, ensure email/password login is enabled. You can turn off public sign-ups after creating your three accounts. Do not use shared personal passwords.
4. Under **Authentication → Users**, use **Add user** to create three accounts (parent, Vinny, Norah) with distinct email addresses and strong passwords. These can be parent-controlled email addresses. If Supabase offers **Auto Confirm User**, use it for these parent-created accounts. Copy the UUID shown for each user. Do not use the Supabase service-role key anywhere in the web app.
5. Return to SQL Editor. In `database.sql`, copy the two seed statements inside the final `/* ... */` block into a NEW query, without the comment delimiters. Replace `PARENT_AUTH_UUID`, `NORAH_AUTH_UUID`, `VINNY_AUTH_UUID` with the three actual UUIDs. Run the seed statements **once**. These create family profiles and the starter tasks.

## 2. Connect the app

1. Go to **Project Settings → API** (sometimes **Connect**) and copy your Project URL and **publishable/anon** key. Never use the `service_role` or secret key.
2. Open `index.html` in a plain-text editor and replace `PASTE_SUPABASE_PROJECT_URL` and `PASTE_SUPABASE_ANON_KEY` with those two values (keep the quote marks).
3. Save the file.

## 3. Publish for free with GitHub Pages

1. Create a free account at https://github.com and create a new **public** repository, e.g. `morning-missions`. Public means the HTML code is visible, **not** your private task data, which is protected by Supabase authentication and row-level security.
2. Upload `index.html` and `manifest.webmanifest` to the repository root. Do **not** upload passwords, UUID seed notes, or private keys.
3. Under **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, and save.
4. Wait a few minutes for the published URL shown on that Pages screen, e.g. `https://YOUR-USERNAME.github.io/morning-missions/`.
5. Open the URL and sign in as the parent. Check that both children's task lists appear. Sign in on each child's device with their own account.

## 4. Add to iPhone / iPad home screens

1. Open the published link in **Safari** on each device.
2. Tap **Share → Add to Home Screen → Add** (depending on iOS version, use **Open as Web App** if offered).
3. Each device stays signed in as its own user. Use a device passcode; avoid sharing account passwords.
4. On the parent's phone, open the same link and sign in as the parent. You will see completion updates when the kids check off tasks. A manual Refresh button is also available.

## 5. Test together

- On Norah's iPad, mark “Wash face” complete. On the parent dashboard, verify it changes to checked.
- On Vinny's iPhone, mark “Get dressed” complete. Verify his progress increases.
- Test unchecking a task, adding a task in parent view, and removing a task.
- Task completion automatically resets when the Eastern Time date changes. Past completion history is kept for streak calculations.

## Important notes

- Free tiers can change, and an inactive Supabase free project may pause. This setup is intended for a small household; check current limits before relying on it.
- No push notifications or direct Alexa integration in version 1. Continue using your existing Alexa routines for reminders.
- Streaks count completed **weekdays**. A missed weekday breaks the streak; weekends are skipped. Today is included once all tasks are complete.
- Parents can view progress and edit tasks; children can only check/uncheck their own tasks. Child accounts should be supervised by the parent.
- The countdown uses the device clock formatted for America/New_York. It is informational, not an alarm.
- Avoid adding sensitive personal information to task names. Never publish passwords or a service-role key.
- The initial setup requires basic copy/paste in Supabase and GitHub; the kids' daily use requires only tapping tasks.
