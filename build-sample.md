# DroidStar Android Build Sample Log

This document records the commands and output for a clean build of DroidStar for Android (arm64-v8a) on macOS.

## 1. Cleanup

**Command:**
```bash
rm -rf build_android
```

## 2. Configuration

**Command:**
```bash
export PATH=$HOME/Library/Android/sdk/cmake/4.1.2/bin:$PATH && ~/Qt/6.10.2/android_arm64_v8a/bin/qt-cmake . -B build_android -DANDROID_NDK_ROOT=$HOME/Library/Android/sdk/ndk/29.0.14206865 -DANDROID_SDK_ROOT=$HOME/Library/Android/sdk
```

**Output:**
```
-- Android toolchain file within NDK detected: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/build/cmake/android.toolchain.cmake
-- Android toolchain file within NDK detected: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/build/cmake/android.toolchain.cmake
-- The C compiler identification is Clang 21.0.0
-- The CXX compiler identification is Clang 21.0.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/toolchains/llvm/prebuilt/darwin-x86_64/bin/clang - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/toolchains/llvm/prebuilt/darwin-x86_64/bin/clang++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- Found Threads: TRUE
-- Performing Test HAVE_STDATOMIC
-- Performing Test HAVE_STDATOMIC - Success
-- Found WrapAtomic: TRUE
-- Performing Test HAVE_EGL
-- Performing Test HAVE_EGL - Success
-- Found EGL: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/toolchains/llvm/prebuilt/darwin-x86_64/sysroot/usr/include (found version "1.5")
-- Performing Test HAVE_GLESv2
-- Performing Test HAVE_GLESv2 - Success
-- Found GLESv2: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/toolchains/llvm/prebuilt/darwin-x86_64/sysroot/usr/include
-- Found WrapVulkanHeaders: /Users/daxiao/Library/Android/sdk/ndk/29.0.14206865/toolchains/llvm/prebuilt/darwin-x86_64/sysroot/usr/include
-- Configuring 'DroidStar' for the following Android ABIs: arm64-v8a (default)
CMake Warning (dev) at /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6CoreMacros.cmake:3530 (message):
  Qt policy QTP0002 is not set: Target properties that specify
  android-specific paths may contain generator expressions but they must
  evaluate to valid JSON strings.  Check
  https://doc.qt.io/qt-6/qt-cmake-policy-qtp0002.html for policy details.
  Use the qt_policy command to set the policy and suppress this warning.

Call Stack (most recent call first):
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6AndroidMacros.cmake:1153 (__qt_internal_setup_policy)
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6AndroidMacros.cmake:136 (_qt_internal_android_format_deployment_paths)
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6AndroidMacros.cmake:1699 (qt6_android_generate_deployment_settings)
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6CoreMacros.cmake:801 (_qt_internal_android_executable_finalizer)
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6CoreMacros.cmake:801 (cmake_language)
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6CoreMacros.cmake:879 (_qt_internal_finalize_executable)
  /Users/daxiao/Qt/6.10.2/android_arm64_v8a/lib/cmake/Qt6Core/Qt6CoreMacros.cmake:848:EVAL:1 (qt6_finalize_target)
  CMakeLists.txt:DEFERRED
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Found android platform plugin at: /Users/daxiao/Qt/6.10.2/android_arm64_v8a/plugins/platforms/libplugins_platforms_qtforandroid_arm64-v8a.so
-- Configuring done (2.4s)
-- Generating done (0.1s)
-- Build files have been written to: /Users/daxiao/code/DroidStar/build_android
```

## 3. Build

**Command:**
```bash
export JAVA_HOME="/opt/homebrew/opt/openjdk@21/libexec/openjdk.jdk/Contents/Home" && export PATH=$HOME/Library/Android/sdk/cmake/4.1.2/bin:$PATH && cmake --build build_android --parallel
```

**Output:**
```
[  1%] Populating .qmlls.ini file at /Users/daxiao/code/DroidStar/build_android/.qt/.qmlls.build.ini
[  2%] Copying DroidStar qml sources into build dir
[  3%] Copying DroidStar qml resources into build dir
[  3%] Built target qt_internal_plugins
[  3%] Built target DroidStar_copy_apk_dependencies
[  3%] Built target DroidStar_copy_qml
[  3%] Built target DroidStar_copy_res
[  3%] Built target generate_qmlls_build_ini_file
[  3%] Built target DroidStar_autogen_timestamp_deps
[  4%] Automatic MOC and UIC for target DroidStar
[  4%] Built target DroidStar_autogen
[  5%] Running AUTOMOC file extraction for target DroidStar
[  6%] Running rcc for resource DroidStar_raw_qml_0
[  8%] Generating .rcc/qmlcache/DroidStar_qmlcache_loader.cpp
[  9%] Running rcc for resource qmake_DroidStarApp
[  9%] Running moc --collect-json for target DroidStar
[ 10%] Generating meta_types/qt6droidstar_metatypes.json
[ 11%] Automatic QML type registration for target DroidStar
[ 12%] Generating .rcc/qmlcache/DroidStar_AboutTab_qml.cpp, .rcc/qmlcache/DroidStar_AboutTab_qml.cpp.aotstats
[ 13%] Generating .rcc/qmlcache/DroidStar_LogTab_qml.cpp, .rcc/qmlcache/DroidStar_LogTab_qml.cpp.aotstats
[ 15%] Generating .rcc/qmlcache/DroidStar_HostsTab_qml.cpp, .rcc/qmlcache/DroidStar_HostsTab_qml.cpp.aotstats
[ 16%] Generating .rcc/qmlcache/DroidStar_MainTab_qml.cpp, .rcc/qmlcache/DroidStar_MainTab_qml.cpp.aotstats
[ 17%] Generating .rcc/qmlcache/DroidStar_SettingsTab_qml.cpp, .rcc/qmlcache/DroidStar_SettingsTab_qml.cpp.aotstats
[ 18%] Generating .rcc/qmlcache/DroidStar_Main_qml.cpp, .rcc/qmlcache/DroidStar_Main_qml.cpp.aotstats
[ 19%] Building CXX object CMakeFiles/DroidStar.dir/DroidStar_autogen/mocs_compilation.cpp.o
...
[ 97%] Linking CXX shared module libDroidStar_arm64-v8a.so
[ 97%] Built target DroidStar
[ 98%] Copying DroidStar binary to apk folder
[ 98%] Built target DroidStar_prepare_apk_dir
[100%] Creating APK for DroidStar
Generating Android Package
  Input file: /Users/daxiao/code/DroidStar/build_android/android-DroidStar-deployment-settings.json
  Output directory: /Users/daxiao/code/DroidStar/build_android/android-build/
  Application binary: DroidStar
  Android build platform: android-36
  Install to device: No
BUILD SUCCESSFUL in 3s
33 actionable tasks: 33 executed
Android package built successfully in 9.576 ms.
  -- File: /Users/daxiao/code/DroidStar/build_android/android-build//build/outputs/apk/debug/android-build-debug.apk
[100%] Built target DroidStar_make_apk
[100%] Built target apk
[100%] Built target apk_all
```
