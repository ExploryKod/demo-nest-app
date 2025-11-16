# Security Guidelines

## Protecting Sensitive Information

This repository contains sensitive information that should **NEVER** be committed to version control.

### What to Protect

1. **Environment Variables** (`.env` files)
   - Database connection strings
   - API keys
   - JWT secrets
   - Firebase credentials

2. **Firebase Service Account Keys**
   - `quizzam-firebase-key.json`
   - Any file containing Firebase credentials

3. **Private Keys and Certificates**
   - `.pem`, `.key`, `.p12`, `.pfx` files

### Files Already Protected

The following files are automatically ignored by `.gitignore`:
- `.env` and `.env.*` files
- `**/firebase*key*.json` files
- `**/*secret*` and `**/*credential*` files

### If You Accidentally Committed Sensitive Data

If you've already committed sensitive information:

1. **Remove the file from git history:**
   ```bash
   git rm --cached quizzam/.env
   git commit -m "Remove sensitive .env file"
   ```

2. **If already pushed, you need to rewrite history:**
   ```bash
   # Use git filter-branch or BFG Repo-Cleaner
   # WARNING: This rewrites git history!
   git filter-branch --force --index-filter \
     "git rm --cached --ignore-unmatch quizzam/.env" \
     --prune-empty --tag-name-filter cat -- --all
   ```

3. **Rotate all exposed secrets immediately:**
   - Change database passwords
   - Regenerate API keys
   - Create new Firebase service account keys

### Best Practices

1. **Always use `.env.example`** as a template
2. **Never commit** actual `.env` files
3. **Use environment variables** in CI/CD pipelines
4. **Rotate secrets** if accidentally exposed
5. **Use secret management tools** for production (AWS Secrets Manager, Azure Key Vault, etc.)

### Setting Up Local Environment

1. Copy the example file:
   ```bash
   cp quizzam/.env.example quizzam/.env
   ```

2. Fill in your actual values in `.env`

3. Verify `.env` is in `.gitignore`:
   ```bash
   git check-ignore quizzam/.env
   ```

