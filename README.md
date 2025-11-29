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

---

## 📤 Submitting Your Work

### Congratulations on completing the Newbie Level! 🎉

Now it's time to document and submit your work for evaluation.

### Step 1: Create Your Outcome Branch

From the newbie branch, create your group's outcome branch:

```bash
# Make sure you're on the newbie branch
git checkout newbie

# Create your outcome branch (replace X with your group letter: A, B, C, etc.)
git checkout -b group-X-outcomes/newbie
```

**Example**: If you're in Group A:
```bash
git checkout -b group-A-outcomes/newbie
```

### Step 2: Document Your Outcomes

1. **Copy the outcome template**:
   ```bash
   git checkout main -- OUTCOME_TEMPLATE.md
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   ```

2. **Fill out `OUTCOMES.md`** with:
   - **Exercise 1 Documentation**:
     - Commands you used (config, clone, add, commit, status, log)
     - Output from `git log` showing your commits
     - Screenshot or output of `git status`
   
   - **Exercise 2 Documentation**:
     - Commands for creating and switching branches
     - Output from `git branch -a` showing your branches
     - Output from `git log --oneline --graph --all`
     - Screenshot showing your branch on GitHub
   
   - **Challenges & Solutions**:
     - Did you have SSH key issues? How did you resolve them?
     - Any confusion about staging vs. committing?
     - Problems with push/pull?
   
   - **Reflection**:
     - What did you learn about the three-tree architecture (working dir, staging, repo)?
     - When would you use branches in real projects?
     - What's the difference between local and remote repositories?

### Step 3: Commit Your Documentation

```bash
git add OUTCOMES.md
git commit -m "docs: Add newbie level exercise outcomes for Group X"
```

### Step 4: Push to Remote

```bash
git push origin group-X-outcomes/newbie
```

### Step 5: Create a Pull Request (Optional)

If your instructor requires it:
1. Go to https://github.com/miguel-oltra/taller-master-ugr
2. Click "Pull Requests" → "New Pull Request"
3. Select your branch: `group-X-outcomes/newbie` → `main`
4. Title: "Outcomes: Group X - Newbie Level"
5. Add description with any questions or comments
6. Submit for review

### What to Include in Your Documentation

✅ **For Exercise 1**:
- Git configuration commands
- Clone command and output
- At least 3 commits demonstrating add/commit workflow
- Git log output
- Git status at different stages

✅ **For Exercise 2**:
- Branch creation commands
- Output showing local and remote branches
- Push command and confirmation
- Pull command and output
- Evidence of successful remote operations

✅ **General Requirements**:
- All commands with their full output
- Screenshots of key steps (optional but recommended)
- Explanation of any errors encountered
- Reflection on what you learned (minimum 100 words)
- Self-assessment of confidence (1-5 scale) for each topic

### Evaluation Criteria

Your newbie level work will be evaluated on:

| Criterion | Weight | What We're Looking For |
|-----------|--------|------------------------|
| Completion | 20% | All exercises finished with documentation |
| Understanding | 25% | Clear grasp of Git basics, staging area, branches |
| Practical Skills | 25% | Correct use of commands, clean commit history |
| Problem-Solving | 20% | How you handled challenges and learned from them |
| Documentation | 10% | Clear, complete, and well-organized submission |

**Minimum score to advance to Intermediate level**: 70/100

See `EVALUATION_CRITERIA.md` in the main branch for complete rubric.

### Tips for Success

💡 Save all command outputs as you work  
💡 Take screenshots of important steps  
💡 Write notes about challenges immediately when they occur  
💡 Be honest about difficulties - that shows learning!  
💡 Ask questions if something isn't clear  

### Need Help?

- Review `OUTCOME_TEMPLATE.md` for detailed guidance
- Check `EVALUATION_CRITERIA.md` for expectations
- Ask your instructor or group members
- Review Git documentation: https://git-scm.com/doc

---

**Next Steps**: Once you've completed these exercises, you're ready to move to the `intermediate` branch for more challenging tasks!

