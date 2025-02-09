# Android Locators

## By Accessibility ID $('~')

* Cross-platform(iOS and Android)
* preferred option
* Always try to create accessibility Id-s
* it does not change with localization
* `$('~App')` - accessibility id selector
* Resource id
  * sould also be unique

## By Class Name / By Tag Name

* Class is usually not unique
  * TextView, Button, Layout

## By xpath

* Goto selector after accessibility ID
* Dynamic and flexible
* Long and difficult to read

## Find element by Android UiAutomator

* used for finding elements
* additional search capabilities
* framework tha provides a number of ways to find elements
* [Link](https://developer.android.com/reference/androidx/test/uiautomator/UiSelector)

```js
 await $('android=new UiSelector().textContains("Alert")').click();
```

## Find multiple elements

* Use `$$` to access multiple elements
* Use loop to loop through elements

```js
  for(const element of textList){
    actualList.push(await element.getText());
    }
```