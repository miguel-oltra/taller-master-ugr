# Purpose
I am doing a lecture class to master students at the university wit a focus on Git Technology and want to setup in github.com an organization and a repository so the trainees can do some exercises to demonstrate their competences. Hence different levels of exercises I want them as a trainer they need to pass with four levels of complexity (newbie, intermediate, master, and master of the universe)

# Specification
- Repository URL for the exercises: https://github.com/miguel-oltra/taller-master-ugr
- Training content 
   - Git Key Features
        - How it works (local server) (commits, working tree, staging area, references)
        - Branching
        - How it works (remote server) (push, pull, fetch, clone, references)
        - Visualize the log
        - Introduction to branching strategies
        - Visualize remote server
        - Exercises using (https://learngitbranching.js.org/?NODEMO)
        - Rewriting history (modify a message, uncommit, rewing history, remove sensitive data, avoid impersonation) 
        - Hooks (pre-commit, post-commit, pre-push, pre-receive, post-receive)
        - Configure SSH keys, GPG keys
        - Collaboration workflows - Git workflows (Github lightweight workflow, Github lightweight workflow forking, Gitflow, Gitlab flow, )
        - Digital Trends - Everything as Code (GitOps, IaC, CI/CD, DevSecOps)
   
   
   
   - Levels of exercises
        - Newbie - 2 exercises
            - Basic git commands (init, clone, add, commit, status, log)
            - Create and switch branches
            - Basic remote operations (push, pull)
        - Intermediate - 3 exercises
            - Merging branches and resolving conflicts
            - Using tags
            - Stashing changes
            - Working with remotes (adding/removing remotes)
        - Master - 3 exercises
            - Rewriting history (rebase, amend commits)
            - Advanced branching strategies
            - Using hooks            
        - Master of the Universe - 2 exercises
            - Branch protection rules
            - Security best practices (GPG signing, managing sensitive data) - verified commits
            
# Repository Structure

## PROMPT 1 - Repository Structure and branches for exercises
GIVEN  the MODEL_SPEC.MD file that describes the purpose and specification of a Git training repository with different levels of exercises
WHEN  creating the repository structure
THEN  create the following branches in the local repository:
  - main: The default branch containing the final version of the exercises.
  - newbie: A branch for newbie-level exercises.
  - intermediate: A branch for intermediate-level exercises.
  - master: A branch for master-level exercises.
  - master-of-the-universe: A branch for master-of-the-universe-level exercises.

THEN  update the README.md file in each branch to include only the exercises relevant to that level, ensuring that each branch contains a clear and concise description of the exercises to be completed at that level.

## PROMPT 2 - Outcome of the results to evaluate the alumni
GIVEN  the MODEL_SPEC.MD file that describes the purpose and specification of a Git training
GIVEN the README.md file that describes the structure of the training repository with different levels of exercises
WHEN  evaluating the alumni who have completed the Git training exercises
THEN  use the following criteria to assess their performance:
  - Completion of Exercises: Verify that the alumni have completed all exercises in their chosen difficulty level branch.
  - Understanding of Concepts: Assess their understanding of key Git concepts covered in the exercises, such as branching, merging, and rewriting history.
  - Practical Application: Evaluate their ability to apply Git commands and workflows effectively in real-world scenarios.
  - Problem-Solving Skills: Review how well they handled challenges such as merge conflicts and history rewriting.
  - Security Practices: For those who completed the Master of the Universe level, assess their knowledge of security best practices, including GPG signing and managing sensitive data.

THEN  provide feedback based on these criteria to help alumni improve their Git skills further.
THEN evolve all the training so each group (A, B, C, ...)of trainess can showcase their outcomes of each exercise in a dedicated branch named  `group-X-outcomes/<level>` where `<level>` is the difficulty level they completed (e.g., `group-X-outcomes/newbie`, `group-X-outcomes/intermediate`, etc.).
THEN ensure that each outcome branch contains:
  - A summary of the exercises completed.
  - Screenshots or logs demonstrating the commands used and their results.
  - A reflection on what they learned and any challenges faced during the exercises.

THEN evolve the README.md file in the main branch and the exercises branches to include a section on how alumni can create and submit their outcome branches for review.
