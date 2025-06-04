[[cFSD-R Architecture]]
#### Emulation
```bash
//navigate
cd C:\Users\User\AppData\Local\Android\Sdk\cmdline-tools\bin

//get the name
avdmanager list avd

//navigate
cd C:\Users\User\AppData\Local\Android\Sdk\emulator

//load
emulator -avd <name of device>
emulator -avd Medium_Tablet_API_35
emulator -avd Medium_Tablet_API_35 -no-snapshot-load
```
Start project:
```bash
npx expo start
```
#### Development Tools
- run watch task `Ctrl+Shift+B` to track import errors on whole codebase