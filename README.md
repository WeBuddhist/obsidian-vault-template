# obsidian-vault-template

A template for creating shared [Obsidian](https://obsidian.md) vaults that sync via Git every 10 minutes. Comes preconfigured with the [obsidian-git](https://github.com/Vinzent03/obsidian-git) community plugin.
## What this gives you

- A Git-backed Obsidian vault that auto-pulls every 10 minutes and auto-commits/pushes your changes on a 10-minute interval
- A `.gitignore` that keeps personal workspace state and OS junk (`.DS_Store`, `.trash/`, etc.) out of the repo
- The obsidian-git plugin already bundled and configured, so new collaborators can sync as soon as they clone your repo and open in Obsidian

## Set up a new vault

### 1. Install Obsidian

Download and install Obsidian from [obsidian.md](https://obsidian.md). It's free and available for Mac, Windows, Linux.

### 2. Create a new repo from this template

1. Go to the [WeBuddhist organization on GitHub](https://github.com/WeBuddhist) and click the **Repositories** tab.
2. Click the green **New repository** button (top right).
3. Give the repo a name (e.g. `team-notes`).
4. Choose **Private** or **Public** as appropriate.
5. Next to **Start with a template** click on the **No template** dropdown and select `WeBuddhist/obsidian-vault-template.
6. Click **Create repository**.

GitHub will create a new repo with the vault structure and obsidian-git config.

### 3. Install Git on your computer and authorize the command line

You'll need Git on your machine to clone the repo and let Obsidian sync.

**Mac**

1. Open Terminal (⌘ + Space, type "Terminal").
2. Run `git --version`. If Git isn't installed, macOS will prompt you to install the Xcode Command Line Tools — accept the prompt and wait for it to finish.
3. Set your identity (this is what shows up on commits):
   ```
   git config --global user.name "Your Name"
   git config --global user.email "you@webuddhist.com"
   ```
4. Authorize GitHub from the command line. The easiest way is to install [GitHub CLI](https://cli.github.com/) (`brew install gh`), then run:
   ```
   gh auth login
   ```
   Choose **GitHub.com → HTTPS → Login with a web browser**, and follow the prompts. This stores credentials so you won't be prompted on every push.

**Windows**

1. Install [Git for Windows](https://git-scm.com/download/win). Use the defaults during install.
2. Open Git Bash (or PowerShell) and set your identity:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "you@webuddhist.com"
   ```
3. Install [GitHub CLI](https://cli.github.com/) and run `gh auth login` to authorize:
	Choose **GitHub.com → HTTPS → Login with a web browser**, and follow the prompts. This stores credentials so you won't be prompted on every push.

### 4. Clone the repo to your computer

On the new repo's GitHub page, click the green **Code** button and copy the HTTPS URL.

In Terminal (Mac)(or Git Bash), navigate to where you want the vault folder to live and run:

```
cd ~/Documents
git clone https://github.com/WeBuddhist/<your-new-repo>.git
```

This creates a folder with the vault contents inside it.

(If you're using GitHub Desktop, click **File → Clone repository**, pick the repo from the list, and choose where to save it.)

### 5. Open the folder as a vault in Obsidian

1. Open Obsidian.
2. Click **Open another vault** (the vault-switcher icon, bottom-left).
3. Choose **Open folder as vault** and select the folder you just cloned.

### 6. Trust the author and enable the plugin

The first time you open the vault, Obsidian will warn you about community plugins.

1. Click **Trust author & enable plugins**.
2. Go to **Settings → Community plugins** and confirm **Obsidian Git** is enabled.

That's it — the vault will start auto-pulling and auto-committing on a 10-minute interval.

## Inviting collaborators

Each teammate repeats steps 1 and 3–6 above:

1. Install Obsidian.
2. Install Git and authorize the command line (or use GitHub Desktop).
3. Make sure they have access to the repo on GitHub.
4. Clone the repo and open the folder as a vault in Obsidian.
5. Trust the author and enable plugins.

## How sync works

The obsidian-git plugin is configured in `.obsidian/plugins/obsidian-git/data.json` to:

- Auto-pull every 10 minutes (and on app boot)
- Auto-commit changes every 10 minutes with a message like `vault backup: 2026-05-05 14:32:01`
- Pull before pushing, using merge as the sync method

If two people edit the same note at the same time, you may see a merge conflict — Obsidian Git will show conflict markers in the file, and you can resolve them like any other Git conflict.

### Committing on demand

If you don't want to wait for the 10-minute auto-commit (e.g. you just finished a big edit and want to share it now), click the **Source Control View** icon in the left ribbon to open the right-side Git panel. From there you can stage files, write a commit message, and push with one click. You can also run **Obsidian Git: Create backup** from the command palette (`Cmd/Ctrl + P`) to do a full add → commit → push in one shot.

## Mobile

Obsidian works on iOS and Android, and obsidian-git supports mobile too. Mobile setup requires a personal access token; see the [obsidian-git docs](https://publish.obsidian.md/git-doc/Getting+Started) for the current steps.

## Customizing the template

- **Sync interval** — edit `autoPullInterval` and `autoSaveInterval` in `.obsidian/plugins/obsidian-git/data.json`. Default is `10` (minutes).
- **Commit message format** — edit `commitMessage` in the same file.
- **Ignored files** — edit `.gitignore` to add anything else you don't want tracked.

## Troubleshooting

- **"Author not trusted" warning keeps appearing** — make sure you clicked **Trust author & enable plugins**, not just **Turn on community plugins**.
- **Nothing is syncing** — open the command palette (`Cmd/Ctrl + P`) and run `Obsidian Git: Check repository status`. The status bar at the bottom of Obsidian should also show the current branch and sync state.
- **Authentication errors on push** — re-run `gh auth login`, or set up an [SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) if you prefer.
