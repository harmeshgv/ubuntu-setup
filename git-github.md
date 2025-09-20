Here’s a clear step-by-step guide to **install Git** and **connect it to your GitHub account** on Ubuntu.

---

## 1️⃣ Install Git

Open a terminal and run:

```bash
sudo apt update
sudo apt install git
```

Check the installation:

```bash
git --version
```

You should see something like `git version 2.xx.x`.

---

## 2️⃣ Configure Git With Your Info

Git uses your name and email for commit metadata.

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

> **Tip:** Use the **same email** as your GitHub account so commits show as “verified” on GitHub.

You can confirm with:

```bash
git config --list
```

---

## 3️⃣ Create an SSH Key (Recommended for GitHub)

SSH keys let you push/pull without typing your password every time.

1. Generate a key:

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   * Press **Enter** to accept the default file path (`~/.ssh/id_ed25519`).
   * Optionally add a passphrase.

2. Start the ssh-agent:

   ```bash
   eval "$(ssh-agent -s)"
   ```

3. Add the key to the agent:

   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```

4. Copy the public key to your clipboard:

   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```

   (or use `xclip -sel clip < ~/.ssh/id_ed25519.pub` if you have `xclip` installed)

---

## 4️⃣ Add the Key to GitHub

1. Log in to [GitHub](https://github.com/).
2. Go to **Settings → SSH and GPG keys → New SSH key**.
3. Give it a name (e.g., “Ubuntu laptop”) and paste the copied key.

---

## 5️⃣ Test the Connection

```bash
ssh -T git@github.com
```

You should see:

```
Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 6️⃣ Clone / Push Repos

Now you can use SSH URLs for GitHub repos:

```bash
git clone git@github.com:username/repository.git
```

When you create a new repo locally:

```bash
cd your-project
git init
git remote add origin git@github.com:username/repository.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

---

✅ **Summary:**
`apt install git` → `git config` → generate & add SSH key → add key to GitHub → test → clone/push.

That’s it—your Ubuntu system is now connected to your GitHub account.
