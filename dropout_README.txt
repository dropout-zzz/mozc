---

this is a tree trying to make the old ver buildable again

other changes may come in future and if so ill add it to this document

so far they're:
 * bumping targetSdk to Android 7 (no other code change required)
   tested to install and work just fine on Android 16

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
