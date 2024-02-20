# Git Cheat Sheet

Certainly! Git is a powerful tool for version control, allowing multiple people to work on the same project without conflicts. Below is a beginner-friendly cheat sheet guide to Git, including some basic concepts, commands, and examples.

## 1. **What is Git?**

Git is a distributed version control system designed to handle projects of any size with speed and efficiency. It allows you to track changes in your files, collaborate with others, and revert to previous states of a project whenever needed.

## 2. **Setting Up Git**

- **Install Git:** Depending on your operating system, find the appropriate version at [git-scm.com](https://git-scm.com/) and follow the installation instructions.

- **Configure Git:** Set your user name and email address because every Git commit uses this information:
  ```sh
  git config --global user.name "Your Name"
  git config --global user.email "youremail@example.com"
  ```

## 3. **Basic Git Commands**

- **Initialize a Git repository:**

  ```sh
  git init
  ```

  This command turns a directory into an empty Git repository.

- **Clone a repository:**

  ```sh
  git clone https://github.com/example/repo.git
  ```

  This command is used to copy an existing Git repository from a remote source.

- **Add files to staging:**

  ```sh
  git add <filename>
  git add .
  ```

  Adds specific file or all changes in the directory to the staging area.

- **Commit changes:**

  ```sh
  git commit -m "Commit message"
  ```

  Records your changes to the local repository with a descriptive message.

- **Check status:**

  ```sh
  git status
  ```

  Displays the status of your working directory and staging area.

- **View commit history:**

  ```sh
  git log
  ```

  Shows the commit history.

- **Create a branch:**

  ```sh
  git branch <branch_name>
  ```

  Creates a new branch.

- **Switch branches:**

  ```sh
  git checkout <branch_name>
  ```

  Switches to another branch.

- **Merge branches:**

  ```sh
  git merge <branch_name>
  ```

  Merges specified branch into the current branch.

- **Pull changes from remote repository:**

  ```sh
  git pull origin <branch_name>
  ```

  Fetches and merges changes on the remote server to your working directory.

- **Push changes to remote repository:**
  ```sh
  git push origin <branch_name>
  ```
  Sends your commits to the remote repository.

## 4. **Branching and Merging**

Branching allows you to diverge from the main line of development and continue to work independently without affecting the main line. Merging is the process of putting a forked history back together.

- **Creating a new branch:**

  ```sh
  git branch new-feature
  ```

- **Switching to the new branch:**

  ```sh
  git checkout new-feature
  ```

- **Merging a branch into the main branch:**
  First, switch to the branch you want to merge into:
  ```sh
  git checkout main
  ```
  Then merge the branch:
  ```sh
  git merge new-feature
  ```

## 5. **Handling Merge Conflicts**

Merge conflicts happen when Git can’t automatically resolve differences in code between two commits. When this occurs, Git will ask you to manually resolve the conflicts.

- To see which files have conflicts, use:

  ```sh
  git status
  ```

- Open the conflicted file(s) in your editor, find the conflicting changes (marked with `<<<<<<<`, `=======`, and `>>>>>>>`), and decide which changes to keep.

- After resolving the conflicts, add the files:

  ```sh
  git add <filename>
  ```

- Then commit the resolved changes:
  ```sh
  git commit
  ```
  Git will open a text editor for you to write a merge commit message.

## 6. **Git Stash**

Stashing takes your modified tracked files and saves them on a stack of unfinished changes that you can reapply at any time.

- **Stash changes:**

  ```sh
  git stash
  ```

- **List stashes:**

  ```sh
  git stash list
  ```

- **Apply the most recent stash:**
  ```sh
  git stash apply
  ```

## 7. **.gitignore File**

To ignore certain files from being tracked by Git, you can create a `.gitignore` file in your repository's root directory and list the files or directories you want to ignore.

- Example of a `.gitignore` file:
  ```
  node_modules/
  .env
  build/
  ```
