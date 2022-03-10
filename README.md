# react-native-unity-demo

This is a demo project for [react-native-unity](https://github.com/f111fei/react-native-unity-view)

## Unity Version

Use the master branch (Unity >= 2018.2)

Use [unity-2017](https://github.com/f111fei/react-native-unity-demo/tree/unity-2018.1) branch (Unity = 2018.1)
Use [unity-2017](https://github.com/f111fei/react-native-unity-demo/tree/unity-2017) branch (Unity < 2018)

## How to Build

1. Open `unity/Cube/Assets/test.unity`

2. Click `Build` => `Export Android` or `Export IOS`

3. Set name "UnityExport" for exported folder, move this folder to path `android/UnityExport`

```
cd react-native-unity-demo

npm install

npm run watch

npm run android or npm run ios
```

## Preview

![gif](https://user-images.githubusercontent.com/7069719/37143096-12be6810-22f5-11e8-89d8-562e9213072e.gif)


## Known issue and solution

1. Build failed, missing Unity class.

Copy `./android/UnityExport/libs/unity-classes.jar` to `../node_modules/react-native-unity-view/android/libs/unity-classes.jar`.

After that, add `implementation fileTree(dir: 'libs', include: ['*.jar'])` to `dependencies` section of `build.gradle` in the same folder.

`Note that, it's just a hot-fix to be able to run the project.`

2. Const declarations are not supported

Problem come from one of it's package dependencies. Bundle React native source files to get rid of this error.

`mkdir ./android/app/src/main/assets/react/release`

`npx react-native bundle --dev false --platform android --entry-file index.js --bundle-output ./android/app/src/main/assets/react/release/index.android.bundle --assets-dest ./android/app/src/main/res`

Note that, the cmd is work in RN 0.57.0. For later versions of RN, generate bundle file to `assets/index.android.bundle` instead.

3. String resource 0x0 error when you click to Toogle Unity button.

Add line below to to strings.xml file in android project. 

```
<string name="game_view_content_description">Game view</string>
<string name="unity_root">unity_root</string>
```

### For production

There is a newer lib which already fix some of these issues and a lot more. You can find the lib at this repo:

https://github.com/old-rookies/react-native-unity-play

