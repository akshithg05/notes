# 1. Build the React app

cd c:\Users\gunashee\Documents\Learning\todo-app

npm run build

  
# 2. Sync to Android

npx cap sync android

# 3. Set JAVA_HOME and build APK

$env:JAVA_HOME = "C:\Program Files\Android\Android Studio\jbr"

cd android

.\gradlew assembleDebug

  
# APK location:

# android\app\build\outputs\apk\debug\app-debug.apk