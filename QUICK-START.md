# Quick Start Guide - NHS Wales Git to GitHub

## Before You Start
✅ Get approval from Information Governance team  
✅ Ensure no patient data in your repository  
✅ Have GitHub account ready  
✅ Install Git and/or GitHub Desktop  

## Method 1: Command Line (5 minutes)

### If you have existing git repository:
```bash
# 1. Navigate to your repo
cd /path/to/your/repo

# 2. Add GitHub remote
git remote add origin https://github.com/USERNAME/REPO.git

# 3. Push to GitHub
git push -u origin main
```

### If starting fresh:
```bash
# 1. Initialize git
git init
git add .
git commit -m "Initial commit"

# 2. Add GitHub remote and push
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

## Method 2: GitHub Desktop (3 clicks)

1. **File** → **Add Local Repository** → Select your folder
2. **Publish repository** → Choose private → **Publish**
3. Done! 🎉

## Daily Workflow

### Command Line:
```bash
git add .
git commit -m "Your changes"
git push
```

### GitHub Desktop:
1. Review changes
2. Write commit message
3. Click **Commit to main**
4. Click **Push origin**

## Need Help?
- Full guide: [README.md](README.md)
- IT Support: Contact your local NHS Wales IT team
- Emergency: Follow incident reporting procedures

## Security Reminders
❌ Never commit patient data  
❌ Never commit passwords or keys  
✅ Always use private repositories  
✅ Regular security reviews  