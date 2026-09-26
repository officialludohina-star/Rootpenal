# GitHub Setup Guide

## ✅ Step 1: Upload to GitHub

### Create New Repository
1. Go to [github.com](https://github.com)
2. Click **"New Repository"** button
3. Repository name: `RootPanel`
4. Description: `Free Fire Root Mod Panel - Auto-builds with GitHub Actions`
5. Click **"Create Repository"**

### Push Code to GitHub
```bash
# Navigate to project
cd RootPanel

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - Root panel with auto-build workflow"

# Add remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/RootPanel.git

# Push to GitHub
git branch -M main
git push -u origin main
```

---

## ⚙️ Step 2: GitHub Actions Setup

### Automatic Workflow
After pushing to GitHub:

1. Go to **Actions** tab
2. You'll see **"Build APK"** workflow
3. It automatically triggers on push
4. Check workflow status in **"Build APK"** action

### Workflow Triggers
The workflow runs automatically on:
- ✅ Push to `main` branch
- ✅ Push to `master` branch
- ✅ Push to `develop` branch
- ✅ Pull requests to these branches

---

## 📥 Step 3: Download Built APK

### From GitHub Actions

1. Go to **Actions** tab in your repository
2. Click **"Build APK"** workflow run
3. Scroll down to **"Artifacts"** section
4. Download **"app-debug.apk"**

### Installation
```bash
adb install app-debug.apk
```

Or via Android Studio:
1. Open Device File Explorer
2. Navigate to Downloads
3. Drag and drop APK to device

---

## 🔄 Step 4: Making Changes

### To Rebuild APK After Changes

1. Make changes to code (e.g., GameInjector.kt)
2. Commit and push:
   ```bash
   git add .
   git commit -m "Updated injection methods"
   git push origin main
   ```

3. GitHub Actions automatically builds new APK
4. Download from Actions → Artifacts

---

## 📤 Step 5: Create Release APK

### Create Git Tag (Release)
```bash
# Tag current commit
git tag v1.0.0

# Push tag to GitHub
git push origin v1.0.0
```

### Results
- GitHub Actions builds Release APK
- Auto-creates "Release" with APK attached
- Found in **"Releases"** section

---

## 🔑 Optional: Signing APK

### Generate Keystore (One-time)
```bash
keytool -genkey -v -keystore release.keystore \
    -alias release-key \
    -keyalg RSA -keysize 2048 -validity 10000
```

### Update build.gradle
```gradle
android {
    signingConfigs {
        release {
            keyAlias = 'release-key'
            keyPassword = 'YOUR_PASSWORD'
            storeFile = file('release.keystore')
            storePassword = 'YOUR_PASSWORD'
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
}
```

---

## 🚨 Troubleshooting

### Build Fails in GitHub Actions

**Check Logs:**
1. Go to **Actions** → **Build APK** → Failed workflow
2. Click **"build"** job
3. Expand logs to see error

**Common Issues:**

#### Java Version Error
```
Error: Android Gradle requires Java 11
```
✅ Solution: Already fixed in workflow (uses Java 11)

#### Gradle Wrapper Permission
```
Permission denied: ./gradlew
```
✅ Solution: Workflow already runs `chmod +x gradlew`

#### Build Tools Not Found
```
Error: Build tools version not found
```
✅ Solution: Update compileSdk in app/build.gradle:
```gradle
compileSdk 34  // Latest version
```

### APK Not Appearing in Artifacts

1. Check if build actually succeeded (green checkmark)
2. Check logs for errors
3. Verify `app/build/outputs/apk/debug/app-debug.apk` path exists

---

## 📝 Branch Management

### Development Workflow

```bash
# Create develop branch
git checkout -b develop
git push origin develop

# Make changes
git add .
git commit -m "New feature"
git push origin develop

# Create Pull Request on GitHub
# → Merge to main → Triggers build
```

---

## 🔐 GitHub Secrets (Optional)

For advanced features:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Create secrets for:
   - `KEYSTORE_PASSWORD`
   - `KEY_ALIAS_PASSWORD`

3. Use in workflow:
   ```yaml
   - name: Build Signed APK
     run: |
       ./gradlew assembleRelease \
       -Pandroid.injected.signing.key.password=${{ secrets.KEY_PASSWORD }} \
       -Pandroid.injected.signing.store.password=${{ secrets.STORE_PASSWORD }}
   ```

---

## 📊 Workflow Monitoring

### View Build History
1. **Actions** tab
2. **Build APK** workflow
3. See all build attempts with timestamps

### Email Notifications
- GitHub sends email on workflow failure
- Configure in **Settings** → **Notifications**

---

## 🎉 Complete!

You now have:
- ✅ GitHub repository with full source code
- ✅ Automated APK building with GitHub Actions
- ✅ Easy APK downloads from Artifacts
- ✅ Version releases for final builds
- ✅ Change tracking with git commits

**Just push code → APK builds automatically!** 🚀

---

## 📚 Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Android Gradle Documentation](https://developer.android.com/studio/build)
- [Git Documentation](https://git-scm.com/doc)

**Happy coding!** 🎮
