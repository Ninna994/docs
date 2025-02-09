# Native Features

## Package & Activity

* appPackage - full name of application
  * technical name
  * top level package under all code is situated
  * package attribute in appium inspector
    * when accessed homescreen of aplication is opened
* appActivity - functionality or screen
  * MainActivity, AlertDialogSamples...
  * all activities build app package
  * Access app activity
    * Actions > Device > Android Activity > Current Activity
* help access screen directly
* saves time by not jumping to screens
* helps with stabilization of tests

```js
 await driver.startActivity("io.appium.android.apis", "io.appium.android.apis.app.AlertDialogSamples");
```

## Dialog and Alerts - Android

* Actions
  * Accept alert `.acceptAlert()`
  * Dismiss alert `dismissAlert()`
  * OK / Cancel
  * `getAlertText()`

## Vertical Scrolling - Android

* When we are working with elements that aren't displayed within the viewport
* Find scrollable element
  * Scroll to end
  * Scroll to top
  * Scroll Text into view
* [UIScrollable](https://developer.android.com/reference/androidx/test/uiautomator/UiScrollable)

```js
    await $('android=new UiScrollable(new UiSelector().scrollable(true)).scrollTextIntoView("Secure Surfaces")').click();
```

## Horizontal Scrolling - Android

* Same as vertical but set to horizontal list
* Gallery example

```js
    await $(
      "android=new UiScrollable(new UiSelector().scrollable(true)).setAsHorizontalList().scrollForward()"
    );

    await $(
      "android=new UiScrollable(new UiSelector().scrollable(true)).setAsHorizontalList().scrollBackward()"
    );
```

## Handle Permissions

* Permissions are handled in capabilities ` "appium:autoGrantPermissions": true,`

## setValue and addValue

* set value first clears value and then inserts it
* add value just adds value

