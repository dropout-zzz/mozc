---

this is a tree trying to make the old ver buildable again

other changes may come in future and if so ill add it to this document

so far they're:
 * bumping targetSdk to Android 7 (no other code change required)
   tested to install and work just fine on Android 16

todo list, some are non-trivial:
 * bump target api to even higher
 * modernize build system and migrate to androidx
 * bump dependencies
 * remove jar binaries in tree
 * sync mozc and dict updates from upstream
 * update emoji and kaomoji tables
 * material 3
 * add github ci
 * system light/dark mode handling

note that the fdroid packaging and archlinux `fcitx5-mozc` packaging included "not really FOSS licensed" zipcode dictionary files, however these are actually not copyrighted, free to redistribute and modify
moreover these dictionaries are not useful unless you live in japan, IMO

there are actually some cool FOSS alternatives to "Mozc for Android", so this repo is for who wanna stick with it for all kind of reasons ^^;

---

obviously this git tree has some binaries in it
but not much concerning as far as i know, for example the jar in tree is seemingly just downloaded from some maven repo
and im too lazy to clean those up

u may also notice mozc has some peak huge squashed(?) commits in history

so this code is all old, yadayada, you're warned, but obviously im not responsible for anything

---

we can guess google deprecated "mozc for android" is because the merge with gboard
which probably made it hard to maintain two different code base

at time of writing, fdroid only has arm32 build of this,
i can guess packager didnt know other arches can be built or not interested in that
we can guess the interest/effort been stopped on fdroid side since that...

this can still be built using the docker setup! thanks to the GrapheneOS thread and ppl on there who shared this info
also thanks to who made the japanese blog post about building this in modern times linked in the thread.

just a small note this can still be installed and work on modern android if you use --bypass-low-target-sdk-block

---

in order to build arches other than arm32, check `build_mozc.py gyp --help`

---

seems like google deprecated "mozc for android" in 2018 which is before "google japanese input" stops updating on google play in 2020

my observation is code in OSS repo have stopped feature updates in around 2016, as you can see the app looks identical to a build of "google japanese input" in 2016 (except online dictionary updating feature and telemetry options)

for the gplay ver, google later added better theme support and revamped ui, and it has higher target api (Android 11)
the theme stuff looks the same as in gboard, and similar to what is already implemented in Fcitx5-Android today

---

it is possible to use georgewfraser/java-language-server to provide code completion for development
this is tested within KDE Kate

build the project first and add these jars into classpath:

  ./src/android/libs/android-support-v13.jar
  ./src/android/libs/guava.jar
  ./src/android/libs/jsr305.jar
  ./src/android/libs/protobuf-java.jar

(also android.jar from android sdk)

you also need some generated source files

in ./src/android/resources/gen, grab these:

  org/mozc/android/inputmethod/japanese/resources/R.java
  org/mozc/android/inputmethod/japanese/resources/BuildConfig.java

in ./src/android/gen, grab these:

  org/mozc/android/inputmethod/japanese/R.java
  org/mozc/android/inputmethod/japanese/BuildConfig.java
  org/mozc/android/inputmethod/japanese/protobuf/ProtoEngineBuilder.java
  org/mozc/android/inputmethod/japanese/protobuf/ProtoCandidates.java
  org/mozc/android/inputmethod/japanese/protobuf/ProtoCommands.java
  org/mozc/android/inputmethod/japanese/protobuf/ProtoConfig.java
  org/mozc/android/inputmethod/japanese/protobuf/ProtoUserDictionaryStorage.java
  org/mozc/android/inputmethod/japanese/SymbolData.java
  org/mozc/android/inputmethod/japanese/EmoticonData.java
  org/mozc/android/inputmethod/japanese/emoji/EmojiData.java

simply copy those files into your src/android/src

---

issues:
 * "This app was built for an older version of Android" warning
   but the app IS working as expected and its misleading.
   this can be suppressed by bumping target api to 28.
   it works, but that would cause a ui bug.
   need to figure out why.

 * localizations for many languages exist in tree
   but not compiled for some reasons

bugs to fix:
 * "Next" button in "Please change input method to Mozc" popup
   sometimes does not bring up system settings.

---
