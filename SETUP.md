# Setup guide

## Fixing your current git conflict (do this first)

The conflict you're hitting is because GitHub's repo already has Andrew Grant's original
template files in it (probably from when the repo was created), and your local repo has
different content. The simplest fix is to just replace everything with this final,
personalized version:

```
# from inside your local anantrajputcode folder
git checkout --ours .          # if mid-conflict, keep resolving manually instead — see below
```

Actually, the cleanest path given where you are now:

1. **Finish or abort the current merge**, whichever state you're in:
   ```
   git merge --abort
   ```
   (This safely cancels the in-progress merge and returns you to before you ran `git pull`.)

2. **Delete the old files** in your local folder and replace them with the files from this
   package (README.md, today.py, dark_mode.svg, light_mode.svg, requirements.txt,
   .github/workflows/main.yml, cache/.gitkeep).

3. **Force your local version to become the new main**, since you don't need Andrew's
   original commit history:
   ```
   git add .
   git commit -m "Personalize profile README"
   git push origin main --force
   ```
   `--force` overwrites whatever's on GitHub with your local version. This is safe here
   since it's just template files you don't need to preserve.

## 1. Create the special profile repo (skip if already done)

Create a repo named exactly your username: `anantrajputcode/anantrajputcode`. GitHub
automatically shows this repo's README.md on your profile page.

## 2. File structure

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

1. **GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens**
2. Click **Generate new token**
3. **Resource owner**: yourself. **Repository access**: this repo (or all repos)
4. **Permissions**:
   - Account: `Followers` (read), `Starring` (read), `Watching` (read)
   - Repository: `Commit statuses` (read), `Contents` (read), `Issues` (read),
     `Metadata` (read), `Pull requests` (read)
5. Generate and copy the token — you won't see it again

## 4. Add the token as a repo secret

**Settings → Secrets and variables → Actions → New repository secret**
- Name: `ACCESS_TOKEN`
- Value: the token from step 3

## 5. Run it

- Runs automatically once a day, and on every push to `main`
- To trigger immediately: **Actions** tab → **Update profile stats** → **Run workflow**
- It fills in your live GitHub stats on the card and commits the update back

## Customizing later

- **Bio fields on the card** (OS, Role, Editor, Languages, Hobbies, Contact links):
  edit the hardcoded `<tspan>` text directly in `dark_mode.svg` and `light_mode.svg` —
  these are NOT script-generated, so you can freely change the wording
- **Birthday**: edit the `BIRTHDAY` variable near the top of `today.py`
- **Live stats** (age, repos, stars, commits, followers, lines of code): these ARE
  script-generated — don't hand-edit the `id="..."` elements, the script overwrites them
- **Colors**: edit the `.key`, `.value`, `.addColor`, `.delColor`, `.cc` styles at the
  top of each SVG
