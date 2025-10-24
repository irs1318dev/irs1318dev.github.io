# Simple Command Line Operations and Git Usage

Starting in the 2019 season, there’s been a stronger need to use the command line than in previous years. Command-line interfaces are used often in real-world engineering and software development, so learning them is very useful.

## Opening CMD and navigating to a directory in Windows

(Note that the first few steps are different on macOS/Linux—please search for instructions specific to your OS. On Linux/Unix, you are looking for a Bash/shell window; on macOS, you are looking for Terminal.)

Press the Start button (or the Windows key on your keyboard), type `cmd`, and open Command Prompt. This opens Command Prompt (cmd) scoped to your user home directory (typically `C:\\Users\\username\\`).

You’ll need to navigate around to do anything useful. To list the contents of your current directory, type `dir` (`ls` on macOS/Linux). To navigate to another directory, use the change directory command (`cd`) like `cd directory`. With this command, `..` references the directory above your current location, and `.` references the current directory. You can also use a full path, such as `cd C:\\Users\\username\\git\\`, to navigate directly.

## Simple Git operations in Command Prompt

1. `git status` shows the files that differ from what has been committed.
2. `git restore filename` discards changes to the specified file in your working directory and replaces it with the last-committed version from the local repository.
3. `git add -A` stages all currently changed files in your working directory.
4. `git commit -m "message"` commits all currently staged changes with the provided message.
5. `git push` pushes commits from your local repository to the remote repository (you may need to run `git push origin branchname` the first time you push a new branch).
6. `git branch` shows the branches that currently exist for the repository.
7. `git branch -c master branchname` creates a new topic branch off of the master branch, and `git checkout -b branchname` creates a new topic branch off of the current branch.
8. `git pull` updates your local repository with changes that have been pushed to the remote repository.
9. `git checkout branchname` switches your working directory to a different branch.
10. `git clone https://github.com/irs1318dev/Fauxbot.git` clones the repository tracked at the provided URL, creating a local copy.

For more information about Git in the command prompt, see:

-   [GitHub’s Git cheat sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet/)
-   [GitHub’s Git Handbook](https://guides.github.com/introduction/git-handbook/)
