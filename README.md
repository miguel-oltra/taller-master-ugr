# taller-master-ugr
A repository to showcase how GitHub works to master students

# Master of the Universe Level Exercises

Welcome to the Master of the Universe level! These expert-level exercises focus on repository security, branch protection, and professional best practices for team collaboration.

## Exercise 1 - Branch Protection Rules and Pull Request Workflows
**Objective**: Implement enterprise-grade branch protection and establish secure collaboration workflows.

**Tasks - Part A: Set Up Branch Protection on GitHub**:
1. Navigate to your repository on GitHub
2. Go to Settings → Branches → Add branch protection rule
3. Configure protection for the `main` branch:
   * Branch name pattern: `main`
   * ✅ Require a pull request before merging
   * ✅ Require approvals (at least 1)
   * ✅ Dismiss stale pull request approvals when new commits are pushed
   * ✅ Require review from Code Owners (create a CODEOWNERS file)
   * ✅ Require status checks to pass before merging
   * ✅ Require branches to be up to date before merging
   * ✅ Require conversation resolution before merging
   * ✅ Include administrators (enforce rules on admins too)

4. Create a `CODEOWNERS` file in the repository root:
   ```bash
   # CODEOWNERS file
   # These owners will be requested for review when someone opens a PR
   
   # Global owners
   * @your-username
   
   # Specific directory owners
   /docs/ @doc-team
   /src/security/ @security-team
   *.sql @database-team
   ```

**Tasks - Part B: Protected Branch Workflow**:
1. Try to push directly to main (should be blocked):
   ```bash
   git checkout main
   echo "test" > direct-push.txt
   git add direct-push.txt
   git commit -m "Attempting direct push"
   git push origin main  # This should fail!
   ```

2. Proper workflow - create a PR:
   ```bash
   git checkout -b feature/protected-workflow
   echo "Proper workflow" > workflow.txt
   git add workflow.txt
   git commit -m "feat: Add workflow documentation"
   git push origin feature/protected-workflow
   ```

3. On GitHub:
   * Create a Pull Request
   * Request reviews from required reviewers
   * Wait for status checks (CI/CD) to pass
   * Address review comments
   * Get required approvals
   * Merge using the appropriate strategy (squash, rebase, or merge)

**Tasks - Part C: Implement Status Checks**:
1. Create a GitHub Actions workflow for status checks (`.github/workflows/pr-checks.yml`):
   ```yaml
   name: PR Checks
   
   on:
     pull_request:
       branches: [ main ]
   
   jobs:
     lint:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         - name: Run linters
           run: echo "Running linters..."
     
     test:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
         - name: Run tests
           run: echo "Running tests..."
   ```

**Success Criteria**:
- Main branch is protected and cannot accept direct pushes
- All changes must go through Pull Request review
- Code owners are automatically requested for review
- Status checks must pass before merging
- You understand the balance between security and workflow efficiency

## Exercise 2 - Security Best Practices: GPG Signing and Sensitive Data Management
**Objective**: Implement commit signing for verified commits and learn to manage sensitive data securely.

**Tasks - Part A: Set Up GPG Commit Signing**:
1. Generate a GPG key:
   * Follow: [Generate GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
   ```bash
   gpg --full-generate-key
   # Choose: RSA and RSA, 4096 bits, no expiration (or set expiration)
   # Enter your name and email (must match GitHub email)
   ```

2. List your GPG keys:
   ```bash
   gpg --list-secret-keys --keyid-format=long
   ```

3. Export your GPG public key:
   ```bash
   gpg --armor --export YOUR_KEY_ID
   ```

4. Add GPG key to GitHub:
   * Go to GitHub Settings → SSH and GPG keys → New GPG key
   * Paste your public key
   * [Add GPG key to GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account)

5. Configure Git to use your GPG key:
   ```bash
   git config --global user.signingkey YOUR_KEY_ID
   git config --global commit.gpgsign true
   ```
   * [Tell Git about signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)

6. Associate email with GPG key:
   * [Associate email with GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/associating-an-email-with-your-gpg-key)

7. Make a signed commit:
   ```bash
   echo "Signed commit test" > signed.txt
   git add signed.txt
   git commit -S -m "feat: Add signed commit test"
   git log --show-signature -1
   ```

8. Push and verify on GitHub (should show "Verified" badge)

**Tasks - Part B: Managing Sensitive Data**:
1. **Prevention** - Create `.gitignore` to prevent accidental commits:
   ```bash
   # .gitignore
   .env
   .env.local
   config/secrets.yml
   *.key
   *.pem
   credentials.json
   ```

2. **Detection** - Use git-secrets or similar tools:
   ```bash
   # Install git-secrets
   git secrets --install
   git secrets --register-aws
   ```

3. **Remediation** - Remove accidentally committed secrets:
   
   **Option A: Using git-filter-repo (recommended)**
   ```bash
   # Install git-filter-repo
   pip install git-filter-repo
   
   # Remove sensitive file from history
   git filter-repo --path config/secrets.yml --invert-paths
   
   # Force push (WARNING: coordinate with team!)
   git push origin --force --all
   ```
   
   **Option B: Using BFG Repo-Cleaner**
   ```bash
   # Download BFG
   # Remove file
   bfg --delete-files secrets.yml
   git reflog expire --expire=now --all
   git gc --prune=now --aggressive
   ```

4. **Best Practices**:
   * Use environment variables for secrets
   * Use secret management tools (HashiCorp Vault, AWS Secrets Manager)
   * Use GitHub Secrets for CI/CD
   * Rotate any exposed credentials immediately
   * Enable secret scanning on GitHub

**Tasks - Part C: Security Audit**:
1. Review your repository for security issues:
   ```bash
   # Check for large files
   git rev-list --objects --all | \
     git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
     sed -n 's/^blob //p' | \
     sort --numeric-sort --key=2 | \
     tail -n 10
   
   # Check for sensitive patterns in history
   git log -p | grep -i "password\|api_key\|secret"
   ```

2. Enable GitHub security features:
   * Go to Settings → Code security and analysis
   * Enable: Dependency graph
   * Enable: Dependabot alerts
   * Enable: Dependabot security updates
   * Enable: Secret scanning
   * Enable: Code scanning (GitHub Advanced Security)

**Success Criteria**:
- All your commits are GPG signed and show "Verified" on GitHub
- You have a comprehensive `.gitignore` file
- You can identify and remove sensitive data from Git history
- You understand prevention, detection, and remediation of security issues
- Repository has all available security features enabled
- You can perform a security audit of a repository

---

## 📤 Submitting Your Work

### 🌟 Congratulations on Reaching Master of the Universe Level! 🌟

You're demonstrating elite-level Git expertise with enterprise security practices. This final submission showcases your professional readiness.

### Step 1: Create Your Outcome Branch

```bash
git checkout master-of-the-universe
git checkout -b group-X-outcomes/master-of-the-universe
```

### Step 2: Document Your Outcomes

1. **Get the template**:
   ```bash
   git checkout main -- OUTCOME_TEMPLATE.md
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   ```

2. **Complete comprehensive documentation**:

   **Exercise 1 - Branch Protection & Workflows**:
   
   - **Branch Protection Configuration**:
     - Screenshots of GitHub branch protection settings
     - Explanation of each protection rule enabled
     - Documentation of CODEOWNERS file
     - Status checks configuration
   
   - **Protected Branch Workflow**:
     - Demonstration of blocked direct push (screenshot/output)
     - Complete PR workflow documentation
     - PR review process
     - Status check results
     - Merge strategy chosen and why
   
   - **GitHub Actions Workflow**:
     - Complete `.github/workflows/pr-checks.yml` file
     - Workflow run results (screenshots)
     - Explanation of each check
   
   **Exercise 2 - Security Best Practices**:
   
   - **GPG Setup (Critical)**:
     - GPG key generation output (redact key ID if public)
     - GitHub GPG key configuration screenshots
     - Git configuration commands
     - `git log --show-signature` output showing verified commits
     - Multiple signed commits demonstrating consistency
   
   - **Sensitive Data Management**:
     - Comprehensive `.gitignore` file content
     - Documentation of files/patterns excluded
     - Demonstration of secret detection (if using tools)
     - Sensitive data removal demonstration:
       - Before: Evidence of "sensitive" data in history
       - Commands used (git-filter-repo or BFG)
       - After: Clean history verification
   
   - **Security Audit**:
     - Repository security scan results
     - Large file analysis output
     - Pattern search for potential secrets
     - GitHub security features enabled (screenshots)
     - Security recommendations document

3. **Security-focused challenges**:
   - GPG configuration issues across OS/platforms?
   - Difficulties with commit signing in IDE/editor?
   - Challenges removing sensitive data from complex history?
   - Branch protection limitations or conflicts with workflow?
   - Balancing security with developer productivity?

4. **Professional reflection** (minimum 250 words):
   - Why is commit verification critical in enterprise environments?
   - How do branch protection rules prevent security incidents?
   - What's your strategy for secret management in real projects?
   - How would you implement these practices in your organization?
   - What trade-offs exist between security and velocity?
   - How do these practices integrate with DevSecOps principles?

### Step 3: Package Security Artifacts

Create organized security documentation:

```bash
mkdir security-artifacts
cp .gitignore security-artifacts/
cp .github/workflows/pr-checks.yml security-artifacts/ 2>/dev/null || echo "No workflow file"
# Export your public GPG key
gpg --armor --export YOUR_KEY_ID > security-artifacts/public-key.asc
git add security-artifacts/
```

### Step 4: Commit and Push (With Signature!)

```bash
git add OUTCOMES.md security-artifacts/
git commit -S -m "docs: Add master-of-the-universe level exercise outcomes for Group X"
git log --show-signature -1  # Verify signature
git push origin group-X-outcomes/master-of-the-universe
```

### What to Include

✅ **Exercise 1 Requirements**:
- Complete branch protection configuration with screenshots
- CODEOWNERS file with meaningful entries
- Working GitHub Actions workflow
- Documented PR workflow from creation to merge
- Evidence of blocked direct pushes
- Status check execution results
- Discussion of appropriate merge strategies

✅ **Exercise 2 Requirements**:
- GPG key successfully configured and verified
- Minimum 5 signed commits showing "Verified" badge
- Comprehensive `.gitignore` (50+ entries recommended)
- Successful sensitive data removal demonstration
- Security audit with findings and recommendations
- All GitHub security features documented
- Public GPG key exported in security-artifacts/

✅ **Security Best Practices Demonstrated**:
- All submission commits are GPG signed
- No secrets in repository (even test/dummy ones)
- Professional `.gitignore` covering common scenarios
- Security-first mindset in all documentation
- Proactive security measures explained

✅ **General Requirements**:
- Professional-quality documentation (250+ word reflection)
- Screenshots of all GitHub configurations
- Complete command history with outputs
- Security artifacts packaged properly
- Self-assessment including security topics
- Clear explanations of security trade-offs

### Evaluation Criteria

| Criterion | Weight | Key Focus for Master of Universe |
|-----------|--------|-----------------------------------|
| Completion | 20% | All exercises with enterprise-grade implementations |
| Understanding | 25% | Deep security knowledge, policy implications, trade-offs |
| Practical Skills | 25% | Working GPG, proper protections, security tooling |
| Problem-Solving | 20% | Security issues, configuration challenges, policy design |
| **Security Practices** | 10% | Commit signing, secret management, audit capabilities |

**Minimum score to complete training**: 85/100

### Critical Security Topics

🔐 **Commit Signing**:
- Why does commit signing matter for supply chain security?
- What attacks does GPG signing prevent?
- How do you verify someone else's signed commits?
- What happens if you lose your GPG key?

🔐 **Branch Protection**:
- How do protection rules prevent unauthorized changes?
- What's the minimum viable set of protections?
- How do you balance security with emergency fixes?
- What are the limitations of branch protection?

🔐 **Secret Management**:
- Why is removing secrets from history insufficient?
- What's your secret rotation strategy after exposure?
- How do you prevent secrets in commits (pre-commit hooks)?
- What tools help detect secrets in repositories?

🔐 **Security Audit**:
- What are the top security risks in Git repositories?
- How do you conduct a comprehensive security review?
- What GitHub security features are most important?
- How does Git security fit into DevSecOps?

### Excellence Indicators

💎 GPG key configured with expiration and backup plan  
💎 Branch protection rules follow industry best practices  
💎 `.gitignore` includes security-sensitive patterns  
💎 Secret detection automated (pre-commit hooks)  
💎 Comprehensive security audit with prioritized findings  
💎 Documentation includes threat models and mitigations  
💎 All security practices explained with real-world context  

### Common Pitfalls to Avoid

⚠️ Unsigned commits in submission (must be signed!)  
⚠️ Weak or incomplete branch protection rules  
⚠️ Generic `.gitignore` without security focus  
⚠️ Not actually removing sensitive data, just hiding it  
⚠️ GPG key without email matching GitHub  
⚠️ Security theater without understanding the "why"  

### Resources

- Commit signature verification: https://docs.github.com/en/authentication/managing-commit-signature-verification
- Branch protection: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches
- GitHub security features: https://docs.github.com/en/code-security
- Git-filter-repo: https://github.com/newren/git-filter-repo
- BFG Repo-Cleaner: https://rtyley.github.io/bfg-repo-cleaner/
- OWASP Git Security: https://owasp.org/www-community/attacks/Git

---

## 🎓 Training Completion

**Congratulations!** 🎉 You've completed all levels of Git mastery. You now have the skills to work professionally with Git in enterprise environments, manage complex workflows, and maintain security best practices.

### What You've Achieved

✨ **Newbie**: Mastered Git fundamentals and basic workflows  
✨ **Intermediate**: Conquered merging, conflicts, and collaboration  
✨ **Master**: Mastered history rewriting, branching strategies, and automation  
✨ **Master of Universe**: Achieved enterprise-level security and governance expertise  

### Your Professional Git Portfolio

Your completed outcome branches demonstrate:
- ✅ Technical proficiency across all Git features
- ✅ Problem-solving abilities in complex scenarios
- ✅ Security-first mindset and best practices
- ✅ Professional documentation and communication skills
- ✅ Ready for enterprise Git workflows

### Next Steps

**Continue Learning**:
- 🚀 Practice these skills in real projects
- 🚀 Contribute to open-source projects on GitHub
- 🚀 Learn about GitOps and Infrastructure as Code
- 🚀 Explore CI/CD integration with Git workflows
- 🚀 Study advanced topics: Git LFS, submodules, subtrees
- 🚀 Share your knowledge with others through mentoring

**Professional Development**:
- Add Git expertise to your CV/resume
- Share your learning journey on LinkedIn
- Write blog posts about complex Git topics
- Contribute to Git-related projects or documentation

**Stay Current**:
- Follow Git release notes and new features
- Join Git communities and forums
- Attend conferences or meetups about version control
- Explore emerging tools in the Git ecosystem

---

**Thank you for completing this training!** Your dedication to mastering Git will serve you well in your professional career. 🌟

