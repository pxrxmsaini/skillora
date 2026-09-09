# Skillora — deploy + admin setup (5–10 min)

This is a **static site with a real admin panel**. There's no traditional
server or database — instead, when you (the admin) publish a guide, it gets
committed straight into `data/posts.json` in your GitHub repo, and the live
site reads from that file. This is the same pattern used by many small
static blogs.

## What's in here

```
index.html          the live site
data/posts.json      all blog posts — the site's "database"
admin/index.html      the admin panel (Decap CMS)
admin/config.yml      tells the admin panel what fields a "guide" has
netlify.toml
```

## 1. Push this folder to GitHub

Create a new GitHub repo and push everything in this folder to it
(keep the folder structure exactly as-is — `data/` and `admin/` must stay
at the top level, next to `index.html`).

## 2. Connect it to Netlify

1. Go to [app.netlify.com](https://app.netlify.com) → **Add new site → Import
   an existing project** → pick your GitHub repo.
2. Build settings: leave the build command **empty**, publish directory `.`
   (this repo has no build step — it's plain HTML).
3. Click **Deploy**. Your site will be live at a `*.netlify.app` URL
   (you can add a custom domain later in Site settings → Domain management).

## 3. Turn on the admin login (Netlify Identity + Git Gateway)

This is what makes the admin panel real — it's what lets you log in and
have your changes actually saved back to GitHub.

1. In your Netlify site dashboard: **Site configuration → Identity → Enable
   Identity**.
2. Under Identity → **Registration**, set it to **Invite only** (so random
   people can't sign up as admins).
3. Under Identity → **Services → Git Gateway**, click **Enable Git Gateway**.
4. Back on the Identity tab, click **Invite users**, and invite yourself
   (your email). You'll get an email with a link to set your password.

## 4. Log in and publish

Visit `https://your-site.netlify.app/admin/`, log in with the account you
just set up, and you'll see the **Guides** collection — every post as a
list you can edit, reorder, add to, or delete. Saving a change commits
directly to `data/posts.json` in your GitHub repo, and Netlify
auto-redeploys the site within a few seconds.

The nav's **"Admin login ↗"** button already links to `/admin/`, so this
is the only way guides get published now — the old browser-only "quick
publish" popup has been removed since it never touched the real site.

## Notes

- Everything else on the site (dark mode, the skill tracker, the Prompt
  Studio) still works exactly as before — those are genuinely
  per-visitor, browser-only features, which is normal for a static site.
- If you ever want real user accounts, comments, or a full database
  instead of this Git-backed model, that's a bigger step up (a real
  backend like Supabase or Firebase) — happy to help with that separately
  if you get there.
