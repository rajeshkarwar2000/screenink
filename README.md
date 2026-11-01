name: Build APK
on: [workflow_dispatch, push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with: {distribution: temurin, java-version: 17}
      - uses: gradle/actions/setup-gradle@v4
        with: {gradle-version: 8.7}
      - run: unzip -q ScreenInk-android-project.zip
      - run: cd ScreenInk && gradle assembleDebug --no-daemon
      - uses: actions/upload-artifact@v4
        with: {name: ScreenInk-apk, path: ScreenInk/app/build/outputs/apk/debug/app-debug.apk}
