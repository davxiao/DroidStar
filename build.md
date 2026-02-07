# Building DroidStar for Android

This guide outlines the steps and dependencies required to build DroidStar for Android on macOS.

## Dependencies

Ensure the following tools are installed and configured:

1.  **JDK (Java Development Kit)**
    *   **Required Version**: JDK 17 or JDK 21. Java 25 is *too new* and causes build failures with current Gradle versions.
    *   **Installation**: `brew install openjdk@21`
    *   **Configuration**: Ensure `JAVA_HOME` points to your JDK installation.
        ```bash
        export JAVA_HOME="/opt/homebrew/opt/openjdk@21/libexec/openjdk.jdk/Contents/Home"
        ```

2.  **Qt Framework**
    *   **Version**: Qt 6.5+ (Tested with 6.10.2)
    *   **Required Modules**:
        *   Qt Multimedia
        *   Qt SerialPort
    *   **Installation**: Use the Qt Maintenance Tool to install Qt 6.10.2 for **Android** (e.g., `arm64_v8a`) and **macOS**, along with the required modules.

3.  **Android SDK & NDK**
    *   **Android SDK**: Typically located at `~/Library/Android/sdk`.
    *   **Android NDK**: Version 29 (tested with `29.0.14206865`). Install via Android Studio/SDK Manager ("NDK (Side by side)").

4.  **CMake**
    *   Use the `cmake` provided by the Android SDK or a recent version (3.22+).
    *   Path example: `~/Library/Android/sdk/cmake/3.22.1/bin/cmake`

5.  **External Libraries**
    *   **android_openssl**: Required for SSL support on Android.
        *   Clone into `3rdparty/android_openssl`:
            ```bash
            mkdir -p 3rdparty
            git clone https://github.com/KDAB/android_openssl.git 3rdparty/android_openssl
            ```

## Build Instructions

### 1. Configure Environment Variables
Set up your environment variables before building:

```bash
export JAVA_HOME="/opt/homebrew/opt/openjdk@21/libexec/openjdk.jdk/Contents/Home"
export ANDROID_HOME=$HOME/Library/Android/sdk
export ANDROID_NDK_ROOT=$ANDROID_HOME/ndk/29.0.14206865
export PATH=$JAVA_HOME/bin:$ANDROID_HOME/cmake/3.22.1/bin:$PATH
```

*(Adjust paths if your versions differ)*

### 2. Run CMake Configuration
Use the `qt-cmake` wrapper from your Qt Android kit.

```bash
~/Qt/6.10.2/android_arm64_v8a/bin/qt-cmake . -B build_android \
    -DANDROID_NDK_ROOT=$ANDROID_NDK_ROOT \
    -DANDROID_SDK_ROOT=$ANDROID_HOME
```

### 3. Build the APK
```bash
cmake --build build_android --parallel
```

### 4. Locate Output
The generated APK will be located at:
`build_android/android-build/build/outputs/apk/debug/android-build-debug.apk`

## Troubleshooting
*   **Java Version Error**: If you see "Unsupported class file major version", check that `JAVA_HOME` points to JDK 21 or 17, not a newer version.
*   **Missing Modules**: Ensure `QtMultimedia` and `QtSerialPort` are installed for the Android architecture you are building for.

## Development with Android Studio

If you wish to use Android Studio for debugging or further development:

1.  **Do NOT open the root `DroidStar` folder**. This is a C++/CMake project, and Android Studio may fail to correctly configure the Android SDK context for Java files, leading to errors like `package android.hardware.usb does not exist`.
2.  **Open the Generated Project**:
    *   Run the CMake configuration step first (Step 2 above).
    *   Navigate to the build directory: `build_android/android-build`.
    *   Open **this directory** in Android Studio.
    *   It will be recognized as a standard Gradle Android project, and Java formatting/symbol resolution will work correctly.

## Optional Features

The following optional features are currently disabled but can be investigated if needed:

### 1. MD380 Vocoder (`USE_MD380_VOCODER`)
*   **Description**: Adds support for AMBE+2 vocoder using firmware emulation.
*   **Status**: **Disabled in build**.
*   **Note**: For **Android arm64**, the `vocoder_plugin.android.arm64` is now **bundled** with the APK and loaded dynamically at runtime. No manual download or build configuration is needed for arm64.
*   **Legacy Info**: The library is strictly 32-bit ARM (`armeabi-v7a`). It is incompatible with `arm64-v8a` builds.

### 2. FLite TTS (`USE_FLITE`)
*   **Description**: Text-to-Speech support.
*   **Status**: **Disabled**.
*   **Requirement**: Requires cross-compiled `flite` libraries for Android.

