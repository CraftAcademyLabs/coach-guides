- go to: https://www.oracle.com/java/technologies/javase-jdk15-downloads.html

- download the version for the Linux Debian Package
- open it and install 

- go to https://developer.android.com/studio and install android studio

- go to the terminal and:
```
android-studio/bin/studio.sh
```
- make sure they tab their way to that so it really exists

- just press enter on everything, if there is a choice they can choose by themselves 

- run the same command again: 
```
android-studio/bin/studio.sh
```
- go to `configure` and `Create new desktop entry`

- go to `configure` and `SDK manager`
- choose `Android 10`

- go to SDK tools and show package details and choose 29.0.2

```
code .zshrc
```

- Put this in there: 
```
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```
- restart terminal

- go to android studio and configure and AVD manager 
- the phone doesn't matter but for the next you download `Q` and then choose it when the installation is done

- open the .zshrc again and put in: 
```
export JAVA_HOME="/home/emma/android-studio/jre/"
```
- to get the current path in linux do pwd 

