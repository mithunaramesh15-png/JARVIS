name: Build Jarvis app

on:
  push:
  workflow_dispatch:

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Unpack app code
        run: unzip -o jarvis-src.zip -d src
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.7'
      - name: Build the app
        working-directory: src
        run: gradle assembleRelease --no-daemon
      - name: Rename app file
        run: cp src/app/build/outputs/apk/release/app-release.apk Jarvis.apk
      - name: Publish for download
        uses: softprops/action-gh-release@v2
        with:
          tag_name: v${{ github.run_number }}
          name: Jarvis v${{ github.run_number }}
          files: Jarvis.apk
          make_latest: true
