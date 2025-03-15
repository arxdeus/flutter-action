# flutter-action

Flutter lightweight environment for use in GitHub Actions. It works on Linux, Windows, and
macOS.

Originally created by [Alif Rachmawadi] and [Bartek Pacia].

Currently maintained by [Artemis Kushner](https://github.com/arxdeus)

Code taken from https://github.com/PlugFox/docker_flutter, big thanks for [Mike Matyunin](https://github.com/plugfox)

The following sections show how to configure this action.

## Specifying Flutter version

### Use specific version and channel

```yaml
steps:
  - name: Clone repository
    uses: actions/checkout@v4
  - name: Set up Flutter
    uses: arxdeus/flutter-action@v1
    with:
      flutter-version: 3.19.0
  - run: flutter --version
```

### Use alternative Flutter repository

This action supports "alternative Flutters" in addition to the official
[`flutter/flutter`](https://github.com/flutter/flutter), for example:
- [Flock](https://github.com/Flutter-Foundation/flutter.git)
- [a Flutter fork that supports
  HarmonyOS](https://gitee.com/harmonycommando_flutter/flutter.git)

```yaml
steps:
  - name: Clone repository
    uses: actions/checkout@v4
  - name: Set up Flutter
    uses: arxdeus/flutter-action@v1
    with:
      flutter-version: 3.24.0
      git-source: https://github.com/Flutter-Foundation/flutter.git
  - run: flutter --version
```


## Build targets

Build **Android** APK and app bundle:

```yaml
steps:
  - name: Clone repository
    uses: actions/checkout@v4
  - name: Set up Flutter
    uses: arxdeus/flutter-action@v1
    with:
      flutter-version: 3.29.2
  - run: flutter pub get
  - run: flutter test
  - run: flutter build apk
  - run: flutter build appbundle
```

### Build for iOS

> [!NOTE]
>
> Building for iOS requires a macOS runner.

```yaml
jobs:
  main:
    runs-on: macos-latest
    steps:
      - name: Clone repository
        uses: actions/checkout@v4
      - name: Set up Flutter
        uses: arxdeus/flutter-action@v1
        with:
          flutter-version: 3.29.2
      - run: flutter pub get
      - run: flutter test
      - run: flutter build ios --release --no-codesign
```

### Build for the web

```yaml
steps:
  - name: Clone repository
    uses: actions/checkout@v4
  - name: Set up Flutter
    uses: subosito/flutter-action@v2
    with:
      flutter-version: 3.29.2
  - run: flutter pub get
  - run: flutter test
  - run: flutter build web
```

### Build for Windows

```yaml
jobs:
  main:
    runs-on: windows-latest
    steps:
      - name: Clone repository
        uses: actions/checkout@v4
      - name: Set up Flutter
        uses: arxdeus/flutter-action@v1
        with:
          flutter-version: 3.29.2
      - run: flutter build windows
```

### Build for Linux desktop

```yaml
jobs:
  main:
    runs-on: ubuntu-latest
    steps:
      - name: Clone repository
        uses: actions/checkout@v4
      - name: Set up Flutter
        uses: arxdeus/flutter-action@v1
        with:
          flutter-version: 3.29.2
      - run: |
          sudo apt-get update -y
          sudo apt-get install -y ninja-build libgtk-3-dev
      - run: flutter build linux
```

### Build for macOS desktop

> [!NOTE]
>
> Building for macOS requires a macOS runner.

```yaml
jobs:
  main:
    runs-on: macos-latest
    steps:
      - name: Clone repository
        uses: actions/checkout@v4
      - name: Set up Flutter
        uses: arxdeus/flutter-action@v1
        with:
          flutter-version: 3.29.2
      - run: flutter build macos
```

[Alif Rachmawadi]: https://github.com/subosito
[Bartek Pacia]: https://github.com/bartekpacia
[Artemis Kushner]: https://github.com/arxdeus
[Mike Matyunin]: https://github.com/plugfox
