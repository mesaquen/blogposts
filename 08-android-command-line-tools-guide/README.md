# Android SDK command line tools only

You can easily find jokes related to Android Studio, the amount of RAM
it consumes, and computer overheating. I've always been someone who
tries to keep the minimum of installed programs or running on my daily
basis. During React Native app development, especially in projects that
don't use Expo, it's common to have to install a full package with IDE
to open the local emulator.

The truth is, you don't always need Android Studio, just some
command-line tools that come with it.

A few years ago, when I discovered this, I looked for a guide on how to
configure the environment in this way, but I found scattered information
or missing information. It was difficult, but I managed to make it work.
Seeing the complexity of the steps and predicting that the next time I
needed to do something similar, my future self would probably not
remember the steps, I created a guide to help me with these
configuration steps.

Time passed, the SDK was updated, some tools and syntaxes changed, and
my guide became outdated.

To solve this, I rewrote the guide, created a public project on GitHub,
and made it available there.

A PDF version of this guide is available in both English and Brazilian
Portuguese on the [GitHub
repository](https://github.com/mesaquen/android-cmdline-tools-guide/).

## Android SDK install guide

This guide was created to assist in setting up the development
environment for Android mobile applications. My current environment is
based on GNU/Linux, but I believe the steps described here can be
adapted to your reality on other operating systems.

If you have any questions or suggestions, feel free to contact me
through my GitHub ([@mesaquen](https://github.com/mesaquen)).

## Command line tools

- Go to [android sdk download
  page](https://developer.android.com/studio#downloads)
- Look for "Command line tools only"
- Download the commandline tools for your operating system

### Extracting and setting up the environment variables

Create a directory named `.android_sdk` and extract the command line
tools you downloaded earlier:

```code
mkdir .android_sdk
unzip commandlinetools-linux-9477386_latest.zip -d ~/.android_sdk/
```

Export the following environment variables in your .bashrc file:

```code
export ANDROID_SDK_ROOT="$HOME/.android_sdk"
export PATH="$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$PATH"
export PATH="$ANDROID_SDK_ROOT/emulator:$PATH"
```

### Install the latest cmdline-tools

```code
$ANDROID_SDK_ROOT/cmdline-tools/bin/sdkmanager \
--sdk_root=$ANDROID_SDK_ROOT "cmdline-tools;latest"
```

Once you've installed the command line tools, the sdkmanager should be
able to recognize the SDK location, and you won't need to provide the
sdk_root flag anymore.

### Install the platforms, build-tools and extras

```code
sdkmanager "platforms;android-33" "build-tools;33.0.2"
sdkmanager "extras;google;m2repository" "extras;android;m2repository"
sdkmanager "platform-tools" "tools"
sdkmanager --licenses
```

## Installed packages

To see a list of the installed packages, run:

```code
sdkmanager --list_installed
```

## AVD: Android Virtual Device

Before creating an AVD, you'll need to download the system images. To
see a list of available images, run:

```code
sdkmanager --list | grep system-images
```

### Install the chosen system image

```code
sdkmanager "system-images;android-33;google_apis_playstore;x86_64"
```

### Creating the AVD

Create an AVD using the following command:

```code
avdmanager create avd -n device \
--device pixel -k "system-images;android-33;google_apis_playstore;x86_64"
```

To get a list of available virtual devices, run:

```code
avdmanager list avd
```

## Emulator

You can start the emulator by passing the name of the AVD with the
command:

```code
emulator @device
```

Here "device" is the name of the AVD.
