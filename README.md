# SITARAM EVENT — Admin Dashboard

A separate, responsive English/Gujarati-ready admin workspace for SITARAM EVENT. Built with HTML, CSS, JavaScript and Supabase Auth/Postgres.

## Features

- Secure email/password sign-in with an administrator-role check
- Black-and-gold responsive dashboard
- Live overview counts and recent booking inquiries
- Manage inquiries and update their status
- Create, edit and delete services, events, gallery items and reviews
- Edit JSON site settings
- Supabase Row Level Security remains the authority for every database operation

## Supabase project

The dashboard is configured for the existing SITARAM EVENT Supabase project. The browser uses only the public publishable key. Never put a Supabase secret/service-role key in this repository.

## First administrator setup

1. In Supabase Dashboard → Authentication → Users, create the owner's user with email and password.
2. In Supabase SQL Editor, grant that existing Auth user the admin role. Replace the email below with the exact owner email:

```sql
insert into public.user_roles (user_id, role)
select id, 'admin'
from auth.users
where lower(email) = lower('OWNER_EMAIL_HERE')
on conflict (user_id) do update set role = excluded.role;
```

3. Sign in at the admin site's URL using that email/password.

Do not add an admin-role self-registration form. Only a trusted project owner should grant the first admin role.

## Publish with GitHub Pages

1. Open this repository → Settings → Pages.
2. Under Build and deployment, select **Deploy from a branch**.
3. Choose branch **main**, folder **/(root)**, then Save.
4. Wait for the Pages deployment. The admin site URL will be:
   `https://sitaramevent669-prog.github.io/SITARAM-EVENT-ADMIN/`

## Files

- `index.html` — login and dashboard shell
- `styles.css` — responsive black/gold theme
- `app.js` — Supabase Auth, role check and CRUD operations

## Security notes

- The frontend contains a Supabase publishable key only; this key is designed for browser use.
- Database policies must continue to enforce admin permissions. Hiding UI controls is not security.
- Enable leaked-password protection in Supabase Auth settings.
- Keep the repository free of passwords, secret keys and service-role keys.
