# Swift-Player - Better expo-av HLS player for Android
By using a `CustomBandwidthMeter` and `CustomAdaptiveTrackSelection`. Playing an HLS video will start with a fine quality video first then adapt to the network bandwidth.

## How to do it

- Run `yarn` to install the dependencies especially `expo-av`.
- Run `expo eject` to build the project as a standalone app.
- Replace files in `node_modules/expo-av/android/src/main/java/expo/modules/av/player` with the java code in `fixs` directory using command
```shell
cp fixs/* node_modules/expo-av/android/src/main/java/expo/modules/av/player
```
- Build the app, as usual, using `react-native run-android` and `react-native start`.
- Edit the constants in the file
  `CustomBandwidthMeter.java` change `DEFAULT_INITIAL_BITRATE_ESTIMATE` to select the starting bitrate and in file `CustomAdaptiveTrackSelection.java` change `DEFAULT_MIN_DURATION_FOR_QUALITY_INCREASE_MS` to choose how long to wait before upgrade the video quality.
- Rebuild every time after edit the files using command `react-native run-android`

## Maintaining the source code
- Clone ExoPlayer source code from https://github.com/google/ExoPlayer
- Check the `expo-av` android ExoPlayer dependency version at `node_modules/expo-av/android/android/build.gradle` you will the version like this.
```
api 'com.google.android.exoplayer:exoplayer:2.9.2'
```
- Check out the ExoPlayer code at those version by search a commit by version number (e.g. `2.9.2`).
- Find the files name `DefaultAdaptiveTrackSelection.java` and `DefaultBandwidthMeter.java` from ExoPlayer code
then merge it to `CustomAdaptiveTrackSelection.java` and `CustomBandwidthMeter.java` in `fixs` respectively.
- Update `SimpleExoPlayerData.java` only when major api change.
