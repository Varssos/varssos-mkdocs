# GitHub CLI (`gh`)

[`gh`](https://cli.github.com/) is GitHub's command-line client. It can manage authentication, repositories, pull requests, issues, releases, workflows, and other GitHub resources from a terminal.

See the [GitHub CLI manual](https://cli.github.com/manual/) for all commands and options.

## Install

Install the package on Ubuntu or an Ubuntu-based distribution:

```bash
sudo apt update
sudo apt install gh
```

For the newest release, follow the [official Linux installation instructions](https://github.com/cli/cli/blob/trunk/docs/install_linux.md).

Verify the installation:

```bash
gh --version
```

## Log in

Start the interactive login:

```bash
gh auth login
```

For GitHub.com, select these options when prompted:

1. `GitHub.com`
2. `HTTPS` or `SSH` as the Git protocol
3. `Login with a web browser`

The browser displays an authorization page where the one-time code from the terminal can be entered. A personal access token can also be supplied when browser login is unavailable:

```bash
gh auth login --with-token < token.txt
```

Do not pass a token directly as a command argument because it may be saved in the shell history. Delete `token.txt` after use and keep tokens out of Git repositories.

Configure Git to use `gh` as its credential helper for HTTPS operations:

```bash
gh auth setup-git
```

## Check the active account

Show authentication status, stored accounts, the active account, Git protocol, and token scopes:

```bash
gh auth status
```

Print the active username returned by the GitHub API:

```bash
gh api user --jq '.login'
```

## Basic usage

```bash
# Clone a repository
gh repo clone OWNER/REPOSITORY

# Create a repository from the current directory
gh repo create

# List pull requests
gh pr list

# Create a pull request interactively
gh pr create

# List issues
gh issue list

# Open the current repository in a browser
gh repo view --web

# Get help
gh help
gh pr --help
```

Most repository commands detect the GitHub repository from the current Git remote. Use `--repo OWNER/REPOSITORY` to target another repository explicitly.

## Work with multiple accounts

`gh` can store multiple accounts for the same GitHub host. Run the login command again and authenticate as the additional user:

```bash
gh auth login --hostname github.com
```

List the stored accounts and see which one is active:

```bash
gh auth status --hostname github.com
```

Switch the active account used by `gh`:

```bash
# Simply
gh auth switch
# Or more advanced
gh auth switch --hostname github.com --user USERNAME
```

Confirm the switch:

```bash
gh auth status
```

Remove one stored account without logging out the others:

```bash
gh auth logout --hostname github.com --user USERNAME
```

The active `gh` account and the author recorded in Git commits are separate settings. Configure the commit identity for each repository when using personal and work accounts:

```bash
git config user.name "Your Name"
git config user.email "your-address@example.com"
```

Run those commands inside the repository to set a local identity. Adding `--global` changes the default for all repositories. When using SSH remotes, Git authentication is selected by the SSH key and configuration rather than by `gh auth switch`.

## Log ouy
Log out the active account:

```bash
gh auth logout
```

