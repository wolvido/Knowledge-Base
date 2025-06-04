
|Command|Description|
|---|---|
|`npx expo start`|Starts the development server (whether you are using a development build or Expo Go).|
|`npx expo prebuild`|Generates native Android and iOS directories using [Prebuild](https://docs.expo.dev/workflow/prebuild/).|
|`npx expo run:android`|Compiles native Android app locally.|
|`npx expo run:ios`|Compiles native iOS app locally.|
|`npx expo install package-name`|Used to install a new library or validate and update specific libraries in your project by adding `--fix` option to this command.|
|`npx expo lint`|[Setup and configures](https://docs.expo.dev/guides/using-eslint/) ESLint. If ESLint is already configured, this command will [lint your project files](https://docs.expo.dev/guides/using-eslint/#usage).|

## Expo Doctor(https://docs.expo.dev/develop/tools/#expo-doctor)
Expo Doctor is a command line tool used to diagnose issues in your Expo project. To use it, run the following command in your project's root directory:
```bash
npx expo-doctor
```


For deleting unused and updating node modules, use: `expo update`.