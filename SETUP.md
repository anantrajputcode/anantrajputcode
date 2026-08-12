# Setup guide

This makes your GitHub profile README auto-update every day with your live stats
(age, repos, commits, stars, followers, lines of code).

## 1. Create the special profile repo

On GitHub, create a **new repository named exactly your username**
(`anantrajputcode/anantrajputcode`). GitHub automatically shows this repo's
README.md on your profile page.

## 2. Upload these files

Put all of these in the root of that repo, keeping the folder structure:

```
anantrajputcode/
├── README.md
├── today.py
├── requirements.txt
├── dark_mode.svg
├── light_mode.svg
├── cache/
│   └── .gitkeep
└── .github/
    └── workflows/
        └── main.yml
```

## 3. Create a Personal Access Token

1. Go to **GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Click **Generate new token**
3. Set **Resource owner** to yourself, and **Repository access** to "All repositories" (or at least this one)
4. Under **Permissions**, grant:
   - Account permissions: `Followers` (read), `Starring` (read), `Watching` (read)
   - Repository permissions: `Commit statuses` (read), `Contents` (read), `Issues` (read), `Metadata` (read), `Pull requests` (read)
5. Generate the token and copy it — you won't see it again

## 4. Add the token as a repo secret

1. In your `anantrajputcode/anantrajputcode` repo, go to **Settings → Secrets and variables → Actions**
2. Click **New repository secret**
3. Name: `ACCESS_TOKEN`
4. Value: paste the token you just copied

## 5. Let it run

- The workflow (`.github/workflows/main.yml`) runs automatically once a day, and also
  whenever you push to `main`.
- To trigger it manually right away: go to the **Actions** tab → **Update profile stats** →
  **Run workflow**.
- It'll run `today.py`, fill in the numbers on `dark_mode.svg` / `light_mode.svg`, and
  commit the updated files back to the repo. Your profile README will then show the
  refreshed card.

## Customizing later

- **Birthday**: edit the `BIRTHDAY` variable near the top of `today.py`
- **Bio / projects / links**: edit `README.md` directly
- **Card colors/layout**: edit `dark_mode.svg` and `light_mode.svg` — just keep the
  element `id`s (like `id="commit_data"`) unchanged, since the script looks for those
- **Run schedule**: edit the `cron` line in `.github/workflows/main.yml`
  (currently 05:30 UTC daily)
