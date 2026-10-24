# QuantaScripts
React + Vite + Tailwind CSS + Radix UI + Lucide + Recharts, with Supabase for login and data.

1. Create a Supabase project and run `schema.sql` in SQL Editor.
   (Already ran an earlier version? Run only `schema_update.sql`.)
2. `cp .env.example .env.local` and add your project URL and anon key.
3. `npm install` then `npm run dev`, or `npm run build` and deploy `dist/`.
4. In Supabase, turn off **Authentication → Sign In / Providers → Email → Confirm email**.
   Staff sign in with a username; the app stores it as `username@staff.quantascripts.invalid`, an address that can't receive mail.
5. Sign up, then make yourself admin: `update public.profiles set role = 'admin' where email = 'yourusername@staff.quantascripts.invalid';`
   There's no email, so there's no "forgot password". Reset a password in Supabase under **Authentication → Users**.

Desktop app (Electron):
- `npm run electron:dev` runs Vite and opens the app in an Electron window with hot reload.
- `npm run electron:start` builds and opens the production build in Electron.
- `npm run electron:build` makes a Windows installer in `release/`.
The Supabase keys in `.env.local` are baked in at build time, so set them before building.

Releasing an update (installed apps update themselves from github.com/Jerryzxt/quantascripts releases):
1. Raise `"version"` in package.json (e.g. 1.3.0 → 1.4.0).
2. In PowerShell: `$env:GH_TOKEN = "<your token>"` then `powershell -ExecutionPolicy Bypass -File .\release.ps1`.
   The token is a GitHub fine-grained token with Contents: Read and write on that repo only.
3. Open apps find it within 4 hours (or on next launch), download it, and offer "Restart now".

Admin: Overview (sales, expenses, profit split), Products, Team approvals.
Everyone: Chat, Earnings (staff see only their own), Notes, Ideas.
