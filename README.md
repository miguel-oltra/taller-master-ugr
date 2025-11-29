# taller-master-ugr
A repository to showcase how GitHub works to master students

# Master Level Exercises

Welcome to the Master level! These advanced exercises will teach you about rewriting Git history, advanced branching strategies, and using Git hooks for automation.

## Exercise 1 - Rewriting History (Rebase, Amend, and Interactive Rebase)
**Objective**: Learn to rewrite Git history safely and effectively using rebase and amend.

**Tasks - Part A: Amending Commits**:
1. Create a new file `config.txt` with some configuration:
   ```bash
   echo "version=1.0" > config.txt
   git add config.txt
   git commit -m "Add configuration file"
   ```

2. Realize you forgot something. Add more content:
   ```bash
   echo "environment=production" >> config.txt
   git add config.txt
   git commit --amend -m "Add complete configuration file"
   ```

3. View the log to see only one commit was created:
   ```bash
   git log --oneline -n 3
   ```

**Tasks - Part B: Interactive Rebase**:
1. Create multiple commits:
   ```bash
   echo "Feature A" > featureA.txt
   git add featureA.txt
   git commit -m "Add feature A"
   
   echo "Feature B" > featureB.txt
   git add featureB.txt
   git commit -m "Add feature B"
   
   echo "Fix typo in A" >> featureA.txt
   git add featureA.txt
   git commit -m "Fix typo"
   ```

2. Use interactive rebase to clean up the history:
   ```bash
   git rebase -i HEAD~3
   ```
   * In the editor, change the third commit from `pick` to `fixup` to squash it into the first
   * Save and close the editor

3. Verify your cleaned history:
   ```bash
   git log --oneline -n 5
   ```

**Tasks - Part C: Rebase a Branch**:
1. Create a feature branch and make commits
2. Meanwhile, main branch has advanced
3. Rebase your feature branch onto the latest main:
   ```bash
   git checkout feature-branch
   git rebase main
   ```

**Success Criteria**:
- You can amend the last commit without creating a new one
- You can use interactive rebase to squash, reword, or reorder commits
- You understand when to use rebase vs merge
- You know the dangers of rewriting public history

## Exercise 2 - Advanced Branching Strategies
**Objective**: Understand and implement professional branching strategies like Git Flow and GitHub Flow.

**Tasks - Part A: Implement Git Flow Pattern**:
1. Set up the branch structure:
   ```bash
   git checkout -b develop        # Development branch
   git checkout -b feature/login  # Feature branch
   ```

2. Work on the feature:
   * Make commits to `feature/login`
   * When complete, merge into develop:
   ```bash
   git checkout develop
   git merge --no-ff feature/login -m "Merge feature: login system"
   ```

3. Prepare a release:
   ```bash
   git checkout -b release/v1.0
   # Make any final adjustments
   echo "1.0.0" > VERSION
   git add VERSION
   git commit -m "Bump version to 1.0.0"
   ```

4. Merge release to main and develop:
   ```bash
   git checkout main
   git merge --no-ff release/v1.0
   git tag -a v1.0.0 -m "Release version 1.0.0"
   
   git checkout develop
   git merge --no-ff release/v1.0
   ```

5. Create a hotfix if needed:
   ```bash
   git checkout main
   git checkout -b hotfix/security-patch
   # Fix the issue
   git checkout main
   git merge --no-ff hotfix/security-patch
   git checkout develop
   git merge --no-ff hotfix/security-patch
   ```

**Tasks - Part B: GitHub Flow**:
1. Start from main:
   ```bash
   git checkout main
   git pull origin main
   ```

2. Create a descriptive branch:
   ```bash
   git checkout -b add-user-profile
   ```

3. Make commits and push regularly:
   ```bash
   git push -u origin add-user-profile
   ```

4. Open a Pull Request on GitHub (simulate this)

5. After review and CI passes, merge to main

**Success Criteria**:
- You understand the difference between Git Flow and GitHub Flow
- You can implement feature branches, release branches, and hotfixes
- You understand when to use `--no-ff` for merges
- You can choose the appropriate strategy for your project

## Exercise 3 - Using Git Hooks for Automation
**Objective**: Create and use Git hooks to automate checks and enforce policies.

**Tasks - Part A: Create a Pre-Commit Hook**:
1. Navigate to the hooks directory:
   ```bash
   cd .git/hooks
   ```

2. Create a pre-commit hook to check for debug statements:
   ```bash
   # Create pre-commit file (on Windows, create pre-commit without extension)
   cat > pre-commit << 'EOF'
   #!/bin/sh
   # Check for console.log or debugger statements
   
   if git diff --cached --name-only | grep -E '\.(js|ts)$' > /dev/null; then
       if git diff --cached | grep -E '(console\.log|debugger)'; then
           echo "Error: Found debug statements. Please remove them before committing."
           exit 1
       fi
   fi
   
   echo "Pre-commit checks passed!"
   exit 0
   EOF
   
   chmod +x pre-commit
   ```

3. Test the hook:
   * Try to commit a file with `console.log` - it should fail
   * Remove the debug statement and commit - it should succeed

**Tasks - Part B: Create a Commit-Msg Hook**:
1. Create a commit-msg hook to enforce commit message format:
   ```bash
   cat > commit-msg << 'EOF'
   #!/bin/sh
   # Enforce commit message format: "TYPE: Description"
   # Valid types: feat, fix, docs, style, refactor, test, chore
   
   commit_msg=$(cat "$1")
   pattern="^(feat|fix|docs|style|refactor|test|chore): .+"
   
   if ! echo "$commit_msg" | grep -E "$pattern" > /dev/null; then
       echo "Error: Commit message must match format 'TYPE: Description'"
       echo "Valid types: feat, fix, docs, style, refactor, test, chore"
       echo "Example: 'feat: Add user authentication'"
       exit 1
   fi
   
   exit 0
   EOF
   
   chmod +x commit-msg
   ```

2. Test with different commit messages

**Tasks - Part C: Create a Pre-Push Hook**:
1. Create a pre-push hook to run tests:
   ```bash
   cat > pre-push << 'EOF'
   #!/bin/sh
   # Run tests before pushing
   
   echo "Running tests before push..."
   
   # Uncomment and modify based on your project:
   # npm test
   # python -m pytest
   # mvn test
   
   echo "Pre-push checks passed!"
   exit 0
   EOF
   
   chmod +x pre-push
   ```

**Success Criteria**:
- You can create and modify Git hooks
- You understand the different hook types (pre-commit, commit-msg, pre-push, etc.)
- You can use hooks to enforce code quality and team standards
- You understand that hooks are local and not pushed to the repository

---

## 📤 Submitting Your Work

### Congratulations on completing the Master Level! 🎉

You've mastered advanced Git techniques including history rewriting, branching strategies, and automation with hooks. Now demonstrate your expertise!

### Step 1: Create Your Outcome Branch

```bash
git checkout master
git checkout -b group-X-outcomes/master
```

### Step 2: Document Your Outcomes

1. **Get the template**:
   ```bash
   git checkout main -- OUTCOME_TEMPLATE.md
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   ```

2. **Complete `OUTCOMES.md`** with comprehensive documentation:

   **Exercise 1 - Rewriting History**:
   - **Amend demonstration**: Show before/after of `git commit --amend`
   - **Interactive rebase**: Full walkthrough of `git rebase -i`
     - Output showing pick/squash/fixup/reword options
     - Before and after git log comparison
   - **Rebase vs merge**: Explain when to use each, with examples
   - Important: Document the dangers of rewriting public history
   
   **Exercise 2 - Advanced Branching Strategies**:
   - **Git Flow implementation**:
     - Diagram or description of your branch structure
     - Commands for develop, feature, release, hotfix branches
     - `git log --graph --all --oneline` showing the strategy
   - **GitHub Flow demonstration**:
     - Feature branch workflow
     - Commands and process
   - **Comparison**: When to use Git Flow vs GitHub Flow
   
   **Exercise 3 - Git Hooks**:
   - **Pre-commit hook**: Full script content and test results
   - **Commit-msg hook**: Script content and validation examples
   - **Pre-push hook**: Script content and demonstration
   - Screenshots of hooks preventing bad commits
   - Explanation of hook lifecycle and when each fires

3. **Advanced challenges documentation**:
   - Rebase conflicts: How did you resolve them?
   - Interactive rebase mistakes: Any lost commits? How recovered?
   - Hook debugging: Issues with script execution or permissions?
   - Branching strategy choice: Why did you choose certain approaches?

4. **Deep reflection** (minimum 200 words):
   - When is it safe to rewrite history? When is it dangerous?
   - How do branching strategies support team collaboration?
   - What role do hooks play in maintaining code quality?
   - How would you implement these in a professional setting?

### Step 3: Package Your Hooks

Create a `hooks/` directory with your hook scripts:

```bash
mkdir hooks
cp .git/hooks/pre-commit hooks/
cp .git/hooks/commit-msg hooks/
cp .git/hooks/pre-push hooks/
git add hooks/
```

### Step 4: Commit and Push

```bash
git add OUTCOMES.md hooks/
git commit -m "docs: Add master level exercise outcomes for Group X"
git push origin group-X-outcomes/master
```

### What to Include

✅ **Exercise 1 Requirements**:
- Minimum 3 commits demonstrating amend
- Interactive rebase with at least 4 operations (squash, fixup, reword, reorder)
- Side-by-side comparison of rebase vs merge for same scenario
- Explanation of when each technique is appropriate
- Warning documentation about rewriting public history

✅ **Exercise 2 Requirements**:
- Complete Git Flow cycle (feature → develop → release → main)
- Hotfix demonstration
- GitHub Flow demonstration with descriptive branches
- Branch strategy comparison with pros/cons
- `git log --graph` showing your branching patterns

✅ **Exercise 3 Requirements**:
- Working pre-commit hook with test cases
- Working commit-msg hook with test cases  
- Working pre-push hook with test cases
- Hook scripts included in `hooks/` directory
- Documentation of what each hook validates
- Evidence of hooks catching violations

✅ **General Requirements**:
- Complete command history for all operations
- Git log outputs showing history transformations
- Screenshots of hook executions
- Detailed explanations of complex operations
- Professional-quality reflection (200+ words)
- Self-assessment for all master-level topics

### Evaluation Criteria

| Criterion | Weight | Key Focus for Master Level |
|-----------|--------|----------------------------|
| Completion | 20% | All 3 exercises with sophisticated implementations |
| Understanding | 25% | Deep grasp of history rewriting, strategies, automation |
| Practical Skills | 25% | Safe rebase usage, appropriate strategy selection, functional hooks |
| Problem-Solving | 20% | Complex rebase conflicts, hook debugging, strategy decisions |
| Documentation | 10% | Professional-quality explanations and artifacts |

**Minimum score to advance to Master of Universe level**: 80/100

### Critical Topics to Address

🔴 **History Rewriting**:
- Why is `git push --force` dangerous?
- How do you coordinate rebases in a team?
- What's the difference between `git reset` and `git revert`?
- When is interactive rebase the right tool?

🔴 **Branching Strategies**:
- How does your strategy support CI/CD?
- What's the release process in each strategy?
- How do hotfixes work in your chosen strategy?
- What's the role of long-lived vs. short-lived branches?

🔴 **Git Hooks**:
- Why aren't hooks pushed to the repository?
- How would you share hooks across a team?
- What's the performance impact of complex hooks?
- How do hooks integrate with CI/CD pipelines?

### Tips for Excellence

🎯 Show, don't just tell - include comprehensive outputs  
🎯 Create diagrams for branching strategies (ASCII art is fine!)  
🎯 Test hooks thoroughly and document edge cases  
🎯 Connect techniques to real-world professional scenarios  
🎯 Demonstrate both correct usage and common mistakes  
🎯 Include recovery procedures for mistakes  

### Resources

- Git internals: https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain
- Rewriting history: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
- Git Flow: https://nvie.com/posts/a-successful-git-branching-model/
- GitHub Flow: https://guides.github.com/introduction/flow/
- Git Hooks: https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks

---

**Next Steps**: Ready for the ultimate challenge? Move to the `master-of-the-universe` branch for expert-level exercises on branch protection and security best practices!

