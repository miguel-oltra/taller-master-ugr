# taller-master-ugr
A repository to showcase how GitHub works to master students

# Master Level Exercise

Welcome to the Master level! This advanced exercise will teach you about rewriting Git history using rebase and amend commits.

## Exercise - Rewriting History (Rebase and Amend Commits)
**Objective**: Learn to rewrite Git history safely and effectively using rebase and amend to create clean, professional commit histories.

**Tasks**:

### Part 1: Amending Commits
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

### Part 2: Interactive Rebase for Cleaning Up History
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
   * In the editor, change the third commit from `pick` to `fixup` (or `f`) to squash it into the first
   * You can also use `reword` (or `r`) to change commit messages
   * Save and close the editor

3. Verify your cleaned history:
   ```bash
   git log --oneline -n 5
   ```

### Part 3: Rebasing a Branch
1. Create a feature branch and make commits:
   ```bash
   git checkout -b feature/awesome-feature
   echo "Awesome Feature" > awesome.txt
   git add awesome.txt
   git commit -m "Add awesome feature"
   ```

2. Switch back to master and make a change to simulate main branch advancement:
   ```bash
   git checkout master
   echo "Master update" > master-update.txt
   git add master-update.txt
   git commit -m "Update on master branch"
   ```

3. Rebase your feature branch onto the latest master:
   ```bash
   git checkout feature/awesome-feature
   git rebase master
   ```

4. View the history graph to see the linear history:
   ```bash
   git log --graph --oneline --all -n 10
   ```

### Part 4: Understanding the Risks
1. Examine the commit SHAs before and after rebase/amend
2. Understand why you should NEVER rewrite public/shared history
3. Practice the safe workflow:
   * Rewrite history only on private branches
   * Use `git push --force-with-lease` if you must push rewritten history
   * Document when you've rewritten history

**Success Criteria**:
- You can amend the last commit without creating a new one
- You can use interactive rebase to squash, fixup, reword, or reorder commits
- You understand when to use rebase vs merge
- You can rebase a feature branch onto an updated main branch
- You know the dangers of rewriting public history and how to avoid them
- You understand the difference between `git push --force` and `git push --force-with-lease`

---

## 📤 Submitting Your Work

### Congratulations on completing the Master Level! 🎉

You've mastered advanced Git techniques including history rewriting with rebase and amend. Now demonstrate your expertise!

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

   **Part 1 - Amending Commits**:
   - Commands used for amend operations
   - Git log output before and after amend
   - Comparison of commit SHAs to show history was rewritten
   
   **Part 2 - Interactive Rebase**:
   - Commands and editor interactions for interactive rebase
   - Demonstration of fixup, reword, and other rebase operations
   - Git log output showing cleaned-up history before and after
   
   **Part 3 - Rebasing a Branch**:
   - Commands for creating feature branch and rebasing onto master
   - `git log --graph --all --oneline` showing linear history after rebase
   - Explanation of how rebase differs from merge
   
   **Part 4 - Understanding Risks**:
   - Documentation of how commit SHAs change during rebase
   - Explanation of why rewriting public/shared history is dangerous
   - Best practices for safe history rewriting
   - Difference between `--force` and `--force-with-lease`
3. **Advanced challenges documentation**:
   - Rebase conflicts: How did you resolve them?
   - Interactive rebase mistakes: Any issues? How did you recover?
   - Force push understanding: When to use `--force` vs `--force-with-lease`?
   - Real-world scenarios where you'd choose rebase over merge

4. **Deep reflection** (minimum 200 words):
   - When is it safe to rewrite history? When is it dangerous?
   - How does rebase help create clean, professional commit histories?
   - What's the fundamental difference between rebase and merge?
   - How would you implement history-rewriting workflows in a professional team setting?
   - Why is it important to never rewrite public/shared history?

### Step 3: Commit and Push

```bash
git add OUTCOMES.md
git commit -m "docs: Add master level exercise outcomes for Group X"
git push origin group-X-outcomes/master
```

### What to Include

✅ **Part 1 Requirements**:
- Minimum 3 commits demonstrating amend functionality
- Git log showing commit SHAs before and after amend
- Explanation of how amend rewrites history

✅ **Part 2 Requirements**:
- Interactive rebase with at least 4 operations (pick, squash, fixup, reword, etc.)
- Before and after git log comparison
- Documentation of what each rebase operation does

✅ **Part 3 Requirements**:
- Complete demonstration of rebasing a feature branch
- `git log --graph` showing linear history vs merge commit approach
- Explanation of when rebase is preferable to merge

✅ **Part 4 Requirements**:
- Clear documentation of the dangers of rewriting public history
- Examples of safe vs unsafe rebase scenarios
- Explanation of `--force-with-lease` vs `--force`
- Team workflow considerations for history rewriting

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
| Completion | 20% | Exercise completed with all parts and sophisticated implementations |
| Understanding | 25% | Deep grasp of history rewriting, rebase vs merge trade-offs |
| Practical Skills | 25% | Safe rebase usage, proper amend technique, clean histories |
| Problem-Solving | 20% | Complex rebase conflicts, recovery from mistakes |
| Documentation | 10% | Professional-quality explanations and clear demonstrations |

**Minimum score to advance to Master of Universe level**: 80/100

### Critical Topics to Address

🔴 **History Rewriting**:
- Why is `git push --force` dangerous?
- How do you coordinate rebases in a team?
- What's the difference between `git reset`, `git revert`, and `git rebase`?
- When is interactive rebase the right tool?
- How do you recover from a bad rebase?

🔴 **Rebase vs Merge**:
- What's the fundamental difference in how they work?
- When should you choose rebase over merge?
- When should you choose merge over rebase?
- How does each affect the project history?
- What are the collaboration implications of each?

### Tips for Excellence

🎯 Show, don't just tell - include comprehensive command outputs  
🎯 Document commit SHAs before and after rewrites  
🎯 Create git log graphs showing history transformations  
🎯 Test rebase in different scenarios and document results  
🎯 Demonstrate both correct usage and common mistakes with recovery  
🎯 Include real-world scenarios where these techniques are valuable  

### Resources

- Git internals: https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain
- Rewriting history: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
- Git rebase: https://git-scm.com/docs/git-rebase
- Interactive rebase: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#_changing_multiple
- Rebase vs Merge: https://www.atlassian.com/git/tutorials/merging-vs-rebasing

---

**Next Steps**: Ready for the ultimate challenge? Move to the `master-of-the-universe` branch for expert-level exercises on branch protection rules and security best practices with GPG signing!

