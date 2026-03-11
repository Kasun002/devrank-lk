# 🇱🇰 GitHub Sri Lanka — Developer Rankings

A weekly-updated leaderboard of Sri Lankan GitHub developers, ranked by open-source activity.

**Live site →** `https://YOUR_USERNAME.github.io/YOUR_REPO`

---

## How it works

1. A list of Sri Lankan developers is maintained in [`data/users.json`](data/users.json)
2. Every Sunday, a GitHub Action runs a Python script that fetches each developer's stats via the GitHub GraphQL API
3. A `data/rankings.json` file is generated and committed
4. The static `index.html` reads `rankings.json` and renders the leaderboard

## Ranking Score

Developers are ranked by a composite score:

```
score = (commits × 3) + (PRs × 5) + (issues × 2) + (stars × 4) + (followers × 1)
```

All metrics are based on the **past 12 months** of activity.

---

## 🙋 Add yourself to the rankings

1. Fork this repo
2. Add your GitHub username to [`data/users.json`](data/users.json):
   ```json
   { "github": "your-github-username" }
   ```
3. Open a Pull Request

---

## Setup (for repo owners)

### 1. Create a GitHub Personal Access Token

Go to **GitHub → Settings → Developer Settings → Personal Access Tokens → Fine-grained tokens**

Required scopes: `read:user`, `repo` (public only is fine)

### 2. Add it as a repository secret

Go to your repo → **Settings → Secrets and variables → Actions**

Create a secret named `GH_TOKEN` with your token value.

### 3. Enable GitHub Pages

Go to **Settings → Pages** → Source: `Deploy from branch` → Branch: `main` → Folder: `/ (root)`

### 4. Run manually to test

Go to **Actions → Update GitHub Rankings → Run workflow**

---

## Project structure

```
├── .github/
│   └── workflows/
│       └── update-rankings.yml   # Scheduled GitHub Action
├── data/
│   ├── users.json                # List of registered developers
│   └── rankings.json             # Auto-generated — do not edit
├── scripts/
│   └── fetch_data.py             # Fetches stats from GitHub API
├── index.html                    # The ranking page
└── README.md
```
