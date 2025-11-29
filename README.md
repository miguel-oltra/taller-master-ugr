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

**Congratulations!** 🎉 You've completed all levels of Git mastery. You now have the skills to work professionally with Git in enterprise environments, manage complex workflows, and maintain security best practices.

**Next Steps**:
- Practice these skills in real projects
- Contribute to open-source projects
- Learn about GitOps and Infrastructure as Code
- Explore CI/CD integration with Git workflows
- Share your knowledge with others!

