# Deprecated - [See here for new build script](https://github.com/Zackptg5/Curl-and-Aria2-For-Android)

# curl-boringssl-android

Compiles curl (and dependencies ) for Android

Dynamic linking (default) has most features, static has some removed due to various issues/incompatibilities

## Prerequisites

Linux (I've tested this on Manjaro)

autoconf,libtool,go,ninja

## Download

If you do not want to compile them yourself, you can download pre-compiled static binaries from [Cross-Compiled-Binaries-Android](https://github.com/Zackptg5/Cross-Compiled-Binaries-Android).<br/>
Doing your own compilation is recommended, since the pre-compiled binary can become outdated soon.<br/>

Update git submodules to compile newer versions of the libraries:
```
cd submodule_directory
git checkout LATEST_STABLE_TAG
cd ..
```

## Usage

```
bash
git clone --recurse-submodules https://github.com/Zackptg5/curl-boringssl-android.git
```
Optional: Update git submodules to compile newer versions of the libraries:
```
cd submodule_directory
git checkout LATEST_STABLE_TAG
cd ..
```
Edit build.sh script:
```
NDK=android_ndk_version_you_want_to_use
export HOST_TAG=see_this_table_for_info # https://developer.android.com/ndk/guides/other_build_systems#overview
export MIN_SDK_VERSION=21 # or any version you want (dependent on the ndk version - keep 21 if in doubt)
export STATIC=false #Change to true for static binary - note that there will be less features then with dynamic
export ARCH="arm arm64 x86 x64" # Remove ones you don't want to compile
```
Run build script
```
chmod +x ./build.sh
./build.sh
```
All compiled libs are located in `build` directory.

## Options

Change scripts' configure arguments to meet your requirements.

Note that https has been fixed now in Android so the `peer verification failed` message no longer occurs. The solution was to set `--with-ca-path=/system/etc/security/cacerts` configure flag and to use boringssl instead of openssl

## Issues

Curl has weird DNS error in Android Q when not run as superuser

## Working Example

Checkout this [repo](https://github.com/robertying/CampusNet-Android/blob/master/app/src/main/cpp/jni) to see how to integrate compiled static libraries into an existing Android project, including `Android.mk` setup and `JNI` configurations.

## Credits of Originality:

This is a fork of the original here: https://github.com/robertying/openssl-curl-android
