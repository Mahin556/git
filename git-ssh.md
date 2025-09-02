
# **Git SSH Authentication**

Git can use **SSH keys** to securely authenticate with remote repositories without typing your username and password every time.

---

## **1. Check for Existing SSH Keys**

```bash
ls -al ~/.ssh
```

* Look for files like `id_rsa` and `id_rsa.pub`.
* If they exist, you already have an SSH key pair.

---

## **2. Generate a New SSH Key**

```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

* `-t rsa` → type of key
* `-b 4096` → key length
* `-C` → comment (usually your email)

**Steps:**

1. Press Enter to accept the default file location (`~/.ssh/id_rsa`).
2. Enter a secure passphrase (optional but recommended).

---

## **3. Start the SSH Agent and Add Your Key**

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

---

## **4. Add SSH Key to GitHub / GitLab / Bitbucket**

* Copy your public key to clipboard:

```bash
cat ~/.ssh/id_rsa.pub
```

* Go to your Git hosting account:

  * **GitHub:** Settings → SSH and GPG keys → New SSH key → Paste key
  * **GitLab:** Preferences → SSH Keys → Add key
  * **Bitbucket:** Personal settings → SSH keys → Add key
* Give it a descriptive title and save.

---

## **5. Test SSH Authentication**

```bash
ssh -T git@github.com
```

> Expected output:

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

* If it shows your username, SSH authentication is working.

---

## **6. Use SSH URL for Git Remotes**

* **Add remote using SSH**

```bash
git remote add origin git@github.com:username/repo.git
```

* **Update remote to SSH**

```bash
git remote set-url origin git@github.com:username/repo.git
```

* **Push/Pull**

```bash
git push -u origin main
git pull origin main
```

---

## **7. Common SSH Troubleshooting**

| Problem                       | Solution                                                                               |
| ----------------------------- | -------------------------------------------------------------------------------------- |
| Permission denied (publickey) | Check if your SSH key is added to the agent and to your Git host account               |
| Wrong key used                | Specify key with `ssh -i ~/.ssh/id_rsa git@github.com` or configure in `~/.ssh/config` |
| Multiple keys                 | Create `~/.ssh/config` entries: <br>\`\`\`                                             |
| Host github.com               |                                                                                        |
| HostName github.com           |                                                                                        |
| User git                      |                                                                                        |
| IdentityFile \~/.ssh/id\_rsa  |                                                                                        |

```|


Do you want me to do that?
```
