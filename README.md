# git_worktree

Shared scripts to work with [git-worktree](https://git-scm.com/docs/git-worktree) in an [Elixir](https://elixir-lang.org/) project.

## Prerequisites

- Git 2.5+ (for git-worktree support)
- Elixir project with standard dependency management

## Setup

All projects that warrant the use of [git-worktree](https://git-scm.com/docs/git-worktree) are setup in the same way.

1. Create a new directory and clone the repository as bare:

```bash
mkdir my_new_project
cd my_new_project
git clone --bare git@github.com:<USER>/<PROJECT>.git .bare
echo "gitdir: ./.bare" > .git
```

2. Check out the main branch:

```bash
git worktree add main
```

3. Copy this repository's `bin` directory to the root of your worktree.

4. Replace the `PROJECT_NAME` in `bin/new` with your proper project name.

## Usage

The main workflow commands provide a complete development cycle:

### `./bin/new branch_name`

Creates a new feature branch and development environment:
1. Syncs the main branch with origin
2. Creates a new worktree with a corresponding branch
3. Links cached dependencies from `.cache/deps` to avoid redownload
4. Symlinks compiled dependencies from `.cache/_build` to avoid recompilation
5. Runs `mix setup` to prepare the environment

After running this command, you can work in the new worktree directory, making commits as needed.

### `./bin/done branch_name`

Completes the feature development and cleans up:
1. Merges all your commits into a single squashed commit on main
2. Prompts for a commit message (interactive)
3. Pushes the changes to origin
4. Removes the worktree directory
5. Deletes the feature branch

This ensures a clean git history with one commit per feature.

## Utility Commands

- `./bin/sync` - Syncs the main worktree from origin.
- `./bin/ls` - Lists all worktrees.
- `./bin/remove` - Removes any worktree not removed by `./bin/done`.
