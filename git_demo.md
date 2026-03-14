
# HOW TO PUSH A SINGLE FILE TO A REMTE REPO

---

## LOCAL REPO STEPS

### 1. Check your status and current branch

```bash
git status
git branch
```

### 2. Is your local main up to date? Pull the updated repo
```bash
git pull origin main
```

### 3. Create a new branch using your name and feature name
```bash
# Not recommended
git checkout -b data-cleaning

# Recommended
git checkout -b <your-name>/data-cleaning
```

### 4. Stage ONLY your specific file
```bash
# Not recommended - stages everything
git add .

# Recommended - stage only your file
git add notebooks/your-file.ipynb
```

### 5. Commit your changes
```bash
# Use one of these prefixes:
git commit -m "[Add] data cleaning and quality assessment"
git commit -m "[Fix] corrected missing values in preprocessing"
git commit -m "[Update] updated EDA notebook"
```

### 6. Push your branch to the remote repo
```bash
git push -u origin <your-name>/<feature-name>
```

### 7. Click on the link printed in the terminal to open GitHub and finish the pull request

---

## REMOTE REPO STEPS

1. Go to the GitHub repo in your browser
2. Click **"Compare & pull request"**
3. Add a short description of your changes
4. Request a review from a teammate
5. **Do NOT merge your own PR**

---

## IMPORTANT REMINDERS

- Always create a new branch, **never push directly to main**
- Only stage the file you worked on `git add <specific-file>`
- Pull from main before starting new work
- Use clear branch names: `your-name/what-you-did`