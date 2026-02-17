# Quick Reference Guide - Heroku Deployment

## 🚀 App Information
- **App Name:** venkatsaisanitation
- **Live URL:** https://venkatsaisanitation-c38b35f4e542.herokuapp.com
- **GitHub:** https://github.com/Meherangel23/VenkatSaiSanitation

---

## ⚡ Most Used Commands

### Deploy Updates
```bash
git add .
git commit -m "Your message here"
git push heroku main
```

### View Logs
```bash
heroku logs --tail -a venkatsaisanitation
```

### Open App
```bash
heroku open -a venkatsaisanitation
```

### Check Status
```bash
heroku ps -a venkatsaisanitation
```

### Restart App
```bash
heroku restart -a venkatsaisanitation
```

---

## 🔧 Git Commands Cheat Sheet

| Command | Purpose |
|---------|---------|
| `git status` | Check current status |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Commit changes |
| `git push origin main` | Push to GitHub |
| `git push heroku main` | Deploy to Heroku |
| `git remote -v` | View remotes |
| `git log --oneline` | View commit history |

---

## 🌐 Heroku Commands Cheat Sheet

| Command | Purpose |
|---------|---------|
| `heroku login` | Login to Heroku |
| `heroku auth:whoami` | Check logged-in user |
| `heroku apps` | List all apps |
| `heroku apps:info -a APP_NAME` | App details |
| `heroku logs -a APP_NAME` | View logs |
| `heroku logs --tail -a APP_NAME` | Live logs |
| `heroku ps -a APP_NAME` | Check dynos |
| `heroku restart -a APP_NAME` | Restart app |
| `heroku open -a APP_NAME` | Open in browser |
| `heroku config -a APP_NAME` | View env vars |
| `heroku config:set KEY=VALUE -a APP_NAME` | Set env var |

---

## 📝 One-Line Deploy
```bash
git add . && git commit -m "Update" && git push heroku main
```

---

## 🆘 Emergency Commands

### App Not Responding
```bash
heroku restart -a venkatsaisanitation
heroku logs --tail -a venkatsaisanitation
```

### Check What's Wrong
```bash
heroku ps -a venkatsaisanitation
heroku logs -n 100 -a venkatsaisanitation
```

### Reset Heroku Remote
```bash
git remote remove heroku
heroku git:remote -a venkatsaisanitation
```

---

## 📂 Required Files

### package.json (must have)
- `"start": "node server.js"`
- `"engines": { "node": "18.x" }`

### Procfile (must have)
```
web: node server.js
```

### server.js (must use)
```javascript
const PORT = process.env.PORT || 3000;
```

---

## ✅ Pre-Deploy Checklist
- [ ] Test locally: `npm start`
- [ ] All changes committed
- [ ] Procfile exists
- [ ] package.json has start script
- [ ] server.js uses process.env.PORT

---

**For detailed documentation, see DEPLOYMENT_NOTES.md**
