# obsidian-vault-template

A template for creating a shared [Obsidian](https://obsidian.md) notebook (called a *vault*) that your whole team can edit together. Everyone's changes save and sync automatically every 10 minutes. The vault comes set up with the [obsidian-git](https://github.com/Vinzent03/obsidian-git) community plugin.

## What this gives you

- A shared Obsidian vault. Whatever you write, your teammates see — and the other way around.
- Automatic saving and syncing every 10 minutes, so you don't have to remember to save.
- A list of files to ignore (`.gitignore`) so personal settings and hidden system files stay out of the shared copy.
- The Obsidian Git plugin already installed and set up. New teammates can start using the vault as soon as they finish setup.

## A few words you'll see

- **Vault** — the folder that Obsidian uses to hold your notes.
- **Git** — the tool that syncs the vault between you and your teammates.
- **Terminal** (Mac) / **PowerShell** or **Git Bash** (Windows) — a window where you type commands instead of clicking buttons. You only need it during setup.
- **Clone** — making a copy of the GitHub repo on your own computer.
- **Sync** — what happens automatically: your changes go up to GitHub, and your teammates' changes come down to you.

## Set up a new vault

You only do this once per team. After this, you just open Obsidian like a normal app.

### 1. Install Obsidian

Download Obsidian from [obsidian.md](https://obsidian.md) and install it. It's free and works on Mac, Windows, and Linux.

### 2. Create a new repo from this template

This is the shared home for your vault on GitHub.

1. Go to the [WeBuddhist organization on GitHub](https://github.com/WeBuddhist) and click the **Repositories** tab.
2. Click the green **New repository** button at the top right.
3. Type a name for the repo (for example, `team-notes`).
4. Choose **Private** (only WeBuddhist GitHub team members can see it) or **Public** (anyone can see it).
5. Next to **Repository template**, click the **No template** dropdown and choose `WeBuddhist/obsidian-vault-template`.
6. Click **Create repository**.

GitHub will create a new repo with the vault's structure already inside it.

### 3. Install Git and connect your GitHub account

You only do this once per computer. Git is the tool Obsidian uses to sync the vault. After you connect your GitHub account, you won't have to log in again.

**Mac**

1. Open Terminal. (Press `Cmd + Space`, type "Terminal", and press Return.)
2. Type `git --version` and press Return. If Git isn't installed, your Mac will ask if you want to install the Xcode Command Line Tools — click **Install** and wait for it to finish.
3. Tell Git who you are. This name and email will appear next to every change you save:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "you@webuddhist.com"
   ```
4. Connect your GitHub account. The easiest way is to install [GitHub CLI](https://cli.github.com/) by running:
   ```
   brew install gh
   ```
   If Terminal says `command not found: brew`, you don't have Homebrew yet. Homebrew is a free tool that installs other tools on a Mac. Install it by pasting this into Terminal and pressing Return:
   ```
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
   It will ask for your Mac password and may take a few minutes. When it finishes, you may see a "Next steps" message at the end — copy and run the two `echo` and `eval` lines it shows you (this lets Terminal find `brew`). Then run `brew install gh` again.

   Once GitHub CLI is installed, run:
   ```
   gh auth login
   ```
   Choose **GitHub.com → HTTPS → Login with a web browser** and follow the steps it shows you. After you do this once, GitHub won't ask for your password again.

**Windows**

1. Install [Git for Windows](https://git-scm.com/download/win). Keep the default settings during installation.
2. Open Git Bash (or PowerShell) and tell Git who you are:
   ```
   git config --global user.name "Your Name"
   git config --global user.email "you@webuddhist.com"
   ```
3. Install [GitHub CLI](https://cli.github.com/), then run `gh auth login` to connect your GitHub account. Choose **GitHub.com → HTTPS → Login with a web browser** and follow the steps it shows you. After you do this once, GitHub won't ask for your password again.

### 4. Make a copy of the repo on your computer

This step downloads a copy of the GitHub repo onto your own computer. The technical word for this is *cloning*.

**First, decide where the vault should live.** Use Finder (Mac) or File Explorer (Windows) to create a folder for it — for example, a folder called `WeBuddhist` inside your Documents folder.

**Now tell the Terminal where that folder is.** The "where" is called the *path*. Here are the easiest ways to copy it.

*Mac*

- Open Terminal, type `cd ` (the letters c-d followed by one space), then **drag the folder from Finder onto the Terminal window**. Terminal will paste the path for you. Press Return.
- Or, in Finder, hold the **Option** key and right-click the folder. Choose **Copy "[folder name]" as Pathname** from the menu. Then in Terminal, type `cd ` and paste with `Cmd + V`.

*Windows*

- In File Explorer, click into the address bar at the top of the window — the path will appear. Copy it.
- Or, hold **Shift** and right-click the folder. Choose **Copy as path** from the menu.
- In PowerShell or Git Bash, type `cd ` and paste the path. (You can also drag the folder onto the PowerShell window to paste its path.)

**Copy the repo's link from GitHub.** On your new repo's page on GitHub, click the green **Code** button and copy the HTTPS link.

**Download the repo into that folder.** Back in Terminal (or PowerShell / Git Bash), type `git clone ` and paste the link:

```
git clone https://github.com/WeBuddhist/<your-new-repo>.git
```

Press Return. This creates a new folder inside the one you chose, with the vault's contents inside.

### 5. Open the folder as a vault in Obsidian

1. Open Obsidian.
2. In the menu at the top, choose **File**, then **Open Vault**.
3. In the window that appears, click **Open** next to **Open folder as vault**.
4. Choose the folder that you just downloaded.

Or, if you already have another vault open in Obsidian:

1. Click the name of the open vault in the bottom-left corner of the Obsidian window.
2. In the menu that appears, choose **Manage Vaults**.
3. In the window that appears, click **Open** next to **Open folder as vault**.
4. Choose the folder that you just downloaded.

### 6. Trust the author and turn on the plugin

The first time you open the vault, Obsidian will show a warning about community plugins. This is because the Git plugin came with the template.

1. Click **Trust author & enable plugins**.
2. Go to **Settings → Community plugins** and check that **Obsidian Git** is turned on.

That's it. The vault will now save your changes and pull in your teammates' changes automatically every 10 minutes.

## How sync works

Every 10 minutes, Obsidian Git does two things:

- **Pulls** — downloads any changes your teammates have made.
- **Saves and uploads** — records your changes (called a *commit*) and sends them up to GitHub (called a *push*).

It also pulls when you first open Obsidian, so you start with the latest copy of the vault.

If two people edit the same line of the same note at the same time, Git won't know which version to keep. This is called a **merge conflict**. Obsidian Git will mark the conflicting lines in the file with special symbols. You can pick the version you want, delete the rest, and save the file.

### Saving on demand

If you don't want to wait 10 minutes (for example, you just finished a big edit and want your teammates to see it now), you can save manually.

- Click the **Source Control View** icon in the left ribbon to open the Git panel on the right side of Obsidian. From there, you can pick which files to save, type a short message about the change, and click to save and upload.
- Or, open Obsidian's command palette by pressing `Cmd + P` (Mac) or `Ctrl + P` (Windows). Type "create backup" and choose **Obsidian Git: Create backup**. This saves and uploads everything in one step.

## Troubleshooting

- **The "Author not trusted" warning keeps appearing** — make sure you clicked **Trust author & enable plugins**, not just **Turn on community plugins**.
- **Nothing is syncing** — open the command palette (`Cmd + P` on Mac, `Ctrl + P` on Windows) and run **Obsidian Git: Check repository status**. The bar at the bottom of Obsidian also shows the current branch and sync status.
- **You see an authentication error when saving** — run `gh auth login` again to reconnect your GitHub account. If that doesn't work, you can [set up an SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) instead.
