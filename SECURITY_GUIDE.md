# Security Guide

## ⚠️ CRITICAL: What Was Deleted

**File Deleted:** `the-axiom-473314-s3-322a73e63c69.json`

This was a Google service account key file that should **NEVER** be committed to your repository. This file contained sensitive credentials that could give unauthorized access to your Google Cloud services.

## 🔴 IMMEDIATE ACTIONS REQUIRED

1. **Revoke the exposed key:**
   - Go to Google Cloud Console: https://console.cloud.google.com
   - Navigate to IAM & Admin > Service Accounts
   - Find the service account with ID matching the deleted file
   - Delete or rotate the key immediately

2. **Check for unauthorized access:**
   - Review your Google Cloud audit logs
   - Check for any suspicious activity

## 🛡️ Protection Measures Implemented

1. **Created `.gitignore`** - Blocks the following from ever being committed:
   - All `.json` files except essential config files (package.json, app.json, etc.)
   - Service account keys (pattern: `*-service-account*.json`)
   - Signing keys (`.keystore`, `.jks` files)
   - Binary files (`.aab`, `.apk`)

2. **Binary files in repository:**
   - `application-2ef147e1-4672-4313-b978-b88ff20c7d50.aab` is also tracked
   - This .aab file should be distributed through proper channels, not stored in code

## 📋 Best Practices Going Forward

### Where to Store Credentials

**NEVER store these in your repository:**
- Service account keys
- API keys
- Upload keys/keystores
- Built binaries (.aab, .apk)

**Instead:**
1. **For EAS Build:** Use Expo's secure credential storage
2. **For local builds:** Store in a secure location outside your project
3. **For CI/CD:** Use environment variables or secret managers

### Proper Key Management

```bash
# Store keys OUTSIDE your project directory
~/secure-keys/
  ├── your-project-upload-key.keystore
  └── service-account.json

# Reference them when needed
eas build --local --non-interactive
```

## 📍 Where These Files Are Located

- **Deleted file was:** `/home/user/rork-app/the-axiom-473314-s3-322a73e63c69.json`
- **Protection files:**
  - `.gitignore` - Root of project
  - This guide - Root of project

## ✅ Verification

To verify protection is working:
```bash
# This should show .gitignore is protecting sensitive files
git status
```

## 🔒 Summary

- ✅ Deleted: Exposed service account key
- ✅ Created: .gitignore to prevent future exposure
- ⚠️ TODO: Revoke the exposed key in Google Cloud Console
- ⚠️ TODO: Remove .aab file if not needed in repository
