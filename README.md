# GitPracticeRepo

A practice repository used for teaching/onboarding new Git and GitHub users.  

Want to give it a try? Anyone is welcome to use it!  

Add your name to the `changeme.md` file.  

Check out the [basic contribution workflow](#basic-contribution-workflow) to
get started.  


## Table of Contents
* [Configuring Git for the First Time](#configuring-git-for-the-first-time) 
* [Setting up SSH Authentication](#setting-up-ssh-authentication) 
    * [1. Generate an SSH Key](#1-generate-an-ssh-key) 
    * [2. Add your SSH Authentication Key to GitHub](#2-add-your-ssh-authentication-key-to-github) 
    * [3. Signing your Commits](#3-signing-your-commits) 
* [Basic Contribution Workflow](#basic-contribution-workflow) 
    * [1. Create a Fork](#1-create-a-fork) 
    * [2. Clone the Fork to your Local Machine](#2-clone-the-fork-to-your-local-machine) 
    * [3. Create a New Branch](#3-create-a-new-branch) 
    * [4. Make Changes and Commit](#4-make-changes-and-commit) 
    * [5. Push the Changes](#5-push-the-changes) 
    * [6. Create a Pull Request](#6-create-a-pull-request) 

## Configuring Git for the First Time

If you've never used Git before, you'll need to start by adding some basic
information.  

- See: <https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup>

You can configure Git from the command line by using `git config`.  
```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
git config --global init.defaultBranch main
```

These settings define the name and email that will be attached to all commits
that you make.

It also sets the default branch name for repositories to `main`, a standard
convention.  

> **Note**: If you don't want to use your real email, you can use the one that
> GitHub provides for you.
> 
> Go to your account settings and check the "Emails"
> tab. There will be an email there you can use:
> 
> `01234567+username@users.noreply.github.com`
> 
> This is your ID+Username. Use this as your email to keep it private.  


## Setting up SSH Authentication

In order to push up your local changes to GitHub, you'll need to set up
authentication.  

The easiest way to do this is by using SSH.  

### 1. Generate an SSH Key

To use SSH authentication, you need an SSH key.  

GitHub does not recommend using RSA keys. The `ed25519` encryption algorithm is
more secure than RSA.  

So, generate a key that uses `ed25519` encryption.  

```bash
ssh-keygen -t ed25519
```

The defaults are fine, set a passphrase if you want.  

This will generate two key files: a public key and a private key.  
```bash
~/.ssh/id_ed25519      # Private key
~/.ssh/id_ed25519.pub  # Public key
```
The public key (`.pub`) is the one that you will be using.  

> **Note**: **Never** share your private key with anyone.  

### 2. Add your SSH Authentication Key to GitHub
[Generate a new ssh key](#generate-a-new-ssh-key) if you don't have one.  

Add your SSH **public** key (`.pub` suffix) to GitHub as an "Authentication Key" (default).  

Click your profile picture (top right) and navigate to:
- Settings -> GPG and SSH Keys -> Add SSH Key -> Dropdown -> Authentication Key
- Paste in your key and click "Add SSH key"  
- You may be asked for some confirmation if you have 2FA enabled.  

You can then test if it worked on your command line:
```bash
ssh git@github.com
```
If you set it up properly, you will get the message: 
```plaintext
Hi <your_name>! You've successfully authenticated, bit GitHub does not provide shell access.
```

### 3. Signing your Commits

This part is optional, but encouraged.  

To **sign** your commits with your SSH key, you can simply add your SSH key
**again**, but this time select "Signing Key" instead of "Authentication Key."  

This is the same process as when you added your key for authentication.

Click your profile picture (top right) and navigate to:
- Settings -> GPG and SSH Keys -> Add SSH Key -> Dropdown -> Signing Key
- Paste in your key and click "Add SSH key"  
- You may be asked for some confirmation if you have 2FA enabled.  

Once that's done, you need to configure Git locally to use your key to sign
commits.  

Below is a set of commands that can be used to configure Git to use your SSH
key to sign commits.  
```bash
git config --global user.signingkey "/home/YOUR_USERNAME/.ssh/id_ed25519"
git config --global gpg.format ssh
git config --global tag.gpgsign true
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgSign true
mkdir -p ~/.config/git
touch ~/.config/git/allowed_signers
echo "YOUR_USERNAME $(cat ~/.ssh/id_ed25519.pub)" > ~/.config/git/allowed_signers
git config --global gpg.ssh.allowedSignersFile ~/.config/git/allowed_signers
```
Replace `YOUR_USERNAME` with your username on your PC.  

---

After running those commands, you can check your `~/.gitconfig` file. It should
now contain the following configuration:
```ini
[gpg]
	format = ssh
[tag]
	gpgsign = true
[commit]
	gpgSign = true
[gpg "ssh"]
	allowedSignersFile = /home/YOUR_USERNAME/.config/git/allowed_signers
```

Once all those steps are complete, you'll have successfully enabled both 
SSH authentication and commit signing with SSH.  

## Basic Contribution Workflow

#### This section expects you to have set up [SSH authentication on GitHub](#setting-up-ssh-authentication).  

You'll create your own fork of the repository using the GitHub web UI, clone
that fork to your local machine, create a branch, make changes, push to your
fork, then open a pull request.

The basic steps to contribute are outlined below.

### 1. Create a Fork

Go to the [original repository link](https://github.com/ProfessionalLinuxUsersGroup/GitPracticeRepo).
Click on "Fork" on the top right.

<img width="488" height="129" alt="fork_repo1" src="https://github.com/user-attachments/assets/69e74f29-a09b-4bac-b3f1-2e71a57bc735" />

Then click "Create Fork" on the next page.

<img width="793" height="558" alt="fork_repo2" src="https://github.com/user-attachments/assets/f25e0e15-eaf3-4625-80f9-abe53f895345" />

Now you'll have your own version of the repository tied to your GitHub account.

### 2. Clone the Fork to your Local Machine

After creating your fork, you'll need to clone it down to your local machine in
order to work on it.

```bash
git clone git@github.com:YOUR_USERNAME/GitPracticeRepo.git
```

### 3. Create a New Branch

Whenever making changes, you should create a branch with an appropriate name.  
Switch to that branch, then make changes there.

There are a few different ways to create and switch to a branch, but here we
will use `git branch` and `git switch`.  
```bash
git branch add-yourname-to-list
git switch add-yourname-to-list
```

Or, we could simply use the `-c` (create) option for `git switch`.  
```bash
git switch -c add-yourname-to-list
```

Git branches are typically named with alphanumeric characters separated by
dashes (`-`).  


### 4. Make Changes and Commit

Once you're on your new branch, add your name to the `./changeme.md` file,
using the editor of your choice.

```bash
vi u1ws.md
# Make changes
:wq
```

Once the changes are made, commit them.

```bash
git add changeme.md
git commit -m "feat: Add <my_name> to changeme.md"
```

> **Note**: There are differing opinions on how commit messages should be
> structured. A really solid commit message convention is outlined here:
> 
> <https://www.conventionalcommits.org/en/v1.0.0/#summary>

### 5. Push the Changes

After making your commit, you can now push the changes to **your fork** on the
**new branch** you created earlier.

```bash
git push origin add-yourname-to-list
```

This will update your forked repository on GitHub to contain the new branch
with the new changes.

### 6. Create a Pull Request

Now you'll be able to open a pull request.

GitHub should be smart about detecting new changes and prompt you to open
a pull request upon visiting the original repository or your own fork.

You can also go to the [original repository link](https://github.com/ProfessionalLinuxUsersGroup/GitPracticeRepo), go to the "Pull Requests" tab, and create a new pull request.

After starting your pull request, select your branch `add-yourname-to-list`,
and create a description.

---

Once you've made your PR, that's it! Then, you wait for it to be approved and
merged.

