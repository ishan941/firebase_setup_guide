

### 1. Install Dependencies

```bash
flutter pub get
```

### 2. Change Package Name (Required for Play Store)

```bash
flutter pub run change_app_package_name:main com.nextstep.app
```

_Replace `com.nextstep.app` with your desired package name_

### 3. Install Firebase CLI

Install Node.js dependencies:

```bash
npm install -g npm
npm install -g firebase-tools@latest
```

**For macOS users, use:**

```bash
sudo npm install -g firebase-tools@latest
```

**For Windows users:**

1. Open PowerShell as Administrator
2. Run: `Set-ExecutionPolicy RemoteSigned`
3. Press Y and Enter to confirm

### 4. Install FlutterFire CLI

```bash
dart pub global activate flutterfire_cli
```

Add Dart global packages to your PATH:

- **Windows**: Add `C:\Users\[USERNAME]\AppData\Local\Pub\Cache\bin` to system variables
- **macOS/Linux**: Usually automatically added to PATH

### 5. Firebase Authentication

```bash
firebase login
```

### 6. Configure FlutterFire

```bash
flutterfire configure --project=your-firebase-project-id
```

_Replace `your-firebase-project-id` with your actual Firebase project ID_

### 7. Add Firebase Dependencies

```bash
flutter pub add firebase_core
flutter pub add firebase_auth
flutter pub add cloud_firestore
```

## 🔥 Firebase Setup

### 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project
3. Add your iOS and/or Android app

### 2. Download Configuration Files

**For Android:**

- Download `google-services.json`
- Place it in `android/app/google-services.json`

**For iOS:**

- Download `GoogleService-Info.plist`
- Add it to your Xcode project in the `Runner` folder

### 3. Configure Android

Update `android/build.gradle`:

```gradle
dependencies {
    classpath 'com.google.gms:google-services:4.3.15'
}
```

Update `android/app/build.gradle`:

```gradle
apply plugin: 'com.google.gms.google-services'
```

### 4. Initialize Firebase in main.dart

```dart
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(MyApp());
}
```

## 🏗️ Project Structure

```
lib/
├── main.dart                 # App entry point
├── counter_app.dart         # Counter application
├── counter_app2.dart        # Alternative counter implementation
├── counter_provider.dart    # Counter state management
├── enum.dart               # Application enums
├── firebase_options.dart   # Firebase configuration
├── login/                  # Authentication module
│   ├── login_page.dart
│   ├── login_provider.dart
│   ├── signup_page.dart
│   └── signup_provider.dart
├── task_app/              # Task management module
│   ├── task_app.dart
│   └── task_app_provider.dart
└── widgets/               # Reusable widgets
    └── custom_text_form_field.dart
```
