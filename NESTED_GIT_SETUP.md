# Nested Git Repositories Setup

## Current Structure

Your monorepo has nested git repositories:
```
quizapp/                    # Parent git repository
├── .git/                   # Parent repo (tracked)
├── quizzam/
│   └── .git/               # Nested repo (ignored by parent)
└── quizzy-front/
    └── .git/               # Nested repo (ignored by parent)
```

## Configuration

The root `.gitignore` has been configured to ignore nested `.git` directories:

```gitignore
# Ignore nested .git directories (submodules or nested repos)
quizzam/.git/
quizzy-front/.git/
*/.git/
```

This ensures:
- ✅ The parent repository's `.git/` is tracked normally
- ✅ Sub-repositories' `.git/` directories are ignored
- ✅ Any future nested repos will also be ignored

## Options for Managing Nested Repos

### Option 1: Keep as Separate Repos (Current Setup)
- Each subdirectory maintains its own git history
- Parent repo ignores the nested `.git` folders
- **Pros**: Independent version control for each project
- **Cons**: Cannot track sub-repo changes in parent repo

### Option 2: Convert to Git Submodules
If you want to track the sub-repos in the parent:

```bash
# Remove nested .git directories
rm -rf quizzam/.git quizzy-front/.git

# Add as submodules (if they're in separate remote repos)
git submodule add <quizzam-repo-url> quizzam
git submodule add <quizzy-front-repo-url> quizzy-front
```

### Option 3: Single Monorepo (Merge Histories)
If you want a single unified git history:

```bash
# Remove nested .git directories
rm -rf quizzam/.git quizzy-front/.git

# Add all files to parent repo
git add quizzam/ quizzy-front/
git commit -m "Merge sub-repos into monorepo"
```

## Verification

To verify nested `.git` directories are ignored:

```bash
# Check git status (should not show .git directories)
git status

# Verify ignore patterns
git check-ignore -v quizzam/.git
git check-ignore -v quizzy-front/.git

# List tracked files (should not include nested .git)
git ls-files | grep "\.git"
```

## Important Notes

- **Never commit nested `.git` directories** - they contain the entire history of sub-repos
- **Backup before removing** nested `.git` if you plan to merge histories
- **Consider using submodules** if you need to track sub-repo versions in the parent

