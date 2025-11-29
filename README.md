# taller-master-ugr
A repository to showcase how GitHub works to master students

# Newbie Level Exercises

Welcome to the Newbie level! These exercises will help you get started with basic Git commands and workflows.

## Exercise 1 - Basic Git Commands and Repository Setup
**Objective**: Learn to initialize repositories, make commits, and check repository status.

**Tasks**:
1. Configure your Git identity:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

2. Clone this repository using SSH:
   * First, [configure SSH credentials](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
   * Then clone:
   ```bash
   git clone git@github.com:miguel-oltra/taller-master-ugr.git
   ```

3. Practice basic commands:
   * Create a new file called `hello.txt` with your name in it
   * Use `git status` to see the untracked file
   * Use `git add hello.txt` to stage the file
   * Use `git commit -m "Add hello.txt with my name"` to commit
   * Use `git log` to view your commit history

**Success Criteria**: 
- You have successfully cloned the repository
- You can view the status of your working directory
- You have made at least one commit with a meaningful message

## Exercise 2 - Create and Switch Branches & Basic Remote Operations
**Objective**: Learn to create branches, switch between them, and push changes to remote.

**Tasks**:
1. Create a new branch called `feature/my-info`:
   ```bash
   git branch feature/my-info
   git checkout feature/my-info
   # Or use the shortcut: git checkout -b feature/my-info
   ```

2. Add a new file called `my-info.txt` containing:
   * Your name
   * Your favorite programming language
   * Why you're learning Git

3. Commit your changes:
   ```bash
   git add my-info.txt
   git commit -m "Add personal information"
   ```

4. Push your branch to the remote repository:
   ```bash
   git push origin feature/my-info
   ```

5. Switch back to the main branch:
   ```bash
   git checkout main
   ```

6. Pull the latest changes from remote:
   ```bash
   git pull origin main
   ```

**Success Criteria**:
- You have created and switched between branches
- Your feature branch exists on the remote repository
- You understand the difference between local and remote branches
- You can successfully push and pull changes

**Next Steps**: Once you've completed these exercises, you're ready to move to the `intermediate` branch for more challenging tasks!

