# Garudaname: Android CI

on:
  push:
    branches:
      - main

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Checkout source
      uses: actions/checkout@v2

    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: '11'
        distribution: 'adopt'

    - name: Grant execute permission for gradlew
      run: chmod +x ./gradlew

    - name: Build with Gradle
      run: ./gradlew assembleDebug

    - name: Upload APK
      uses: actions/upload-artifact@v2
      with:
        name: GarudaRayaNews.apk
        path: app/build/outputs/apk/debug/app-debug.apk

