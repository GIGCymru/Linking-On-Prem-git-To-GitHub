# Linking On-Premise Git Repositories to GitHub - NHS Wales Guide

A comprehensive guide for NHS Wales users on how to link their on-premise git repositories (hosted on local shared drives, SharePoint, or other internal systems) to GitHub.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [NHS Wales Specific Considerations](#nhs-wales-specific-considerations)
3. [Command Line Approach](#command-line-approach)
4. [GitHub Desktop Application](#github-desktop-application)
5. [On-Premise DevOps Integration](#on-premise-devops-integration)
6. [Troubleshooting](#troubleshooting)
7. [Best Practices](#best-practices)
8. [Support and Resources](#support-and-resources)

---

## Prerequisites

Before you begin, ensure you have:

- **Git installed** on your local machine
- **GitHub account** with appropriate permissions
- **Access to your on-premise git repository**
- **Network access** to GitHub.com (check with your IT team if behind corporate firewall)
- **Appropriate permissions** from your line manager and IT security team

### Required Software

- Git (version 2.20 or later recommended)
- Text editor (VS Code, Notepad++, etc.)
- GitHub Desktop (optional, for GUI approach)
- Terminal/Command Prompt access

---

## NHS Wales Specific Considerations

### Security and Compliance

⚠️ **Important**: Before linking any NHS Wales repositories to GitHub, ensure you have:

1. **Approval from your Information Governance team**
2. **Reviewed data classification** of your repository contents
3. **Ensured no patient data** or sensitive information is included
4. **Followed NHS Wales IT security policies**
5. **Considered using GitHub Enterprise** for additional security features

### Data Protection

- Never commit patient data, personal information, or sensitive NHS data
- Use `.gitignore` files to exclude configuration files with sensitive information
- Regularly audit your repository contents
- Consider using private repositories for internal NHS Wales projects

### Network Considerations

NHS Wales networks may have specific firewall rules. Contact your IT support if you experience connectivity issues with:
- `github.com`
- `api.github.com`
- Git over HTTPS (port 443) or SSH (port 22)

---

## Command Line Approach

### Scenario 1: Existing Git Repository on Local Drive/SharePoint

If you already have a git repository on your local drive or SharePoint that you want to link to GitHub:

#### Step 1: Navigate to Your Repository

```bash
# Navigate to your existing git repository
cd /path/to/your/existing/repo

# Verify it's a git repository
git status
```

#### Step 2: Create a New Repository on GitHub

1. Go to [GitHub.com](https://github.com)
2. Click the "+" icon in the top right corner
3. Select "New repository"
4. Enter repository name (preferably matching your local repo name)
5. Choose visibility (Public/Private - recommend Private for NHS Wales projects)
6. **Do NOT initialize with README, .gitignore, or license** if you have existing content
7. Click "Create repository"

#### Step 3: Add GitHub as Remote Origin

```bash
# Add GitHub repository as remote origin
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git

# Verify remote was added
git remote -v
```

#### Step 4: Set Up Authentication

**Option A: Personal Access Token (Recommended for HTTPS)**

```bash
# Configure Git with your credentials
git config --global user.name "Your Name"
git config --global user.email "your.email@wales.nhs.uk"

# When prompted for password, use your Personal Access Token
# Create token at: https://github.com/settings/tokens
```

**Option B: SSH Key (More Secure)**

```bash
# Generate SSH key (if you don't have one)
ssh-keygen -t ed25519 -C "your.email@wales.nhs.uk"

# Add SSH key to ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard (Windows)
clip < ~/.ssh/id_ed25519.pub

# Copy public key to clipboard (Mac)
pbcopy < ~/.ssh/id_ed25519.pub

# Copy public key to clipboard (Linux)
cat ~/.ssh/id_ed25519.pub
```

Then add the public key to your GitHub account:
1. Go to GitHub Settings → SSH and GPG keys
2. Click "New SSH key"
3. Paste your public key
4. Click "Add SSH key"

```bash
# Update remote to use SSH
git remote set-url origin git@github.com:YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
```

#### Step 5: Push Your Repository to GitHub

```bash
# Push your main branch to GitHub
git branch -M main
git push -u origin main

# Push any other branches
git push --all origin

# Push tags if you have any
git push --tags origin
```

### Scenario 2: Starting Fresh - No Existing Git Repository

If your code is in a folder that's not yet a git repository:

#### Step 1: Initialize Git Repository

```bash
# Navigate to your project folder
cd /path/to/your/project

# Initialize git repository
git init

# Add all files to tracking
git add .

# Create initial commit
git commit -m "Initial commit"
```

#### Step 2: Follow Steps 2-5 from Scenario 1

Continue with creating GitHub repository and linking as described above.

### Scenario 3: SharePoint Integration

For repositories stored on SharePoint:

#### Step 1: Sync SharePoint to Local Drive

```bash
# If using SharePoint sync client, navigate to synced folder
cd "C:\Users\%USERNAME%\OneDrive - NHS Wales\Your-Project-Folder"

# Or map SharePoint as network drive
# \\your-sharepoint-site.sharepoint.com\sites\your-site\Shared Documents\Your-Project
```

#### Step 2: Follow Standard Process

Once you have local access, follow the same steps as Scenario 1 or 2.

### Common Git Commands for Ongoing Work

```bash
# Check repository status
git status

# Pull latest changes from GitHub
git pull origin main

# Add and commit changes
git add .
git commit -m "Descriptive commit message"

# Push changes to GitHub
git push origin main

# Create and switch to new branch
git checkout -b feature-branch-name

# Switch between branches
git checkout main
git checkout feature-branch-name

# Merge branch into main
git checkout main
git merge feature-branch-name

# Delete local branch
git branch -d feature-branch-name

# Delete remote branch
git push origin --delete feature-branch-name
```

---

## GitHub Desktop Application

GitHub Desktop provides a user-friendly graphical interface for managing git repositories. This section covers how to use it for linking on-premise repositories to GitHub.

### Installation and Setup

#### Step 1: Download and Install GitHub Desktop

1. Download from [desktop.github.com](https://desktop.github.com/)
2. Install following your organization's software installation procedures
3. Launch GitHub Desktop

#### Step 2: Sign In to GitHub

1. Click "Sign in to GitHub.com"
2. Enter your GitHub credentials
3. Authorize GitHub Desktop

### Linking Existing Repository

#### Option 1: Add Existing Repository from Local Drive

1. **File** → **Add Local Repository**
2. Browse to your on-premise repository folder
3. Click **Add Repository**

If Git is not initialized:
1. Click **Create a repository** instead
2. Choose **Local path** pointing to your project folder
3. Fill in repository details
4. Click **Create Repository**

#### Option 2: Clone from GitHub (if repository already exists on GitHub)

1. **File** → **Clone Repository**
2. Select **GitHub.com** tab
3. Choose your repository from the list
4. Select local path (e.g., your SharePoint synced folder)
5. Click **Clone**

### Publishing to GitHub

If you added a local repository that doesn't exist on GitHub yet:

1. Click **Publish repository** in the top toolbar
2. Choose repository name
3. Add description (optional)
4. Select **Keep this code private** for NHS Wales projects
5. Choose organization (if applicable)
6. Click **Publish repository**

### Daily Workflow with GitHub Desktop

#### Making Changes

1. Edit your files in your preferred editor
2. Return to GitHub Desktop
3. Review changes in the **Changes** tab
4. Enter commit message in the summary field
5. Add description if needed
6. Click **Commit to main**

#### Syncing with GitHub

1. Click **Push origin** to upload your commits
2. Click **Fetch origin** to check for remote changes
3. Click **Pull origin** if there are remote changes to download

#### Branch Management

**Creating a New Branch:**
1. Click **Current branch** dropdown
2. Click **New branch**
3. Enter branch name
4. Click **Create branch**

**Switching Branches:**
1. Click **Current branch** dropdown
2. Select desired branch from list

**Merging Branches:**
1. Switch to main branch
2. Click **Current branch** dropdown
3. Click **Choose a branch to merge into main**
4. Select branch to merge
5. Click **Merge**

### SharePoint Integration with GitHub Desktop

#### Method 1: SharePoint Sync Folder

1. Ensure SharePoint folder is synced to local drive
2. Use **Add Local Repository** to add the synced folder
3. GitHub Desktop will manage the repository in the synced location
4. Changes sync automatically to SharePoint and can be pushed to GitHub

#### Method 2: Traditional Workflow

1. Keep your main working copy in a regular local folder
2. Use GitHub Desktop for version control and GitHub synchronization
3. Manually copy finalized versions to SharePoint as needed

### Advanced Features

#### Viewing History

1. Click **History** tab
2. Browse commits and see changes
3. Right-click commits for options like revert

#### Handling Conflicts

When merge conflicts occur:
1. GitHub Desktop will highlight conflicted files
2. Click **Open in External Editor**
3. Resolve conflicts in your preferred editor
4. Save files
5. Return to GitHub Desktop and commit resolved changes

#### Settings and Preferences

Access via **File** → **Options** (Windows) or **GitHub Desktop** → **Preferences** (Mac):

- **Git** tab: Configure name and email
- **Appearance**: Choose theme
- **Advanced**: Configure external editor and shell

---

## On-Premise DevOps Integration

This section covers integrating your on-premise DevOps processes with GitHub while maintaining NHS Wales compliance and security standards.

### Azure DevOps Integration

Many NHS Wales organizations use Azure DevOps. Here's how to integrate with GitHub:

#### Option 1: GitHub Actions with Azure DevOps

```yaml
# .github/workflows/azure-devops-integration.yml
name: Azure DevOps Integration

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  trigger-azure-pipeline:
    runs-on: ubuntu-latest
    steps:
    - name: Trigger Azure DevOps Pipeline
      uses: Azure/pipelines@v1
      with:
        azure-devops-project-url: 'https://dev.azure.com/yourorg/yourproject'
        azure-pipeline-name: 'YourPipelineName'
        azure-devops-token: ${{ secrets.AZURE_DEVOPS_TOKEN }}
```

#### Option 2: Mirror Repositories

**Set up automatic mirroring from GitHub to Azure DevOps:**

```bash
# Add Azure DevOps as additional remote
git remote add azure-devops https://yourorg@dev.azure.com/yourorg/yourproject/_git/yourrepo

# Push to both remotes
git push origin main
git push azure-devops main

# Create script for automatic dual push
# save as push-both.sh
#!/bin/bash
git push origin "$1"
git push azure-devops "$1"
```

### Jenkins Integration

For organizations using Jenkins for CI/CD:

#### GitHub Webhook Configuration

1. **In GitHub Repository:**
   - Go to Settings → Webhooks
   - Add webhook URL: `http://your-jenkins-server/github-webhook/`
   - Select events: Push, Pull requests
   - Add webhook

2. **In Jenkins:**
   - Install GitHub Plugin
   - Configure job to trigger on GitHub webhooks
   - Set up GitHub credentials in Jenkins

#### Example Jenkinsfile

```groovy
// Jenkinsfile for NHS Wales projects
pipeline {
    agent any
    
    environment {
        NHS_COMPLIANCE_CHECK = 'true'
        SECURITY_SCAN = 'enabled'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('NHS Compliance Check') {
            steps {
                script {
                    // Custom compliance checks for NHS Wales
                    sh 'python scripts/nhs-compliance-check.py'
                }
            }
        }
        
        stage('Security Scan') {
            steps {
                // Security scanning for sensitive data
                sh 'python scripts/security-scan.py'
            }
        }
        
        stage('Build') {
            steps {
                // Your build steps
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Deploy to Internal') {
            when {
                branch 'main'
            }
            steps {
                // Deploy to internal NHS Wales infrastructure
                sh 'scripts/deploy-internal.sh'
            }
        }
    }
    
    post {
        always {
            // Clean up sensitive files
            sh 'scripts/cleanup-sensitive-data.sh'
        }
        failure {
            // Notify NHS Wales team
            emailext(
                subject: "NHS Wales Build Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                body: "Build failed. Please check Jenkins for details.",
                to: "your-team@wales.nhs.uk"
            )
        }
    }
}
```

### GitHub Actions for NHS Wales

#### Example Workflow with Compliance Checks

```yaml
# .github/workflows/nhs-wales-ci.yml
name: NHS Wales CI/CD Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

env:
  NHS_ENVIRONMENT: production
  SECURITY_LEVEL: high

jobs:
  compliance-check:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: NHS Compliance Check
      run: |
        echo "Running NHS Wales compliance checks..."
        # Check for patient data patterns
        if grep -r "NHS\s\+number\|Patient\s\+ID" --include="*.py" --include="*.js" --include="*.json" .; then
          echo "❌ Potential patient data found!"
          exit 1
        fi
        echo "✅ No sensitive NHS data detected"
    
    - name: Security Scan
      uses: securecodewarrior/github-action-add-sarif@v1
      with:
        sarif-file: 'security-scan-results.sarif'

  build-and-test:
    needs: compliance-check
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run tests
      run: npm test
    
    - name: Build application
      run: npm run build
    
    - name: Archive production artifacts
      uses: actions/upload-artifact@v3
      with:
        name: build-files
        path: dist/

  deploy-internal:
    if: github.ref == 'refs/heads/main'
    needs: [compliance-check, build-and-test]
    runs-on: ubuntu-latest
    environment: nhs-wales-internal
    steps:
    - name: Deploy to NHS Wales Infrastructure
      run: |
        echo "Deploying to NHS Wales internal infrastructure..."
        # Your deployment commands here
```

### Integration with Internal Systems

#### SharePoint Document Management

```bash
# Script to sync documentation to SharePoint
#!/bin/bash
# sync-to-sharepoint.sh

# Configuration
SHAREPOINT_SITE="https://yourorg.sharepoint.com/sites/your-site"
LOCAL_DOCS="./docs"
SHAREPOINT_DOCS="Shared Documents/Technical Documentation"

# Sync documentation
echo "Syncing documentation to SharePoint..."
rsync -av "$LOCAL_DOCS/" "/path/to/synced/sharepoint/$SHAREPOINT_DOCS/"

echo "Documentation synced successfully"
```

#### Network Drive Integration

```bash
# Script to backup code to network drives
#!/bin/bash
# backup-to-network.sh

NETWORK_DRIVE="/mnt/nhs-shared-drive"
PROJECT_NAME="your-project"
BACKUP_DIR="$NETWORK_DRIVE/code-backups/$PROJECT_NAME"

# Create backup directory
mkdir -p "$BACKUP_DIR/$(date +%Y-%m-%d)"

# Create compressed backup
tar -czf "$BACKUP_DIR/$(date +%Y-%m-%d)/backup-$(date +%H%M%S).tar.gz" \
    --exclude='.git' \
    --exclude='node_modules' \
    --exclude='dist' \
    .

echo "Backup created in $BACKUP_DIR"
```

### Monitoring and Compliance

#### Automated Compliance Reporting

```python
# scripts/nhs-compliance-check.py
import os
import re
import json
from datetime import datetime

def check_sensitive_data():
    """Check for NHS sensitive data patterns"""
    patterns = [
        r'\b\d{10}\b',  # NHS numbers
        r'patient[_\s]+id',  # Patient IDs
        r'medical[_\s]+record',  # Medical records
        # Add more patterns as needed
    ]
    
    violations = []
    
    for root, dirs, files in os.walk('.'):
        # Skip .git and node_modules
        dirs[:] = [d for d in dirs if d not in ['.git', 'node_modules', 'dist']]
        
        for file in files:
            if file.endswith(('.py', '.js', '.json', '.md', '.txt')):
                filepath = os.path.join(root, file)
                try:
                    with open(filepath, 'r', encoding='utf-8') as f:
                        content = f.read()
                        
                    for pattern in patterns:
                        if re.search(pattern, content, re.IGNORECASE):
                            violations.append({
                                'file': filepath,
                                'pattern': pattern,
                                'line': content.count('\n', 0, content.find(re.search(pattern, content, re.IGNORECASE).group())) + 1
                            })
                except:
                    continue
    
    return violations

if __name__ == "__main__":
    violations = check_sensitive_data()
    
    if violations:
        print("❌ NHS Compliance violations found:")
        for violation in violations:
            print(f"  File: {violation['file']}, Line: {violation['line']}")
        exit(1)
    else:
        print("✅ NHS Compliance check passed")
        
    # Generate compliance report
    report = {
        'timestamp': datetime.now().isoformat(),
        'status': 'PASS' if not violations else 'FAIL',
        'violations': violations
    }
    
    with open('compliance-report.json', 'w') as f:
        json.dump(report, f, indent=2)
```

---

## Troubleshooting

### Common Issues and Solutions

#### 1. Authentication Problems

**Issue**: `remote: Repository not found` or `Permission denied`

**Solutions**:
```bash
# Check if remote URL is correct
git remote -v

# Update remote URL if incorrect
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git

# For SSH issues, test connection
ssh -T git@github.com

# Regenerate SSH key if needed
ssh-keygen -t ed25519 -C "your.email@wales.nhs.uk"
```

#### 2. Large File Issues

**Issue**: `file too large` error when pushing

**Solutions**:
```bash
# Remove large files from history
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch path/to/large/file' \
--prune-empty --tag-name-filter cat -- --all

# Or use BFG Repo-Cleaner (faster)
java -jar bfg.jar --strip-blobs-bigger-than 100M

# Push cleaned repository
git push --force-with-lease origin main
```

#### 3. Network/Firewall Issues

**Issue**: Cannot connect to GitHub

**Solutions**:
1. Contact NHS Wales IT support to allow GitHub domains
2. Use HTTPS instead of SSH if port 22 is blocked
3. Configure proxy if required:

```bash
# Configure Git to use proxy
git config --global http.proxy http://proxy.server:port
git config --global https.proxy https://proxy.server:port

# For authenticated proxy
git config --global http.proxy http://username:password@proxy.server:port
```

#### 4. SharePoint Sync Issues

**Issue**: Git repository in SharePoint sync folder not working properly

**Solutions**:
1. Ensure SharePoint sync is not interfering with `.git` folder
2. Add `.git` to SharePoint sync exclusions if possible
3. Consider using separate local repository and manual SharePoint updates

#### 5. Merge Conflicts

**Issue**: Conflicts when merging or pulling

**Solutions**:
```bash
# Check status
git status

# Open conflicted files and resolve manually
# Look for conflict markers: <<<<<<<, =======, >>>>>>>

# After resolving conflicts
git add .
git commit -m "Resolve merge conflicts"

# Or abort merge if needed
git merge --abort
```

#### 6. Branch Management Issues

**Issue**: Branches out of sync or complex history

**Solutions**:
```bash
# Reset branch to match remote
git fetch origin
git reset --hard origin/main

# Clean up local branches
git branch -d branch-name

# Prune remote-tracking branches
git remote prune origin
```

---

## Best Practices

### Security Best Practices

1. **Never commit sensitive information**:
   ```bash
   # Create .gitignore file
   echo "*.env" >> .gitignore
   echo "config/secrets.json" >> .gitignore
   echo "*.key" >> .gitignore
   echo "*.pem" >> .gitignore
   ```

2. **Use private repositories** for NHS Wales projects

3. **Enable two-factor authentication** on GitHub account

4. **Regular security audits**:
   ```bash
   # Check for secrets in repository
   git log --all --full-history -- "*.env"
   git log --all --full-history -- "*secret*"
   ```

5. **Use branch protection rules** on GitHub

### Workflow Best Practices

1. **Use descriptive commit messages**:
   ```bash
   # Good commit message format
   git commit -m "Add patient data validation to admission form
   
   - Implement NHS number validation
   - Add postcode format checking
   - Update unit tests for new validation rules
   
   Fixes #123"
   ```

2. **Regular commits and pushes**:
   ```bash
   # Commit frequently with small, logical changes
   git add specific-file.py
   git commit -m "Fix validation bug in patient form"
   ```

3. **Use feature branches**:
   ```bash
   # Create feature branch
   git checkout -b feature/patient-validation
   
   # Work on feature, commit changes
   git add .
   git commit -m "Add patient validation logic"
   
   # Push feature branch
   git push origin feature/patient-validation
   
   # Create pull request on GitHub for review
   ```

4. **Keep repositories clean**:
   ```bash
   # Regular cleanup
   git gc --prune=now
   git remote prune origin
   ```

### NHS Wales Specific Best Practices

1. **Information Governance Compliance**:
   - Get approval before creating public repositories
   - Regular review of repository contents
   - Document data classification levels

2. **Documentation Standards**:
   - Include README.md with project description
   - Document NHS Wales specific configurations
   - Maintain CHANGELOG.md for version tracking

3. **Code Review Process**:
   - Require pull request reviews
   - Include security team in sensitive changes
   - Use GitHub's code scanning features

4. **Backup and Recovery**:
   - Regular backups to NHS Wales infrastructure
   - Document recovery procedures
   - Test backup restoration process

### File Organization

```
your-nhs-project/
├── .gitignore                 # Exclude sensitive files
├── README.md                  # Project documentation
├── CHANGELOG.md               # Version history
├── .github/
│   ├── workflows/             # GitHub Actions
│   └── ISSUE_TEMPLATE.md      # Issue templates
├── docs/                      # Documentation
│   ├── nhs-compliance.md      # NHS specific docs
│   └── deployment.md          # Deployment guide
├── src/                       # Source code
├── tests/                     # Test files
├── scripts/                   # Utility scripts
│   ├── compliance-check.py    # NHS compliance checker
│   └── backup.sh             # Backup script
└── config/                    # Configuration (non-sensitive)
    └── .env.example          # Environment template
```

---

## Support and Resources

### NHS Wales Contacts

- **IT Support**: Contact your local NHS Wales IT support team
- **Information Governance**: Reach out to your IG team for data classification questions
- **Security Team**: For security-related questions about GitHub usage

### GitHub Resources

- **GitHub Docs**: [docs.github.com](https://docs.github.com)
- **GitHub Desktop Help**: [docs.github.com/en/desktop](https://docs.github.com/en/desktop)
- **Git Documentation**: [git-scm.com/doc](https://git-scm.com/doc)
- **GitHub Skills**: [skills.github.com](https://skills.github.com) - Interactive tutorials

### Training Resources

1. **Git Basics Course**:
   - [Git Handbook](https://guides.github.com/introduction/git-handbook/)
   - [Pro Git Book](https://git-scm.com/book) (Free online)

2. **GitHub-specific Training**:
   - [GitHub Learning Lab](https://lab.github.com/)
   - [GitHub Desktop Tutorial](https://docs.github.com/en/desktop/installing-and-configuring-github-desktop/overview/getting-started-with-github-desktop)

3. **NHS Wales Specific**:
   - Internal training sessions (contact your training coordinator)
   - Lunch and learn sessions on version control

### Emergency Procedures

If you accidentally commit sensitive NHS data:

1. **Immediate Actions**:
   ```bash
   # Remove file from latest commit
   git rm --cached sensitive-file.txt
   git commit --amend -m "Remove sensitive file"
   git push --force-with-lease origin main
   ```

2. **For Historical Commits**:
   - Contact your IT security team immediately
   - Consider repository deletion and recreation if data is highly sensitive
   - Use BFG Repo-Cleaner or git filter-branch to remove from history

3. **Reporting**:
   - Report incident to Information Governance team
   - Document actions taken
   - Follow NHS Wales incident reporting procedures

### Getting Help

1. **Internal Help**:
   - Your team's senior developer
   - NHS Wales technical forums
   - Local IT support

2. **External Resources**:
   - Stack Overflow (for technical Git questions)
   - GitHub Community Forum
   - Git official support channels

---

## Quick Reference Card

### Essential Commands

```bash
# Setup
git config --global user.name "Your Name"
git config --global user.email "your.email@wales.nhs.uk"

# Daily workflow
git status                    # Check status
git add .                     # Stage changes
git commit -m "message"       # Commit changes
git push origin main          # Push to GitHub
git pull origin main          # Pull from GitHub

# Branch management
git checkout -b new-branch    # Create and switch to branch
git checkout main             # Switch to main branch
git merge feature-branch      # Merge branch into current

# Emergency
git stash                     # Temporarily save changes
git reset --hard HEAD~1       # Undo last commit (destructive)
git revert HEAD               # Undo last commit (safe)
```

### GitHub Desktop Quick Actions

- **Ctrl+Shift+A**: Add repository
- **Ctrl+T**: Create new branch
- **Ctrl+Enter**: Commit changes
- **Ctrl+P**: Push to GitHub
- **Ctrl+Shift+P**: Pull from GitHub

---

*This guide is maintained by the NHS Wales Technical Team. For updates or corrections, please submit an issue or pull request to this repository.*

**Version**: 1.0  
**Last Updated**: October 2024  
**Next Review**: January 2025

---
