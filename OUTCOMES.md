# Exercise Outcomes Submission Template

**Student/Group Name**: [Najib Bahij - group-02]  
**Level Completed**: [master]  
**Date**: [12/01/2026]

---

## 📋 Exercise Summary

### Exercise: [master]
**Status**: ✅ Completed

**What I did**:
[In that exercice I learned what is the amend and rebase commands.
Amend is when we do a commit and then we make a change so it helpes up to fuse those changes into the last commit with a new commit id, it basically helps us only with the last commit
rebase is kind of take the entire branch and move it to a new one, in our case, the change made in the branch master was moved to the feature branch and placed right before the last commit of the branch feature
]

**Commands Used**:
```bash
# List the key Git commands you used across all parts of the exercise
git add
git commit -m
git commit --amend -m # modifies the most recent commit
git log --oneline -n 3
git rebase -i HEAD~3 # opens editor to edit the last 3 commits
git rebase master # moves the current branch to start on top of the latest master branch commit

```

**Results/Output**:
```
echo "environment=production" >> config.txt
   git add config.txt
   git commit --amend -m "Add complete configuration file"
[master 5d5d0b0] Add complete configuration file

git log --oneline -n 3
5d5d0b0 (HEAD -> master) Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level

git rebase -i HEAD~3
Successfully rebased and updated refs/heads/master.
brahim@MacBook-Air taller-master-ugr % git log --oneline -n 5
7c5ab78 (HEAD -> master) Add feature B
8eb06d1 Add feature A
5d5d0b0 Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level

git rebase -i HEAD~3  
Successfully rebased and updated refs/heads/master.

brahim@MacBook-Air taller-master-ugr % git rebase master
Successfully rebased and updated refs/heads/feature/awesome-feature.
```

**Screenshots** (if applicable):
view screenshots folder, each screenshot has a descriptive title

---

## 🎯 Key Learnings

**Main concepts I learned**:
1. [Concept 1, "how to use amend command"]
2. [Concept 2, e.g., "how to use rebase command"]
3. [Concept 3, difference between merge and rebase]
4. [Concept 4, safe workflow]
5. [Concept 5, understand the difference between `git push --force` and `git push --force-with-lease`]
6. [Concept 6, dangers of rewriting public history and how to avoid them]

**Skills I improved**:
- [Skill 1, "when to use the amend command"]
- [Skill 2, "Resolving merge conflicts"]
- [Skill 3, "rebase branch"]

---

## 🚧 Challenges Faced

### Challenge 1: [amend command]
**Problem**: [to be honest, I didnt really understand the command amend and what it did]

**Solution**: [I asked gen ai, I could understand that this command helps with the last commit,it replaces the last commit with the changes made
the commit id was 144d8e2 named 'add configuration file' and then after the amend command, the commit id is 5d5d0b0 named 'add complete configuration file'
]

**Commands/Approach**:
```bash
echo "environment=production" >> config.txt
   git add config.txt
   git commit --amend -m "Add complete configuration file"

```

---

### Challenge 2: [the command rebase & fixup vs amend]
**Problem**: [then what does the command fixup actually do?]

**Solution**: [gen ai helped me understand that with the command git rebase -i HEAD~3 we could squash with fixup the commit 'fix typo' into 'add feature b' and give them a new id 
before rebase :
[master 8eb06d1] Add feature A
[master 5039a01] Add feature B
[master f581acc] Fix typo
after rebase:
7c5ab78 (HEAD -> master) Add feature B #was squashed with fix typo and the commit id is 7c5ab78
8eb06d1 Add feature A #didnt change
5d5d0b0 Add complete configuration file #didnt change

]

---

**Part 1 - Amending Commits**:
   - Commands used for amend operations : 
git commit --amend -m "Add complete configuration file"
   - Git log output before and after amend
before :
   git add config.txt
   git commit -m "Add configuration file"
   [master 144d8e2] Add configuration file
   1 file changed, 1 insertion(+)
   create mode 100644 config.txt

after:
echo "environment=production" >> config.txt
git add config.txt
git commit --amend -m "Add complete configuration file"
[master 5d5d0b0] Add complete configuration file
Date: Mon Jan 12 13:44:43 2026 +0100
1 file changed, 2 insertions(+)
create mode 100644 config.txt

for amend 2 : please view on screenshots folder amend2.1.ping and amend2.2.png
for amend 3 : please view on screenshots folder amend3.png

   - Comparison of commit SHAs to show history was rewritten
first amend :from 144d8e2 to 5d5d0b0
second amend : f927298d71ea6fb74279441b924167763136c993 to 6f92c4ae7b6d53c95b7ee895a870f3458790a4f0 ( please view on screenshots folder amend2.1.ping and amend2.2.png)
third amend : 6f92c4ae7b6d53c95b7ee895a870f3458790a4f0 to dce2c3a2463b1883ad85122f356c4ccbd450be0a ( please view screenshots amend3.png)

so basically amend function helps with replacing the commit id with a new clean one
   **Part 2 - Interactive Rebase**:
   - Commands and editor interactions for interactive rebase
the command : git rebase -i HEAD~3
On editor, we changed the word pick to fixup on the third line
   - Demonstration of fixup, reword, and other rebase operations
In the editor, on the line of the commit fix typo, we change the command pick to fixup to fusion it with the commit above it
   - Git log output showing cleaned-up history before and after
before : 
[master 8eb06d1] Add feature A
 1 file changed, 1 insertion(+)
 create mode 100644 featureA.txt
[master 5039a01] Add feature B
 1 file changed, 1 insertion(+)
 create mode 100644 featureB.txt
[master f581acc] Fix typo
 1 file changed, 1 insertion(+)

after:
7c5ab78 (HEAD -> master) Add feature B
8eb06d1 Add feature A
5d5d0b0 Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level

   **Part 3 - Rebasing a Branch**:
   - Commands for creating feature branch and rebasing onto master
command for creating feature branch : git checkout -b feature/awesome-feature
command for rebasing: git rebase master

   - `git log --graph --all --oneline` showing linear history after rebase :
d2d9d3e (HEAD -> feature/awesome-feature) Add awesome feature
4998875 (master) Update on master branch
7c5ab78 Add feature B
8eb06d1 Add feature A
5d5d0b0 Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level
f0055a0 Update README for master level exercises
74b9100 (origin/group-02-outcomes/intermediate, group-02-outcomes/intermediate) submitting work
db67cd4 screenshots
   - Explanation of how rebase differs from merge
merge doesn't rewrite history but rebase does :
Git cuts the branch from the original spot and pastes it on top of the latest main branch and commits moved get new Ids
   
   **Part 4 - Understanding Risks**:
   - Documentation of how commit SHAs change during rebase
during branch rebase the 'add awesome feature' commit id changed from 3277396 to d2d9d3e
before : 
git checkout -b feature/awesome-feature
   echo "Awesome Feature" > awesome.txt
   git add awesome.txt
   git commit -m "Add awesome feature"
Switched to a new branch 'feature/awesome-feature'
[feature/awesome-feature 3277396] Add awesome feature

after :

git log --graph --oneline --all -n 10
d2d9d3e (HEAD -> feature/awesome-feature) Add awesome feature
4998875 (master) Update on master branch
7c5ab78 Add feature B
8eb06d1 Add feature A
5d5d0b0 Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level
f0055a0 Update README for master level exercises
74b9100 (origin/group-02-outcomes/intermediate, group-02-outcomes/intermediate) submitting work
db67cd4 screenshots

   - Explanation of why rewriting public/shared history is dangerous
so as the commit id of 'add awesome feature' was 3277396, if my collegue were to pull the project and work on top of it, then I do a rebase so the commit id of 'add awesome feature' becomes d2d9d3e, so if my friend wants to commits his changes, it would be like he wants to commit on another commit that is inexistant
   - Best practices for safe history rewriting
best practice is to only rewrite history on branches only you are working on and that are not shared with other collegues
   - Difference between `--force` and `--force-with-lease`
--force make git overwrites the remote branch with your local changes without checking if others made push or not

--force-with-lease only proceeds if no one made some push commands, if not, it alerts you

3. **Advanced challenges documentation**:
   - Rebase conflicts: How did you resolve them?
there weren't any
   - Interactive rebase mistakes: Any issues? How did you recover?
no issues
   - Force push understanding: When to use `--force` vs `--force-with-lease`?
we can use --force when working on private branches only us are working on, otherwise we should use --force-with-ease
   - Real-world scenarios where you'd choose rebase over merge
In a local feature if there are typo, bugs to fix etc I can open the editor and squash them into one commit so that the reviewer sees it professional


4. **Deep reflection** (minimum 200 words):
   - When is it safe to rewrite history? When is it dangerous?
  
   - How does rebase help create clean, professional commit histories?
   - What's the fundamental difference between rebase and merge?
   - How would you implement history-rewriting workflows in a professional team setting?
   - Why is it important to never rewrite public/shared history?

it is safe to rewrite history if we are working on private branches but it s dangerous with working with public ones

Rebase helps us create a clean linear history because when you update your feature branch using git merge master, Git creates a generic commit saying „Merge branch ‚master‘ into ‚feature‘“. if you do this often then the history becomes cluttered. Rebase avoids this completely by simply moving your work on top of the new code, keeping the log focused purely on the actual changes

the fundamental difference between rebase and merge is that merge for example : if the main history is A -> B and that on my local feature I make a commit C, then it s A -> C, if I were to merge both of them, git merge would give A -> C where B is merged with Cbut with git rebase, let s say the commit is A, the concept is that, I make a commit C on top of it and at the same time if I forgot to add something before it, I can go to the main branch make the commit B and rebase my branch onto main to have A -> B -> C

In a local feature branch I could work and then make some mistakes, then I can use git rebase -i to fix the typosI can use git rebase main to make sure I m working with the latest changes from the team and then use —force-with-lease to not rewrite over noone’s code

we should not rewrite public/shared history because it changes the commit id that other team members are working on


## 💭 Personal Reflection

**What surprised me**:
[The concept of history rewriting and making the work clean and professional]

**What I found most difficult**:
[I had to do some efforts to reflect about what it s not recommended to rebase or rewrite history in public branches]

**What I found most useful**:
[the importance of rewriting in private branches and the use of --force-with-lease]

**How I would apply this in real projects**:
[In real projects I wouldnt rewrite or do rebase on branches my collegues are working on, I would work on a private branch, do amend to make the work clean and then if I want to push my work I would do it with --force-with-lease to not overwrite my collegue's work]

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic | Confidence (1-5) | Notes |
|-------|------------------|-------|
| Basic Git commands | [ 5] | |
| Branching & merging | [ 5] | |
| Remote operations | [5 ] | |
| Conflict resolution | [5 ] | |
| History rewriting | [5 ] | |
| Git hooks | [ 4] | |
| Security practices | [4 ] | |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:
- Link to your outcome branch: `https://github.com/miguel-oltra/taller-master-ugr/tree/group-X-outcomes/[level]`
- Key commits demonstrating your work:
  - Commit hash: [Short description]
  - Commit hash: [Short description]

**Additional files created** (if any):
- File 1: [Description]
- File 2: [Description]

---

## ✅ Completion Checklist

Before submitting, ensure you have:
- [ ] Completed the exercise for your chosen level (including all parts)
- [ ] Documented all commands used with their outputs
- [ ] Described challenges and how you resolved them
- [ ] Provided a thoughtful reflection on your learning
- [ ] Self-assessed your confidence in each topic
- [ ] Pushed your outcome branch to the remote repository
- [ ] Created a Pull Request (if required by your instructor)

---

## 📝 Additional Comments

[Any additional thoughts, questions, or feedback about the exercises]

---

**Submission Date**: [Date]  
**Ready for Review**: ✅ Yes / ❌ No
