# Heroku Deployment Notes - Venkat Sai Sanitation Services

**Date:** February 17, 2026  
**App Name:** venkatsaisanitation  
**Live URL:** https://venkatsaisanitation-c38b35f4e542.herokuapp.com  
**GitHub Repository:** https://github.com/Meherangel23/VenkatSaiSanitation

---

## 📋 Table of Contents
1. [Pre-Deployment Setup](#pre-deployment-setup)
2. [Git Commands](#git-commands)
3. [Heroku Commands](#heroku-commands)
4. [Deployment Process](#deployment-process)
5. [Post-Deployment Commands](#post-deployment-commands)
6. [Troubleshooting](#troubleshooting)
7. [Future Updates](#future-updates)

---

## 🔧 Pre-Deployment Setup

### Required Files for Heroku Deployment

#### 1. **package.json**
```json
{
  "name": "venkat-sai-sanitation",
  "version": "1.0.0",
  "description": "Venkat Sai Sanitation Services - Professional Septic Tank & Drainage Cleaning",
  "main": "index.html",
  "scripts": {
    "start": "node server.js",
    "dev": "live-server --port=3000"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "engines": {
    "node": "18.x"
  }
}
```

**Key Points:**
- `"start": "node server.js"` - Heroku uses this to start the app
- `"engines"` - Specifies Node.js version for Heroku

#### 2. **Procfile**
```
web: node server.js
```

**Purpose:** Tells Heroku how to run the web process

#### 3. **server.js**
```javascript
const express = require('express');
const path = require('path');

const app = express();
const PORT = process.env.PORT || 3000;

// Serve static files
app.use(express.static(__dirname));

// Serve index.html for all routes (SPA support)
app.get('*', (req, res) => {
    res.sendFile(path.join(__dirname, 'index.html'));
});

app.listen(PORT, () => {
    console.log(`🚛 Venkat Sai Sanitation Services running on port ${PORT}`);
    console.log(`📍 Visit: http://localhost:${PORT}`);
});
```

**Key Points:**
- Uses `process.env.PORT` - Heroku assigns port dynamically
- Serves static files from root directory
- Handles all routes for SPA support

---

## 📝 Git Commands

### 1. Check Git Status
```bash
git status
```
**Purpose:** Check current branch and uncommitted changes

### 2. Stage All Changes
```bash
git add .
```
**Purpose:** Add all modified files to staging area

### 3. Commit Changes
```bash
git commit -m "Prepare for Heroku deployment"
```
**Purpose:** Commit staged changes with a message

### 4. Check Remote Repositories
```bash
git remote -v
```
**Output:**
```
heroku  https://git.heroku.com/venkatsaisanitation.git (fetch)
heroku  https://git.heroku.com/venkatsaisanitation.git (push)
origin  https://github.com/Meherangel23/VenkatSaiSanitation.git (fetch)
origin  https://github.com/Meherangel23/VenkatSaiSanitation.git (push)
```

### 5. Remove Incorrect Heroku Remote (if needed)
```bash
git remote remove heroku
```
**Purpose:** Remove wrong Heroku remote before adding correct one

---

## 🚀 Heroku Commands

### 1. Check Heroku CLI Version
```bash
heroku --version
```
**Output:** `heroku/10.17.0 win32-x64 node-v20.20.0`

### 2. Check Logged-in User
```bash
heroku auth:whoami
```
**Output:** `meherangels23@gmail.com`

### 3. Login to Heroku (if not logged in)
```bash
heroku login
```
**Purpose:** Opens browser to authenticate with Heroku

### 4. Create New Heroku App (if app doesn't exist)
```bash
heroku create venkatsaisanitation
```
**Note:** In our case, the app already existed, so we skipped this step

### 5. Check Existing App Info
```bash
heroku apps:info -a venkatsaisanitation
```
**Output:**
```
=== venkatsaisanitation
Auto Cert Mgmt: false
Dynos:          web: 1
Git URL:        https://git.heroku.com/venkatsaisanitation.git
Region:         us
```

### 6. Add Heroku Git Remote
```bash
heroku git:remote -a venkatsaisanitation
```
**Output:** `set git remote heroku to https://git.heroku.com/venkatsaisanitation.git`

### 7. Rename Heroku App (if needed)
```bash
heroku apps:rename new-app-name --app old-app-name
```
**Note:** We attempted to rename but the desired name was already taken

### 8. Delete Unwanted Heroku App
```bash
heroku apps:destroy venkat-sai-sanitation --confirm venkat-sai-sanitation
```
**Purpose:** Remove the incorrectly created app with hyphens

---

## 🎯 Deployment Process

### Step-by-Step Deployment Commands

#### Step 1: Ensure Code is Committed
```bash
# Check status
git status

# Add all changes
git add .

# Commit changes
git commit -m "Prepare for Heroku deployment"
```

#### Step 2: Verify Heroku Remote
```bash
# Check remotes
git remote -v

# If heroku remote is missing or incorrect, add it
heroku git:remote -a venkatsaisanitation
```

#### Step 3: Deploy to Heroku
```bash
git push heroku main
```

**Deployment Output:**
```
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 8 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (13/13), done.
Total 13 (delta 0), reused 0 (delta 0), pack-reused 0
remote: Building source:
remote: Waiting on build...
remote: 
remote: -----> Building on the Heroku-22 stack
remote: -----> Using buildpack: heroku/nodejs
remote: -----> Node.js app detected
remote: -----> Creating runtime environment
remote: -----> Installing binaries
remote:        engines.node (package.json):  18.x
remote:        engines.npm (package.json):   unspecified (use default)
remote: -----> Installing dependencies
remote:        Installing node modules
remote: -----> Build succeeded!
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote: -----> Compressing...
remote: -----> Launching...
remote:        Released v3
remote:        https://venkatsaisanitation.herokuapp.com/ deployed to Heroku
remote: 
To https://git.heroku.com/venkatsaisanitation.git
 * [new branch]      main -> main
```

---

## 📊 Post-Deployment Commands

### 1. Open App in Browser
```bash
heroku open -a venkatsaisanitation
```
**Purpose:** Opens the deployed app in default browser

### 2. View Application Logs
```bash
# View recent logs
heroku logs -a venkatsaisanitation

# View last 50 lines
heroku logs -n 50 -a venkatsaisanitation

# Tail logs in real-time
heroku logs --tail -a venkatsaisanitation
```

### 3. Check Dyno Status
```bash
heroku ps -a venkatsaisanitation
```
**Output:**
```
=== web (Free): node server.js (1)
web.1: up 2026/02/17 09:00:00 +0530 (~ 30m ago)
```

### 4. Restart Application
```bash
heroku restart -a venkatsaisanitation
```

### 5. Scale Dynos (if needed)
```bash
# Scale to 1 web dyno
heroku ps:scale web=1 -a venkatsaisanitation

# Scale to 0 to stop (saves dyno hours)
heroku ps:scale web=0 -a venkatsaisanitation
```

### 6. Check Environment Variables
```bash
heroku config -a venkatsaisanitation
```

### 7. Set Environment Variables (if needed)
```bash
heroku config:set VARIABLE_NAME=value -a venkatsaisanitation
```

---

## 🔍 Troubleshooting

### Issue 1: Wrong Heroku Remote
**Problem:** Git was pushing to wrong Heroku app (naturalresourcemanagement)

**Solution:**
```bash
# Remove incorrect remote
git remote remove heroku

# Add correct remote
heroku git:remote -a venkatsaisanitation

# Verify
git remote -v
```

### Issue 2: App Name Already Taken
**Problem:** Tried to create app with name that already exists

**Solution:**
```bash
# Check if app exists
heroku apps:info -a venkatsaisanitation

# If it exists and belongs to you, just add the remote
heroku git:remote -a venkatsaisanitation
```

### Issue 3: Application Error (H10)
**Problem:** App crashes after deployment

**Solution:**
```bash
# Check logs
heroku logs --tail -a venkatsaisanitation

# Ensure Procfile is correct
# Ensure package.json has correct start script
# Ensure server.js uses process.env.PORT
```

### Issue 4: Build Failed
**Problem:** Heroku build fails during deployment

**Solution:**
```bash
# Check Node.js version in package.json
# Ensure all dependencies are in package.json
# Run locally first: npm install && npm start
```

---

## 🔄 Future Updates

### Standard Update Workflow

#### 1. Make Changes Locally
```bash
# Edit your files
# Test locally: npm start
```

#### 2. Commit Changes
```bash
git add .
git commit -m "Description of changes"
```

#### 3. Push to GitHub (optional but recommended)
```bash
git push origin main
```

#### 4. Deploy to Heroku
```bash
git push heroku main
```

#### 5. Verify Deployment
```bash
# Check logs
heroku logs --tail -a venkatsaisanitation

# Open app
heroku open -a venkatsaisanitation
```

### Quick Deploy Script
Create a file `deploy.sh`:
```bash
#!/bin/bash
echo "🚀 Starting deployment..."

# Add all changes
git add .

# Commit with timestamp
git commit -m "Update: $(date '+%Y-%m-%d %H:%M:%S')"

# Push to GitHub
git push origin main

# Deploy to Heroku
git push heroku main

echo "✅ Deployment complete!"
```

Make it executable:
```bash
chmod +x deploy.sh
```

Run it:
```bash
./deploy.sh
```

---

## 📌 Important Notes

### 1. **Heroku Free Tier Limitations**
- App sleeps after 30 minutes of inactivity
- First request after sleep takes ~10-15 seconds
- 550 free dyno hours per month

### 2. **Environment Variables**
- Never commit sensitive data (API keys, passwords)
- Use Heroku config vars: `heroku config:set KEY=value`

### 3. **Static Assets**
- All static files are served from root directory
- Images, CSS, JS are accessible via relative paths

### 4. **Port Configuration**
- Always use `process.env.PORT` in server.js
- Heroku assigns port dynamically
- Never hardcode port number

### 5. **Node Version**
- Specified in package.json: `"engines": { "node": "18.x" }`
- Heroku uses this to install correct Node.js version

---

## 🎓 Additional Resources

### Heroku Documentation
- [Getting Started with Node.js](https://devcenter.heroku.com/articles/getting-started-with-nodejs)
- [Deploying Node.js Apps](https://devcenter.heroku.com/articles/deploying-nodejs)
- [Heroku CLI Commands](https://devcenter.heroku.com/articles/heroku-cli-commands)

### Git Documentation
- [Git Basics](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics)
- [Git Remote](https://git-scm.com/docs/git-remote)

---

## ✅ Deployment Checklist

- [x] Create/verify `package.json` with start script
- [x] Create/verify `Procfile`
- [x] Create/verify `server.js` with PORT configuration
- [x] Install Heroku CLI
- [x] Login to Heroku
- [x] Initialize Git repository
- [x] Commit all changes
- [x] Create/connect to Heroku app
- [x] Add Heroku remote
- [x] Deploy to Heroku
- [x] Verify deployment
- [x] Test live URL

---

## 📞 Support

**Heroku Account:** meherangels23@gmail.com  
**App Name:** venkatsaisanitation  
**Live URL:** https://venkatsaisanitation.herokuapp.com  
**GitHub Repo:** https://github.com/Meherangel23/VenkatSaiSanitation

---

**Last Updated:** February 17, 2026  
**Deployed By:** Meher Trendz  
**Status:** ✅ Successfully Deployed
