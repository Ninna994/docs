# Basics

## Appium

* Appium is open-source automation framework
  * Works on Native, Hybrid & Mobile web apps
  * iOS, Android and Windows apps
* Cross-platform compatibility
* vendor provided frameworks
  * iOS - XCUITests
  * Android - UIAutomator
  * Windows - WinAppDriver
* WebdriverAPI based
  * Java, JS, Ruby...
* Here used:
  * JavaScript language
  * TestDriver - Mocca
  * Test Framework - WebdriverIO

## WebdriverIO

* JS E2E automation framework
* Supports mobile apps in iOS & Android
* Used by Google, Netflix, Microsoft...
* Easy to install
* Easy readability
* Front-end friendly
* Open source

## Installation process

1. Install NodeJs
   1. Install Node 16.10.0 version globally
   2. [Link](https://nodejs.org/en/download/)

2. Java JDK setup
   1. Set JAVA_HOME path
   2. Check if Java is installed in cmd - java -version
   3. If not installed go to Link and install it
   4. Go to Environment variables > Edit system environment variables > Environment Variables
   5. In the top section click New
      1. Variable name: JAVA_HOME
      2. Variable value: C:\Program Files\Java\jdk1.8.0_51 (or whichever version you downloaded)
      3. OK
      4. Verify installation after restarting computer

3. Setup and Install Android Studio [Link](https://developer.android.com/studio?gclid=CjwKCAjw9NeXBhAMEiwAbaY4ltcH4fj3ZdyhXJuaZ7waEeoI4EAIXJQZck-_kiK09lFpJxVcqUVprRoCWvAQAvD_BwE&gclsrc=aw.ds)
   1. Follow installation instructions
   2. Open Android Studio
   3. Setup PATHS
      1. add user variable - ANDROID_HOME
         1. path to Sdk folder - should be something like --  C:\Users\UserName\AppData\Local\Android\Sdk
      2. add to PATH two new variables - /platform-tools and tools
         1. %ANDROID_HOME%\platform-tools
         2. If tools is missing -  Quick fix: `Go to the Tools –> SDK manager –> SDK tools.  Deselect Hide obsolete packages option on the right bottom and further install Android SDK Tools(obsolete). A new folder named Tools is now generated in the SDK directory. (C:\Users\..\AppData\Local\Android\Sdk\tools.)`

4. Setup Android Emulator
   1. Go to Android Studio > Virtual Device Manager > Create Virtual Device
   2. Choose Device - for example Pixel 3 - and download R and Q versions
   3. Wait for install and finish - first simulator setup is done
   4. Press play and device should boot up

5. Appium Desktop Inspector Setup
   1. [Link for download]("https://github.com/appium/appium-inspector")
   2. Go to Releases > Latest Release > Download version
   3. Follow install instructions and open Appium Inspector
      1. Set remote port to 4724
      2. run appium on the same port -p 4724
      3. set the path to /

6. Appium Installation
   1. `npm install -g appium@next`
   2. check `appium -v` for version check
   3. install appium-doctor `npm install -g appium-doctor`
   4. check `appium-doctor` to check if everything you need is installed correctly
      1. `appium-doctor --android`
      2. `appium-doctor --ios`
      3. ALL SHOULD BE GREEN => SUCCESSFULL INSTALLATION
   5. install it locally also - `npm install appium@next`

7. Install Appium Drivers
   1. `appium driver install xcuitest`
   2. `appium driver install uiautomator2`
   3. confirm installation: `appium driver list`

8. WebdriverIO setup
   1. Initialize directory `npm init -y` - install dependencies, y - accept all dependenies
   2. Install WebdriverIO CLI - allows us to setup project confirguration using cLI commands
      1. `npm i @wdio/cli`
   3. Setup configuration
      1. `npx wdio config`
      2. Configure and follow instructions
      3. wdio.conf.js file is also created with all configurations

   4. Setup Test Folder
      1. add test/specs folder and file.js inside it
      2. Run the tests
   5. Run app with webdriverIO
      1. npx wdio

9. Setup Emulator for Testing
   1. spin up appim server on port -4724 for testing and -4723 for webdriverIO tests
   2. `appium -p 4723'
   3. ![appium localserver setup](appiumLocalServerSetup.png)

10. FINISHED SETUP

## WebdriverIO Configuration

* *specs* - all the tests are here
* *capabilities* - for specification of configuration
  * for Android setup >>>
    * platform name, device name, app path

```js
   // at the top
      const path = require('path');
   // cwd - current working directory  
   platformName: "Android",
   "appium:deviceName": "Pixel 3",
   "appium:automationName": "UIAutomator2",
   "appium:app": path.join(process.cwd(), "app/android/ApiDemos-debug.apk"),
```

* *log level* - logging information
* *baseUrl* - place to set baseUrl
* *services* - used

## MISC

- Create `jsconfig.json` file for autocompletion

```json
  {
    "compilerOptions": {
        "types": [
            "node",
            "webdriverio/async",
            "@wdio/mocha-framework"
        ],
        "module": "CommonJS"
    }, 
    "exclude": ["node_modules"]
}
```

- Setup Babel to use next-generation JS features
  - `npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/register`
- Setup linter
  - `npm i eslint --save-dev`
  - `npm install eslint-plugin-wdio --save-dev`
  - make file `.eslintrc`

```json
   {
    "plugins":[
        "wdio"
    ],
    "extends": ["plugin:wdio/recommended", "eslint:recommended"],
    "parserOptions": {
        "ecmaVeersion": "latest",
        "sourceType": "module"
    },
    "env": {
        "es6": true,
        "mocha": true,
        "node": true
    }
    
}
```

## Implement HOOKS

* Before Hook
* Before Each Hook
* After Hook
* After Each Hook

```js
   before(async() => {

   });

   beforeEach(async() => {

   });
```


## Framework folder structure

- App
- Test
  - Screens
    - Android
    - iOS
  - Specs
    - Android
    - iOS
  - Data
  - Utils
    - helper functions
- Config
  - All configuration for wdio
  - running `npx wdio config/wdio.android.conf.js`
