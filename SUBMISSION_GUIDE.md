# Google Tag Manager Community Template Gallery Submission Guide

This guide walks you through submitting the Shoparize Partner Tracking template to the [GTM Community Template Gallery](https://tagmanager.google.com/gallery).

## ✅ Pre-Submission Checklist

Before submitting, ensure all requirements are met:

- [x] **template.tpl** - Template file with categories added
- [x] **metadata.yaml** - Metadata with homepage, documentation, and version info
- [x] **LICENSE** - Apache 2.0 license (filename must be ALL CAPS)
- [x] **README.md** - Documentation for users
- [x] **logo.png** - Shoparize logo for branding
- [ ] **GitHub repository** - Public repository with all files
- [ ] **Terms of Service** - Agreed to in template (Info tab checkbox)

## 📦 Repository Structure

Your repository must have this exact structure:

```
shoparize-gtm-template/
├── template.tpl          # Renamed from shoparize-gtm-template.tpl
├── metadata.yaml         # Version and documentation info
├── LICENSE               # Apache 2.0 (ALL CAPS filename)
├── README.md             # User documentation
└── logo.png              # Template logo/icon
```

**Important:** The template file MUST be named exactly `template.tpl` (not `shoparize-gtm-template.tpl`).

## 🔧 Step-by-Step Submission

### Step 1: Rename Template File

The template file must be named `template.tpl`:

```bash
cd /Users/du/PhpstormProjects/shoparize/shoparize-gtm-template
mv shoparize-gtm-template.tpl template.tpl
```

### Step 2: Create GitHub Repository

1. Go to [GitHub](https://github.com) and sign in
2. Click **"New repository"** (green button)
3. Configure:
   - **Repository name**: `shoparize-gtm-template`
   - **Description**: "Official Shoparize Partner Tracking template for Google Tag Manager"
   - **Visibility**: ✅ Public (required for Gallery submission)
   - **Initialize**: ❌ Don't add README, .gitignore, or license (we have these)
4. Click **"Create repository"**

### Step 3: Push Files to GitHub

```bash
cd /Users/du/PhpstormProjects/shoparize/shoparize-gtm-template

# Initialize git (if not already)
git init

# Add all files
git add template.tpl metadata.yaml LICENSE README.md logo.png SUBMISSION_GUIDE.md

# Commit
git commit -m "Initial release of Shoparize Partner Tracking GTM template"

# Add remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/shoparize-gtm-template.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Step 4: Update metadata.yaml with SHA

After pushing to GitHub:

1. Go to your GitHub repository
2. Click on **"Commits"**
3. Find your initial commit
4. Click the **clipboard icon** 📋 next to the commit SHA
5. Edit `metadata.yaml` locally:

```yaml
homepage: "https://partner.shoparize.com"
documentation: "https://github.com/YOUR_USERNAME/shoparize-gtm-template/blob/main/README.md"
versions:
  # Latest version
  - sha: PASTE_YOUR_ACTUAL_SHA_HERE
    changeNotes: Initial release of Shoparize Partner Tracking template for Google Tag Manager.
```

6. Commit and push the change:

```bash
git add metadata.yaml
git commit -m "Update metadata.yaml with commit SHA"
git push
```

### Step 5: Verify Repository Structure

Before submitting, verify everything is correct:

1. Visit your GitHub repository
2. Confirm you see these files at the **root level**:
   - ✅ `template.tpl`
   - ✅ `metadata.yaml`
   - ✅ `LICENSE`
   - ✅ `README.md`
3. Click on `template.tpl` and verify it opens correctly
4. Click on `metadata.yaml` and verify the SHA is correct
5. Verify Issues are **enabled** (Settings → Features → Issues ✅)

### Step 6: Submit to Gallery

1. Make sure you're signed in to GitHub
2. Go to [GTM Community Template Gallery](https://tagmanager.google.com/gallery)
3. Click the **⋮** (three dots) button
4. Select **"Submit Template"**
5. Enter your repository URL:
   ```
   https://github.com/YOUR_USERNAME/shoparize-gtm-template
   ```
6. Click **"Submit"**

### Step 7: Wait for Review

- Google will review your submission
- This typically takes **2-3 days**
- You'll receive an email notification about the status
- If approved, your template will appear in the Gallery

## 📝 After Submission

### Monitor Issues

Users can report issues via your GitHub repository. Monitor the Issues tab regularly:

```
https://github.com/YOUR_USERNAME/shoparize-gtm-template/issues
```

### Publishing Updates

When you need to update your template:

1. Make changes to `template.tpl`
2. Commit and push changes to GitHub
3. Get the new commit SHA
4. Add a new version entry to `metadata.yaml`:

```yaml
versions:
  # Latest version
  - sha: NEW_COMMIT_SHA_HERE
    changeNotes: |2
      Bug fixes and improvements:
      - Fixed issue with cookie domain detection
      - Improved error handling
      - Updated API endpoint validation
  # Previous version
  - sha: OLD_COMMIT_SHA
    changeNotes: Initial release of Shoparize Partner Tracking template for Google Tag Manager.
```

5. Commit and push the `metadata.yaml` update
6. The Gallery will automatically detect the update in 2-3 days
7. Users will be notified of the available update

## 🔍 Troubleshooting

### Template Not Appearing in Gallery

- **Check repository structure**: Files must be at root level on main branch
- **Verify LICENSE file**: Must be Apache 2.0 and filename in ALL CAPS
- **Check metadata.yaml**: Ensure SHA is correct and syntax is valid
- **Wait longer**: Sometimes it takes up to 5 days

### Submission Rejected

Common reasons:
- **Wrong license**: Must be Apache 2.0 only
- **Missing categories**: Must have categories in template.tpl INFO section
- **Terms of Service**: Must check the ToS checkbox in template editor
- **Repository structure**: Files not at root level or wrong filenames
- **Missing documentation**: README.md should be comprehensive

### Users Can't Find Template

- Ensure your template has appropriate **categories**
- Check that **displayName** is clear and searchable
- Verify **description** is descriptive
- Make sure **documentation** link works

### Issues Disabled

Users need to be able to report issues:
1. Go to repository **Settings**
2. Scroll to **Features**
3. Ensure **Issues** is checked ✅

## 📚 Resources

- [Official Gallery Documentation](https://developers.google.com/tag-platform/tag-manager/templates/gallery)
- [GTM Template Style Guide](https://developers.google.com/tag-platform/tag-manager/templates/style-guide)
- [GTM Custom Templates Guide](https://developers.google.com/tag-platform/tag-manager/templates)
- [Sample Template Repository](https://github.com/google/gtm-templates-simo-ahava)

## 🎯 Success Criteria

Your submission is ready when:

- ✅ All files are in the correct location
- ✅ Template file is named `template.tpl`
- ✅ LICENSE is Apache 2.0 only (ALL CAPS filename)
- ✅ metadata.yaml has correct SHA and documentation links
- ✅ README.md is comprehensive and helpful
- ✅ Repository is public
- ✅ Issues are enabled
- ✅ Terms of Service checkbox is checked in template
- ✅ Template is thoroughly tested

## 📞 Support

If you encounter issues during submission:

1. Review the [official documentation](https://developers.google.com/tag-platform/tag-manager/templates/gallery)
2. Check [GTM Community](https://www.en.advertisercommunity.com/t5/Google-Tag-Manager/ct-p/Google-Tag-Manager)
3. Contact GTM Support through the Gallery interface

---

**Good luck with your submission!** 🚀

