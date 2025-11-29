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

---

## 📤 Submitting Your Work

### Congratulations on completing the Intermediate Level! 🎉

You've mastered merging, conflict resolution, and advanced remote operations. Time to document your achievements!

### Step 1: Create Your Outcome Branch

From the intermediate branch, create your group's outcome branch:

```bash
git checkout intermediate
git checkout -b group-X-outcomes/intermediate
```

### Step 2: Document Your Outcomes

1. **Get the template**:
   ```bash
   git checkout main -- OUTCOME_TEMPLATE.md
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   ```

2. **Complete `OUTCOMES.md`** with:
   
   **Exercise 1 - Merging & Conflicts**:
   - Commands used to create branches and make conflicting changes
   - Output from `git merge` showing the conflict
   - The conflict markers you saw in your file
   - How you resolved the conflict
   - `git log --graph --oneline --all` showing merge commit
   
   **Exercise 2 - Tags & Stashing**:
   - Commands for creating annotated tags
   - Output from `git tag` and `git show v1.0`
   - Demonstration of stash workflow
   - Output from `git stash list` and `git stash show`
   
   **Exercise 3 - Multiple Remotes**:
   - Output from `git remote -v` before and after adding remotes
   - Commands for adding, renaming, removing remotes
   - Demonstration of fetch/push to specific remotes
   - Explanation of when multiple remotes are useful

3. **Document your challenges**:
   - How did you approach your first merge conflict?
   - Any confusion about when to use stash vs. commit?
   - Difficulties understanding remote tracking?
   - What resources did you use to solve problems?

4. **Reflect deeply**:
   - How does merge conflict resolution work?
   - When would you use tags in a real project?
   - Why is stash useful instead of always committing?
   - Real-world scenarios for multiple remotes (forks, open source, etc.)

### Step 3: Commit Your Documentation

```bash
git add OUTCOMES.md
git commit -m "docs: Add intermediate level exercise outcomes for Group X"
```

### Step 4: Push to Remote

```bash
git push origin group-X-outcomes/intermediate
```

### Step 5: Create Pull Request (If Required)

Submit a PR with title: "Outcomes: Group X - Intermediate Level"

### What to Include

✅ **Exercise 1 Requirements**:
- At least 2 branches with conflicting changes
- Screenshot or output showing conflict markers
- Resolution strategy explained
- Merge commit in git log
- `git log --graph` showing branch structure

✅ **Exercise 2 Requirements**:
- At least 1 annotated tag created
- Tag information with `git show`
- Stash workflow demonstration (save, list, pop)
- Example scenario where stash was useful

✅ **Exercise 3 Requirements**:
- At least 2 remotes configured
- All remote management commands demonstrated
- Explanation of fetch vs. pull
- Real-world use case for multiple remotes

✅ **General Requirements**:
- Complete command history with outputs
- Screenshots of complex operations (optional)
- Detailed problem-solving narratives
- Reflection (minimum 150 words)
- Self-assessment for all intermediate topics

### Evaluation Criteria

| Criterion | Weight | Key Focus for Intermediate Level |
|-----------|--------|----------------------------------|
| Completion | 20% | All 3 exercises with full documentation |
| Understanding | 25% | Merge strategies, conflict resolution, remote concepts |
| Practical Skills | 25% | Clean conflict resolution, proper tag/stash usage |
| Problem-Solving | 20% | How you debugged conflicts and remote issues |
| Documentation | 10% | Clear explanations of complex operations |

**Minimum score to advance to Master level**: 75/100

### Common Challenges to Document

💡 **Merge Conflicts**:
- How did you identify which changes to keep?
- Did you accidentally break code during resolution?
- How did you verify the merge was correct?

💡 **Tags vs. Branches**:
- Can you explain when to use each?
- Did you try pushing tags? What happened?

💡 **Stash Confusion**:
- Did stash pop cause any conflicts?
- When would stash apply be better than pop?

💡 **Remote Tracking**:
- What's the difference between `git fetch` and `git pull`?
- How do tracking branches work?

### Tips for Success

📝 Document conflicts BEFORE resolving them (screenshot!)  
📝 Save git log output at key points  
📝 Explain your thought process, not just commands  
📝 Connect concepts to real-world scenarios  
📝 Show both successes and mistakes  

### Resources

- Merge conflicts: https://git-scm.com/docs/git-merge
- Tags: https://git-scm.com/book/en/v2/Git-Basics-Tagging
- Stash: https://git-scm.com/docs/git-stash
- Remotes: https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes

---

**Next Steps**: Once you've mastered these skills, move to the `master` branch for advanced Git techniques including rewriting history, advanced branching strategies, and Git hooks!

