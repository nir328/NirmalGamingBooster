NirmalGamingBooster-AndroidStudio-Project.zipunzip -o NirmalGamingBooster-AndroidStudio-Project.zipmkdir -p .github/workflows

cat > .github/workflows/android.yml <<'EOF'
name: Build Nirmal Gaming Booster APK

on:
  workflow_dispatch:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source
        uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Setup Gradle
        uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'

      - name: Setup Android SDK
        uses: android-actions/setup-android@v3

      - name: Install Android SDK packages
        run: sdkmanager "platforms;android-35" "build-tools;35.0.0"

      - name: Build Debug APK
        working-directory: NirmalGamingBooster
        run: gradle assembleDebug

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: Nirmal-Gaming-Booster-APK
          path: NirmalGamingBooster/app/build/outputs/apk/debug/app-debug.apk
EOF# NirmalGamingBooster
Nirmal Gaming Booster Android App

