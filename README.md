
Audiowand
=========

A very simple audio tour app built with Cordova

n.b. This is early days - don't get excited!

Setting up a Tour build environment
===================================

* Use Cordova CLI to build the app
        https://cordova.apache.org/docs/en/4.0.0/guide_cli_index.md.html
* Create a Cordova application e.g.
        cordova create glasshouses uk.org.rbge.hyam.audiowand.glasshouses Glasshouses
* Add the media plugin and others - the file plugin will be auto added
        
        com.cordova.background-audio 1.0.0 "background-audio"
        cordova-plugin-device 1.0.1 "Device"
        cordova-plugin-geolocation 1.0.1 "Geolocation"
        cordova-plugin-media 1.0.1 "Media"
        cordova-plugin-splashscreen 2.1.0 "Splashscreen"
        cordova-plugin-statusbar 1.0.1 "StatusBar"
        
* Add the platforms
        cordova platform add ios
        cordova platform add android
* Clone a copy of audiowand into the application directory (not www)
        git clone https://github.com/rogerhyam/audiowand
* Copy the update_core.sh script from the cloned repository to your Cordova project directory and run it.
    cp audiowand/update_core.sh .
    chmod +x update_core.sh
    ./update_core.sh
* (You can run the update_core script anytime you think the git repository might have changed)
* Initialise your data directory with the test data from the core build you only want to do this once at the beginning!
    cp -r audiowand/data/* www/data
* Get a copy of the config.xml in the www and remove the Cordova one. We use one in the WWW to make it simpler with Phonegap 
    rm config.xml
    cp audiowand/config.xml www/config.xml
* Build it e.g.
    cordova build android
* We are now free to change anything under www/data and the www/config.xml. Other files will be overwritten by update_core.sh

Cordova Plugins Required
========================
org.apache.cordova.file 1.3.3 "File"
org.apache.cordova.media 0.2.16 "Media"
org.apache.cordova.device 0.3.0 "Device"
org.apache.cordova.splashscreen 1.0.0 "Splashscreen"
org.apache.cordova.statusbar 0.1.10 "StatusBar"

Useful for Debug
================
cd /Users/rogerhyam/android-sdks/platform-tools
./adb  logcat CordovaLog:D *:S


Creating Synthesised Voice on a Mac
===================================
There is a directory in www/data/script that can be used for managing the audio scripts. There is a bash script in there for generating synthetic voice for testing on a mac.

Voice Synthesis on Ubuntu
==========================

bash file containing:
pico2wave -l=en-GB -w lookdave.wav "$1"
./lookdave.sh "$(cat lookdave.txt)"

Building an Android App
=======================

This guide is useful

http://ionicframework.com/docs/guide/publishing.html


Make sure it is all up to date

$ sudo npm update -g cordova
$ cordova platform update android
$ cordova platform update ios


Build it only to release grade

$ cordova build --release android

You need a key

$ keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000

you need to sign the apk file

$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore /Users/rogerhyam/Dropbox/RBGE/apps/deploy/android/birds-of-peramagroon.keystore MainActivity-release-unsigned.apk alias_name

zipalign it for efficiency and also to rename it

/Users/rogerhyam/android-sdks/build-tools/21.1.2/zipalign -v 4 MainActivity-release-unsigned.apk BirdsOfPeramagroon1.0.apk





