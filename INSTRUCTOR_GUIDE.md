# Instructor Quick Start Guide

This guide helps instructors manage the Git training repository and evaluate student submissions.

---

## 📋 Repository Overview

### Branch Structure

| Branch | Purpose | Exercises |
|--------|---------|-----------|
| `main` | Overview, navigation, templates, evaluation criteria | N/A |
| `newbie` | Basic Git commands, branches, remote operations | 2 |
| `intermediate` | Merging, tags, stashing, multiple remotes | 3 |
| `master` | History rewriting, branching strategies, hooks | 3 |
| `master-of-the-universe` | Branch protection, GPG signing, security | 2 |

### Key Files in Main Branch

- **`README.md`**: Student-facing overview and submission instructions
- **`OUTCOME_TEMPLATE.md`**: Template for students to document their work
- **`EVALUATION_CRITERIA.md`**: Detailed rubric for grading (200+ point system)
- **`INSTRUCTOR_GUIDE.md`**: This file - setup and evaluation guidance
- **`MODEL_SPEC.MD`**: Original specification and requirements

---

## 🚀 Initial Setup

### 1. Push All Branches to Remote

```bash
# Push all exercise branches
git push origin main
git push origin newbie
git push origin intermediate
git push origin master
git push origin master-of-the-universe

# Optionally, set default branch protection on main
# (Configure via GitHub Settings → Branches)
```

### 2. Configure Repository Settings

**On GitHub**:

1. **Settings → General**:
   - Allow merge commits: ✅
   - Allow squash merging: ✅
   - Allow rebase merging: ✅
   
2. **Settings → Branches**:
   - Set `main` as default branch
   - Optionally protect `main` from direct pushes
   - Protect exercise branches (newbie, intermediate, master, master-of-the-universe)

3. **Settings → Collaborators** (if needed):
   - Add students as collaborators
   - Or use GitHub Classroom for automated setup

4. **Settings → Code security and analysis**:
   - Enable all security features (demonstrates Master of Universe concepts)

### 3. Create Organization (Optional)

For better management:
- Create GitHub organization for the course
- Fork/transfer repository to organization
- Use GitHub Classroom for automated student repository creation
- Enables better access management and analytics

---

## 👥 Student Group Management

### Group Naming Convention

Students work in groups (A, B, C, D, etc.) and create outcome branches:

```
group-A-outcomes/newbie
group-A-outcomes/intermediate
group-B-outcomes/newbie
group-C-outcomes/master
```

### Setting Up Student Groups

**Option 1: Manual Assignment**
- Assign students to groups (A, B, C, etc.)
- Students create their outcome branches following the naming convention

**Option 2: GitHub Classroom**
- Create assignment for each level
- Automatic repository creation per group
- Integrated grading interface

**Option 3: Forking Workflow**
- Students fork the repository
- Work in their forks
- Submit PRs back to main repository

---

## 📊 Evaluating Student Submissions

### Step 1: Locate Student Submissions

```bash
# Fetch all remote branches
git fetch --all

# List all outcome branches
git branch -r | grep outcomes

# Example output:
# origin/group-A-outcomes/newbie
# origin/group-A-outcomes/intermediate
# origin/group-B-outcomes/newbie
```

### Step 2: Review a Submission

```bash
# Checkout the student's outcome branch
git checkout group-A-outcomes/newbie

# Review their outcomes file
cat OUTCOMES.md

# Check their commit history
git log --oneline --graph --all

# For Master of Universe, verify signatures
git log --show-signature

# Review any artifacts (hooks, workflows)
ls -la hooks/ security-artifacts/
```

### Step 3: Verify Technical Execution

**For Newbie Level**:
```bash
# Check they have basic commits
git log --oneline | head -10

# Verify they understand branches
git branch -a

# Check for pushed branches
git ls-remote --heads origin | grep group-A
```

**For Intermediate Level**:
```bash
# Look for merge commits
git log --merges --oneline

# Check for tags
git tag -l

# Look for evidence of stash usage in their documentation
```

**For Master Level**:
```bash
# Check for rebased history (non-linear)
git log --graph --oneline --all

# Review hook scripts
cat hooks/pre-commit hooks/commit-msg

# Look for branching strategy evidence
git log --graph --oneline --all | head -30
```

**For Master of Universe**:
```bash
# CRITICAL: Verify GPG signatures
git log --show-signature | head -50

# Check security artifacts
ls security-artifacts/
cat security-artifacts/.gitignore

# Verify CODEOWNERS if present
cat CODEOWNERS
```

### Step 4: Score Using Rubric

Use `EVALUATION_CRITERIA.md` to score across five categories:

1. **Completion of Exercises** (20 points)
2. **Understanding of Concepts** (25 points)
3. **Practical Application** (25 points)
4. **Problem-Solving Skills** (20 points)
5. **Security Practices** (10 points - Master of Universe only)

### Step 5: Provide Feedback

Use the feedback template in `EVALUATION_CRITERIA.md`:

```bash
# Create feedback file
cat > feedback-group-A-newbie.md << 'EOF'
## Evaluation Feedback for Group A

**Level**: Newbie
**Date**: [Date]
**Evaluator**: [Your name]

### Overall Score: 85/100 - Grade: B

### Strengths:
- Excellent documentation of command outputs
- Clear understanding of staging area concept
- Well-organized commit history

### Areas for Improvement:
- Commit messages could be more descriptive
- Add more detail about SSH key configuration challenges
- Include more reflection on learning process

[... rest of feedback ...]
EOF

# Optionally post as PR comment or email
```

---

## 📈 Grading Scale

| Score | Grade | Assessment | Progression |
|-------|-------|------------|-------------|
| 90-100 | A | Outstanding | Ready for next level |
| 80-89 | B | Excellent | Ready for next level |
| 70-79 | C | Good | Ready for next level |
| 60-69 | D | Satisfactory | Additional practice recommended |
| 0-59 | F | Needs Improvement | Must redo |

### Progression Requirements

- **Newbie → Intermediate**: Minimum 70/100
- **Intermediate → Master**: Minimum 75/100
- **Master → Master of Universe**: Minimum 80/100
- **Training Completion**: Minimum 85/100

---

## 🔄 Common Workflows

### Reviewing Pull Requests

If students submit via PR:

1. Go to Pull Requests tab
2. Filter by label or branch name (group-X-outcomes/*)
3. Review the OUTCOMES.md file in Files Changed
4. Check commit history
5. Leave inline comments for specific issues
6. Use review tools: Comment, Approve, Request Changes
7. Merge when approved (or close if submitting for record only)

### Bulk Evaluation

```bash
#!/bin/bash
# Script to checkout and review all submissions

for branch in $(git branch -r | grep outcomes); do
    echo "=== Reviewing $branch ==="
    git checkout ${branch#origin/}
    
    # Check if OUTCOMES.md exists
    if [ -f OUTCOMES.md ]; then
        echo "Found OUTCOMES.md"
        # Extract key info (customize as needed)
        head -20 OUTCOMES.md
    else
        echo "WARNING: No OUTCOMES.md found"
    fi
    
    echo ""
done

git checkout main
```

### Providing Automated Feedback

Create a script to check common issues:

```bash
#!/bin/bash
# check-submission.sh

BRANCH=$1

git checkout $BRANCH

echo "Checking submission on branch: $BRANCH"

# Check for OUTCOMES.md
[ -f OUTCOMES.md ] || echo "❌ Missing OUTCOMES.md"

# Check for sufficient commits
COMMITS=$(git log --oneline | wc -l)
[ $COMMITS -gt 3 ] || echo "⚠️  Only $COMMITS commits (expected 3+)"

# Check commit messages
git log --format=%s | grep -q "^feat:\|^fix:\|^docs:" || echo "⚠️  Commit messages don't follow convention"

# For Master of Universe: Check signatures
if [[ $BRANCH == *"master-of-the-universe"* ]]; then
    SIGNED=$(git log --show-signature | grep -c "Good signature")
    [ $SIGNED -gt 0 ] || echo "❌ No GPG signed commits found"
fi

echo "✅ Basic checks complete"
```

---

## 📚 Teaching Tips

### Week-by-Week Suggested Schedule

**Week 1-2**: Newbie Level
- Lecture: Git fundamentals, three-tree architecture
- Lab: Exercises 1-2
- Assignment: Submit outcomes

**Week 3-4**: Intermediate Level
- Lecture: Collaboration workflows, merge strategies
- Lab: Exercises 1-3
- Assignment: Submit outcomes

**Week 5-6**: Master Level
- Lecture: Advanced Git, branching strategies
- Lab: Exercises 1-3
- Assignment: Submit outcomes

**Week 7-8**: Master of Universe Level
- Lecture: Git security, DevSecOps
- Lab: Exercises 1-2
- Assignment: Submit final outcomes

### Live Demos

Prepare demonstrations for:
- Resolving a merge conflict (intermediate)
- Interactive rebase workflow (master)
- Setting up GPG signing (master of universe)
- Removing sensitive data from history (master of universe)

### Common Student Questions

**Q: Can I use GitHub Desktop or other GUI tools?**
A: Encourage CLI for learning, but GUIs are acceptable for productivity once concepts are understood.

**Q: What if I make a mistake and need to start over?**
A: Mistakes are learning opportunities! Document them in the outcomes. Can reset/rebase if needed.

**Q: Do we need to complete all levels?**
A: Depends on course requirements. Minimum intermediate recommended for practical competency.

**Q: How much time should each level take?**
A: Newbie (1-2h), Intermediate (2-3h), Master (3-4h), Master of Universe (2-3h)

---

## 🛠️ Troubleshooting

### Students Can't Push

**Issue**: Permission denied or authentication failed

**Solutions**:
- Verify SSH keys configured: `ssh -T git@github.com`
- Check repository permissions (collaborator access)
- Ensure correct remote URL: `git remote -v`

### Outcome Branch Naming Errors

**Issue**: Students create incorrectly named branches

**Solution**:
```bash
# Rename branch locally
git branch -m old-name group-A-outcomes/newbie

# Delete old remote branch and push new one
git push origin :old-name
git push origin group-A-outcomes/newbie
```

### Missing Templates

**Issue**: Students can't find OUTCOME_TEMPLATE.md

**Solution**:
```bash
# They need to get it from main branch
git checkout main -- OUTCOME_TEMPLATE.md
```

### GPG Signing Issues (Master of Universe)

**Common Issues**:
- GPG key not configured: `git config --global user.signingkey`
- Email mismatch: Must match GitHub account email
- GPG agent not running: Restart or configure agent

**Debug Commands**:
```bash
gpg --list-keys
git config --global user.signingkey
git config --global user.email
```

---

## 📊 Analytics & Reporting

### Track Student Progress

```bash
# See all outcome branches
git branch -r | grep outcomes | sort

# Count submissions by level
git branch -r | grep outcomes | cut -d'/' -f2 | sort | uniq -c

# Check most recent activity
git for-each-ref --sort=-committerdate refs/remotes/origin/
```

### Generate Reports

Create a summary of all submissions:

```bash
#!/bin/bash
echo "# Training Progress Report"
echo "Generated: $(date)"
echo ""

for level in newbie intermediate master master-of-the-universe; do
    echo "## $level Level"
    COUNT=$(git branch -r | grep "outcomes/$level" | wc -l)
    echo "Submissions: $COUNT"
    git branch -r | grep "outcomes/$level"
    echo ""
done
```

---

## 📧 Communication Templates

### Welcome Email

```
Subject: Git Training Repository - Getting Started

Dear Students,

Welcome to the Git Technology training course!

Repository: https://github.com/miguel-oltra/taller-master-ugr

Please:
1. Clone the repository
2. Review README.md for overview
3. Choose your starting level (suggest: newbie)
4. Form groups (2-4 students)
5. Begin exercises

Groups should be named A, B, C, etc.

Questions? Office hours: [times]

Best regards,
[Your name]
```

### Submission Reminder

```
Subject: Reminder - [Level] Exercise Submission Due [Date]

Hi [Group],

Reminder: [Level] level outcomes are due [date].

Checklist:
☐ All exercises completed
☐ OUTCOMES.md filled out
☐ Outcome branch created: group-[X]-outcomes/[level]
☐ Pushed to remote
☐ PR created (if required)

Need help? Ask in [forum/office hours].

Best,
[Your name]
```

### Feedback Email

```
Subject: Feedback - Group [X] - [Level] Level

Hi Group [X],

I've reviewed your [level] submission. Great work!

Overall Score: [X]/100 - Grade: [Letter]

Key Strengths:
- [Strength 1]
- [Strength 2]

Areas to improve:
- [Area 1]
- [Area 2]

Detailed feedback: [link or attachment]

You're [approved/not approved] to progress to [next level].

Keep up the good work!

Best,
[Your name]
```

---

## 🎯 Best Practices for Instructors

✅ Review submissions within 1 week for timely feedback  
✅ Provide specific, actionable feedback (not just scores)  
✅ Encourage learning from mistakes, not just success  
✅ Share excellent examples (with permission) for others to learn  
✅ Hold office hours for Git troubleshooting  
✅ Create a class discussion forum (GitHub Discussions?)  
✅ Update exercises based on student feedback  
✅ Keep evaluation criteria consistent across groups  

---

## 📞 Support & Resources

**For Instructors**:
- Git Documentation: https://git-scm.com/doc
- GitHub Education: https://education.github.com/
- GitHub Classroom: https://classroom.github.com/

**For Students** (point them to):
- Repository README.md
- OUTCOME_TEMPLATE.md
- EVALUATION_CRITERIA.md
- Office hours and forums

---

**Last Updated**: November 29, 2025

**Questions or suggestions?** Update this guide or contact the course coordinator.
