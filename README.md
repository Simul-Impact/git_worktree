# git_worktree

Shared scripts to work with [git-worktree](https://git-scm.com/docs/git-worktree) in an [Elixir](https://elixir-lang.org/) project.

## How to

All of the projects that warrant the use of [git-worktree](https://git-scm.com/docs/git-worktree) are setup in the same way.

1. A bare repository is cloned in a directory called `.bare`.

- `mkdir my_new_project`
- `cd my_new_project`
- `git clone --bare git@github.com:<USER>/<PROJECT>.git .bare`
- `echo "gitdir: ./.bare" > .git`

Then the main branch is checked out by running `git worktree main`.

Replace the `PROJECT_NAME` in `bin/new` with you proper project name.

Once done copy this repository's bin directory at the root of the worktree.

That way the main workflow commands become available:

`./bin/new branch_name` 

Creates a new worktre and the corresponding branch to work on.
Links the compiled dependencies from the `.cache` directory to avoid redownload and recompilation.

`./bin/done branch_name` 

Merges all your commits into a single one. Pushes to the origin. Then deletes the worktree and the branch.

And also provides the following utility commands:

- `./bin/sync` - Syncs the main worktree from origin.
- `./bin/ls` - Lists all worktrees.
- `./bin/remove` - Removes any worktree not removed by `./bin/done`.
