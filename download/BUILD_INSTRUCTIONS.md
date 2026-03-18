# GTA SA Dev Mod - تعليمات البناء

## المتطلبات الأساسية

### 1. تثبيت Android Studio
قم بتنزيل وتثبيت Android Studio من:
https://developer.android.com/studio

### 2. تثبيت Android SDK
- افتح Android Studio
- اذهب إلى `Settings > Appearance & Behavior > System Settings > Android SDK`
- قم بتثبيت:
  - Android SDK 35
  - Android NDK 25.2.9519653
  - CMake 3.22.1+
  - Android SDK Build-Tools 35
  - Android SDK Platform-Tools

### 3. متغيرات البيئة
```bash
# Linux/macOS
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin

# Windows
setx ANDROID_HOME "%LOCALAPPDATA%\Android\Sdk"
```

## خطوات البناء

### الطريقة 1: باستخدام Android Studio

1. **فتح المشروع**
   ```bash
   # استخراج الملفات
   tar -xzvf GTASADevMod_Source.tar.gz
   ```

2. **فتح في Android Studio**
   - افتح Android Studio
   - اختر `Open an existing project`
   - حدد مجلد `GTASADevMod`

3. **انتظار المزامنة**
   - سيقوم Android Studio بتنزيل Gradle والتبعيات تلقائياً
   - انتظر حتى تنتهي المزامنة

4. **بناء APK**
   - اذهب إلى `Build > Build Bundle(s) / APK(s) > Build APK(s)`
   - أو استخدم: `Build > Generate Signed Bundle / APK` لإنشاء APK موقع

5. **العثور على APK**
   - المسار: `GTASADevMod/app/build/outputs/apk/debug/app-debug.apk`

### الطريقة 2: باستخدام سطر الأوامر

```bash
cd GTASADevMod

# منح صلاحيات التنفيذ
chmod +x gradlew

# بناء APK Debug
./gradlew assembleDebug

# بناء APK Release (يتطلب توقيع)
./gradlew assembleRelease
```

## ملف APK الناتج

- **Debug APK**: `app/build/outputs/apk/debug/app-debug.apk`
- **Release APK**: `app/build/outputs/apk/release/app-release.apk`

## هيكل المشروع

```
GTASADevMod/
├── app/
│   ├── src/main/
│   │   ├── java/com/gtasa/devmod/    # كود Kotlin/Java
│   │   ├── cpp/                       # كود C++ الأصلي
│   │   ├── res/                       # الموارد
│   │   └── AndroidManifest.xml
│   └── build.gradle.kts
├── build.gradle.kts
├── settings.gradle.kts
├── README.md
└── LICENSE
```

## الميزات المضمنة

| الميزة | الوصف |
|--------|-------|
| Crash Reporter | تقارير أعطال محفوظة بوقت |
| Android 15 Support | متوافق مع أحدث إصدار |
| Auto TXD Detection | اكتشاف تلقائي لملفات TXD |
| CPU Arch Detection | اكتشاف معمارية المعالج |
| CLEO Support | دعم سكربتات CLEO |
| High Mem Mode | دعم المودات الثقيلة |

## دليل المستخدم بعد التثبيت

### هيكل المجلدات
```
/sdcard/GTA_SA_Dev/
├── textures/     # ملفات TXD و IMG
├── models/       # ملفات DFF و COL
├── cleo/         # سكربتات CLEO
├── configs/      # ملفات الإعدادات
└── logs/         # سجلات الأعطال
```

### إعدادات settings.ini
```ini
[Performance]
EnableHighMemMode = true
MaxHeapSizeMB = 512

[Modding]
AutoLoadTXD = true
CLEOEnabled = true
```

## حل المشاكل الشائعة

### خطأ: SDK not found
```bash
# تأكد من تثبيت Android SDK
echo $ANDROID_HOME
```

### خطأ: NDK not found
```bash
# ثبّت NDK من Android Studio SDK Manager
```

### خطأ: CMake not found
```bash
# ثبّت CMake من Android Studio SDK Manager
```

## الاتصال والدعم

- **GitHub**: https://github.com/GTASA-DevMod/GTA-SA-Dev-Mod
- **Issues**: للأبلاغ عن المشاكل

---

**ملاحظة**: هذا المشروع للأغراض التعليمية فقط. تأكد من امتلاك نسخة أصلية من GTA San Andreas Android.
