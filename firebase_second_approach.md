
#

#

# Second Approach

#

#

#

# Firebase Setup

### 1. Change package name com.example.app is not supported in play store

run this command :
`flutter pub run  change_app_package_name:main com.devotixs.app`

### 2. Add project in firebase (gradle)

### 3. Download and install node js and set enviroment variable(new )then run this command

Open your browser and go to: https://nodejs.org

You’ll see two versions:

LTS (Recommended for most users) → stable version

`npm install -g npm`

`npm install -g firebase-tools`
// write sudo in front of this line in Mac

or

`npm install -g firebase-tools@latest`

### 5. Open windows powershell window as an administrator

run command
`Set-ExecutionPolicy RemoteSigned`  
 Press `Y` and then press Enter to confirm the change.

// ➡️ You are telling PowerShell:

// "Allow me to run my own scripts, but still block unsigned scripts from the internet for safety."

### 6. firebase login

### 7. Install the FlutterFire CLI by running the following command from any directory:

or
Open firebase console

```bash
dart pub global activate flutterfire_cli
```

```bash
flutterfire configure --project=fir-test-b8c6b
```

### 8. Add to system environment variable

`C:\Users\GF 65\AppData\Local\Pub\Cache\bin`

After that run:

```bash
flutter pub add firebase_core
flutterFire configure
flutter pub add firebase_auth
flutter pub add cloud_firestore
```

### 11. Add in main.dart

```WidgetsFlutterBinding.ensureInitialized();
await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
```

# Congraluation your firebase setup has been completed

## Now Whats next?

### 🔹 1. Setup Firebase in Flutter

Go to Firebase Console
, `create a project`.

Add your iOS and/or Android app.

Download `google-services.json` (for Android) and
` GoogleService-Info.plist` (for iOS), and place them correctly:

Android → `android/app/google-services.json`

iOS → `Xcode → Runner → Add GoogleService-Info.plist`

## Update Gradle files for Android:

// android/build.gradle

```
dependencies {
classpath 'com.google.gms:google-services:4.3.15'
}
```

// android/app/build.gradle
apply plugin: 'com.google.gms.google-services'

Add dependencies in pubspec.yaml:

```
dependencies:
flutter:
sdk: flutter
firebase_core: ^3.5.0
firebase_auth: ^5.2.0
provider: ^6.1.2
```

```
class SignupProvider with ChangeNotifier {
final FirebaseAuth _auth = FirebaseAuth.instance;

bool _isLoading = false;
bool get isLoading => _isLoading;

Future<String?> signUp(String email, String password) async {
try {
_isLoading = true;
notifyListeners();

      await _auth.createUserWithEmailAndPassword(
        email: email,
        password: password,
      );

      _isLoading = false;
      notifyListeners();
      return null; // success
    } on FirebaseAuthException catch (e) {
      _isLoading = false;
      notifyListeners();
      return e.message; // return error message
    }

}
}
```

```
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'signup_provider.dart';

class SignupPage extends StatelessWidget {
const SignupPage({super.key});

@override
Widget build(BuildContext context) {
final emailController = TextEditingController();
final passwordController = TextEditingController();

    return Scaffold(
      appBar: AppBar(
        title: const Text("Sign Up"),
      ),
      body: Center(
        child: Padding(
          padding: const EdgeInsets.all(16.0),
          child: Consumer<SignupProvider>(
            builder: (context, provider, _) => Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                TextField(
                  controller: emailController,
                  decoration: const InputDecoration(labelText: "Email"),
                ),
                const SizedBox(height: 16),
                TextField(
                  controller: passwordController,
                  decoration: const InputDecoration(labelText: "Password"),
                  obscureText: true,
                ),
                const SizedBox(height: 16),
                provider.isLoading
                    ? const CircularProgressIndicator()
                    : ElevatedButton(
                        onPressed: () async {
                          final msg = await provider.signUp(
                            emailController.text.trim(),
                            passwordController.text.trim(),
                          );

                          if (msg == null) {
                            ScaffoldMessenger.of(context).showSnackBar(
                              const SnackBar(
                                  content: Text("Signup successful!")),
                            );
                          } else {
                            ScaffoldMessenger.of(context).showSnackBar(
                              SnackBar(content: Text(msg)),
                            );
                          }
                        },
                        child: const Text("Sign Up"),
                      ),
              ],
            ),
          ),
        ),
      ),
    );

}
}
```
