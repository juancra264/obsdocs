Integrating Obsidian with a GitHub repository is one of the best ways to get free, private version control and backup for your markdown files.

The most powerful and popular tool for this is the **Obsidian Git** community plugin. Here is the step-by-step guide to setting it up on your desktop.

## Step 1: Initialize Git in your Vault

Before configuring Obsidian, your vault folder needs to be a Git repository connected to GitHub.

1. Go to GitHub and create a **New Repository** (keep it Private if you want your notes secure). Do **not** initialize it with a README or `.gitignore`.
    
2. Open your terminal (or Command Prompt) and navigate to your local Obsidian Vault folder:
    ```bash
    cd /path/to/your/obsidian/vault
    ```
    
3. Initialize the repository and link it to GitHub:
    ```
    git init
    git add .
    git commit -m "Initial vault commit"
    git branch -M main
    git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
    git push -u origin main
    ```

> ⚠️ **Important (.gitignore):** Obsidian saves your workspace layout and temporary files frequently. To prevent merge conflicts, create a file named `.gitignore` in your root vault folder and add the following lines:
> 
> Plaintext
> 
> ```
> .obsidian/workspace.json
> .obsidian/workspace-mobile.json
> .trash/
> ```

## Step 2: Install the "Obsidian Git" Plugin

1. Open Obsidian and open your vault.
    
2. Go to **Settings** $\rightarrow$ **Community plugins**.
    
3. Click **Turn on community plugins** if you haven’t already.
    
4. Click **Browse**, search for **Obsidian Git** (by Vinzent03), and click **Install**, then **Enable**.
    

## Step 3: Configure Authentication

The plugin relies on your computer's native Git environment to authenticate with GitHub.

### Option A: Using SSH (Recommended for Developers)

If your computer is already configured with SSH keys for GitHub, you are done! The plugin will just work in the background.

### Option B: Using a Personal Access Token (HTTPS)

If you prefer HTTPS, GitHub requires a Personal Access Token (PAT) instead of your normal password.

1. On GitHub, go to **Settings** $\rightarrow$ **Developer Settings** $\rightarrow$ **Personal Access Tokens** $\rightarrow$ **Tokens (classic)**.
    
2. Generate a new token with the `repo` scope selected. Copy the token string.
    
3. In Obsidian, open your terminal (or use your Git CLI manager) inside your vault folder and update your remote URL to include the token:
    
    Bash
    
    ```
    git remote set-url origin https://YOUR_USERNAME:YOUR_TOKEN@github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
    ```
    
## Step 4: Set Up Automatic Backups

Now that the plumbing is set up, you can configure how often Obsidian backs up your notes.

1. Go to Obsidian **Settings** $\rightarrow$ **Obsidian Git** (under Community Plugins).
    
2. Adjust the following settings to automate your workflow:
    
    - **Vault backup interval (minutes):** Set this to `15` or `30` to automatically commit and push changes. (Set to `0` to disable auto-backup).
        
    - **Auto pull interval (minutes):** Set this to automatically pull changes if you work across multiple computers.
        
    - **Push on backup:** Ensure this toggle is **On** so it actually pushes your commits to GitHub.
        

## How to Sync Manually

If you prefer not to use automatic intervals, you can trigger syncs manually using the Obsidian Command Palette:

1. Press `Ctrl + P` (Windows/Linux) or `Cmd + P` (Mac).
    
2. Type **Obsidian Git: Create backup** to manually commit and push your recent edits.
    
3. Type **Obsidian Git: Pull** to pull changes down from GitHub.