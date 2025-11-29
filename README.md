# taller-master-ugr
A repository to showcase how GitHub works to master students

# Intermediate Level Exercises

Welcome to the Intermediate level! These exercises will teach you about merging, conflict resolution, tags, and advanced remote operations.

## Exercise 1 - Merging Branches and Resolving Conflicts
**Objective**: Learn to merge branches and handle merge conflicts effectively.

**Tasks**:
1. Create two branches from main:
   ```bash
   git checkout main
   git checkout -b feature/header
   git checkout main
   git checkout -b feature/footer
   ```

2. In `feature/header` branch:
   * Create a file `page.html` with a header section
   * Commit your changes:
   ```bash
   git add page.html
   git commit -m "Add header to page"
   ```

3. Switch to `feature/footer` branch:
   ```bash
   git checkout feature/footer
   ```
   * Create the same file `page.html` but with a footer section
   * Commit your changes:
   ```bash
   git add page.html
   git commit -m "Add footer to page"
   ```

4. Merge both branches into main:
   ```bash
   git checkout main
   git merge feature/header
   git merge feature/footer  # This will create a conflict!
   ```

5. Resolve the conflict:
   * Open `page.html` and manually merge the changes
   * Keep both header and footer sections
   * Stage the resolved file: `git add page.html`
   * Complete the merge: `git commit -m "Merge footer with resolved conflicts"`

**Success Criteria**:
- You can successfully merge branches without conflicts
- You can identify and resolve merge conflicts
- You understand the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

## Exercise 2 - Using Tags and Stashing Changes
**Objective**: Learn to create tags for releases and temporarily save work with stash.

**Tasks - Part A: Tags**:
1. Create an annotated tag for your current work:
   ```bash
   git tag -a v1.0 -m "First stable version with merged features"
   ```

2. List all tags:
   ```bash
   git tag
   ```

3. View tag information:
   ```bash
   git show v1.0
   ```

4. Push the tag to remote:
   ```bash
   git push origin v1.0
   ```

**Tasks - Part B: Stashing**:
1. Start making changes to `page.html` (add a navigation section)

2. Before committing, you need to switch branches urgently:
   ```bash
   git stash save "WIP: adding navigation"
   ```

3. Your working directory is now clean. Switch to another branch and work there

4. Come back and restore your work:
   ```bash
   git checkout intermediate
   git stash list  # See your stashed changes
   git stash pop   # Apply and remove from stash
   ```

**Success Criteria**:
- You can create and push tags
- You understand the difference between lightweight and annotated tags
- You can stash and restore work-in-progress changes

## Exercise 3 - Working with Multiple Remotes
**Objective**: Learn to manage multiple remote repositories.

**Tasks**:
1. View your current remotes:
   ```bash
   git remote -v
   ```

2. Add a new remote (for example, a fork or backup):
   ```bash
   git remote add backup https://github.com/yourusername/taller-backup.git
   ```

3. List all remotes again:
   ```bash
   git remote -v
   ```

4. Fetch from a specific remote:
   ```bash
   git fetch backup
   ```

5. Push to a specific remote:
   ```bash
   git push backup intermediate
   ```

6. Rename a remote:
   ```bash
   git remote rename backup secondary
   ```

7. Remove a remote:
   ```bash
   git remote remove secondary
   ```

**Success Criteria**:
- You can add, rename, and remove remotes
- You understand the difference between `origin` and other remotes
- You can fetch and push to specific remotes
- You understand when multiple remotes are useful (forks, backups, upstream)

**Next Steps**: Once you've mastered these skills, move to the `master` branch for advanced Git techniques including rewriting history, advanced branching strategies, and Git hooks!

