# Supabase heartbeat (GitHub Actions)

This repository runs a read-only Supabase REST check at 07:00, 13:00 and 19:00 West Africa Time (WAT), plus manual runs from the Actions tab.

## Required repository secrets

Open **Settings → Secrets and variables → Actions → New repository secret** and add:

- `SUPABASE_URL`: `https://rtbohylgtwcenswdybuv.supabase.co`
- `SUPABASE_ANON_KEY`: the project's publishable key (or legacy anon key) from Supabase **Project Settings → API**.

Do not add a service-role key. Do not put keys in source files or commit them.

## Run and inspect

Open **Actions → Supabase heartbeat → Run workflow** to test immediately. The scheduled runs appear on the same page. A red run means the endpoint, key, network, or table permissions need attention.

## Important limitation

This workflow checks availability; it does not wake a paused project and cannot guarantee that Supabase will never pause a Free project. Supabase's inactivity-pause policy may not count simple REST reads as qualifying activity. If the project pauses, restore it in Supabase. Consider a paid plan or an appropriate supported uptime option for guaranteed continuity.

The workflow uses a public/publishable key and performs only a limited read of published rows. RLS must permit anonymous SELECT of published content. Never use a service-role key for this job.
