# RootPanel - Free Fire Root Mod Menu

Complete Android root panel for Free Fire game injection. Built with Kotlin and ready for GitHub Actions automated building.

## 📋 Requirements

- **Android Device**: Rooted with Magisk
- **Free Fire**: Installed on device
- **Min SDK**: 24 (Android 7.0)
- **Target SDK**: 34 (Android 14)

## 🚀 Features

✅ **Root Access Check**
- Automatic Magisk detection
- Permission request handling

✅ **Aim Features**
- Aim Bot with smoothness control
- Silent Aim
- Auto Aim
- Headshot Only Mode

✅ **ESP Features**
- ESP Box
- ESP Line
- ESP Name (FIXED)
- ESP Health (FIXED)
- ESP Distance
- Field of View (FOV) Control

✅ **Real-time Controls**
- Smooth slider (real-time adjustment)
- FOV slider (real-time adjustment)
- Toggle buttons for each feature

## 📱 Installation

### Method 1: GitHub Actions (Automated)

1. **Fork Repository**
   ```
   Click "Fork" button on GitHub
   ```

2. **GitHub Actions Workflow**
   - Push to `main` branch
   - Workflow automatically builds APK
   - Download from "Actions" → "Build APK" → "Artifacts"

3. **Install on Device**
   ```bash
   adb install app-debug.apk
   ```

### Method 2: Local Android Studio

1. **Clone Repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/RootPanel.git
   cd RootPanel
   ```

2. **Open in Android Studio**
   - File → Open → Select RootPanel folder

3. **Build**
   - Build → Build Bundle(s) / APK(s) → Build APK(s)

4. **Install**
   - Run → Run 'app'

## 🔧 Project Structure

```
RootPanel/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/rootpanel/freefire/
│   │   │   │   ├── MainActivity.kt (UI & Logic)
│   │   │   │   ├── GameInjector.kt (Injection Methods)
│   │   │   │   └── RootUtils.kt (Root Commands)
│   │   │   └── AndroidManifest.xml
│   │   └── res/ (Layouts, Strings, etc.)
│   └── build.gradle (App Configuration)
├── .github/workflows/
│   └── build.yml (GitHub Actions)
├── build.gradle (Project Configuration)
├── settings.gradle
├── gradle.properties
└── README.md
```

## 📝 File Descriptions

### `MainActivity.kt`
- Main UI implementation
- Root permission handling
- Feature toggles and listeners
- Real-time slider controls

### `GameInjector.kt`
- All injection methods
- Free Fire package detection
- Root command execution
- Feature enable/disable

### `RootUtils.kt`
- Root access testing
- Command execution
- Package installation checking
- PID retrieval

## 🔐 Security Notes

⚠️ **WARNING**: This app requires root access and injects into another application.
- Only use on your own device
- Requires Magisk root
- May violate Free Fire Terms of Service

## 🛠️ Configuration

### Change Package Name
Edit `app/build.gradle`:
```gradle
applicationId "com.rootpanel.freefire"  // Change this
```

### Change App Name
Edit `app/src/main/res/values/strings.xml`:
```xml
<string name="app_name">RootPanel</string>  <!-- Change this -->
```

## 📦 Building Release APK

### Local Build
```bash
./gradlew assembleRelease
# Output: app/build/outputs/apk/release/app-release.apk
```

### GitHub Actions Release
1. Create tag: `git tag v1.0.0`
2. Push: `git push origin v1.0.0`
3. APK auto-releases in GitHub Releases

## 🐛 Troubleshooting

### "Root Permission Denied"
- Check Magisk is installed
- Grant root permission to app in Magisk Manager

### "Free Fire Not Detected"
- Ensure Free Fire is installed
- Try: `adb shell pm list packages | grep freefire`

### Build Fails
- Update Android Studio
- Clear cache: `./gradlew clean`
- Update gradle: `gradle wrapper --gradle-version latest`

## 📞 Support

For issues and questions:
1. Check GitHub Issues
2. Review code comments (Urdu comments included)
3. Check manifesto requirements

## 📜 License

This project is provided as-is for educational purposes.

---

**Made with ❤️ for Magisk-Rooted Devices**

🎮 **Happy Modding!**
