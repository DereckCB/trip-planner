# Optional: turn on accounts and cloud sync

Out of the box this app is **demo mode**: no login, no network, everything saved in your own
browser under `localStorage['trips_state']`. That is all most people need.

If you want the same board on your laptop and your phone, point it at your own free
[Supabase](https://supabase.com) project - your data, your project, nobody else's.

## 1. Create the tables

In the Supabase SQL editor:

```sql
create table if not exists public.trip_state (
  user_id uuid primary key references auth.users(id) on delete cascade,
  data jsonb not null,
  updated_at timestamptz not null default now()
);
alter table public.trip_state enable row level security;
create policy "own rows" on public.trip_state
  for all using (auth.uid() = user_id) with check (auth.uid() = user_id);

create table if not exists public.trip_snapshots (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  data jsonb not null,
  created_at timestamptz not null default now()
);
alter table public.trip_snapshots enable row level security;
create policy "own snapshots" on public.trip_snapshots
  for all using (auth.uid() = user_id) with check (auth.uid() = user_id);
create index if not exists trip_snapshots_user_ts on public.trip_snapshots (user_id, created_at desc);
```

Row-level security means each account can only ever read and write its own row.

## 2. Add your keys

Near the bottom of `index.html`:

```js
const SUPABASE_URL = 'https://YOUR-PROJECT.supabase.co';
const SUPABASE_KEY = 'your-publishable-anon-key';
```

The publishable key is safe in the file - RLS is what protects the data.

## 3. Reload

The login screen appears. Create an account, and from then on every change is pushed to your
row about two seconds after you stop typing, with a timestamped snapshot on load and every
couple of minutes (Settings -> History restores any of the last 50).

## What you get either way

| | Demo mode | With keys |
|---|---|---|
| Works offline | yes | yes |
| Data in this browser | yes | yes (cache) |
| Same board on another device | no | yes |
| Versioned history | no | yes, last 50 |
| JSON backup / restore | yes | yes |
