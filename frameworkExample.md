# Selenium Framework Amplitudo

- [Selenium Framework Amplitudo](#selenium-framework-amplitudo)
- [Utils package](#utils-package)
  - [FrameworkSetup.java](#frameworksetupjava)
  - [SharedMethods.java](#sharedmethodsjava)
  - [ExtendedBy.java](#extendedbyjava)
  - [CommonFlows.java](#commonflowsjava)
  - [ApiRequestProcessor.java](#apirequestprocessorjava)
- [Enums](#enums)
- [Objects](#objects)
- [Page Elements](#page-elements)
- [Common rules](#common-rules)
- [Page Workflows](#page-workflows)
- [Test Cases](#test-cases)

# Utils package

## FrameworkSetup.java

- Class
- Location *utils/FrameworkSetup.java*
- It is not meant to be changed
- declarations for: baseUrl, timeout, formats, Extended By, browser, JSExecutor, implicitWait
- retrieving properties from settings.properties file

   ```java
      protected Properties settings = Settings.load("settings.properties");
      public String environment = settings.getProperty("environment");
   ```

- driver setup / stopMethod

   ```java
   // Initialize driver
      @BeforeMethod(alwaysRun = true)
      public void startDriver() throws Exception {
        if(settings.getProperty("run").equalsIgnoreCase("local")) {
            startLocalDriver();
        } else if(settings.getProperty("run").equalsIgnoreCase("remote")) {
            startRemoteDriver();
        }
    }

    // Stopping driver
    @AfterMethod(alwaysRun = true)
    public void stopDriver() {
        driver().quit();
    }

    // startLocalDriver()

    private void startLocalDriver(){
        WebDriver driver = driver();
        String os = System.getProperty("os.name").toLowerCase();
        if (browser.equalsIgnoreCase("Chrome")) {
            if (os.contains("win")) {
                System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe");
            } else if (os.contains("mac")) {
                System.setProperty("webdriver.chrome.driver", "drivers/chromedriver");
            }

            DesiredCapabilities caps = new DesiredCapabilities();
            caps.setCapability("resolution", "1280x768");

            Map<String, Object> chromePrefs = new HashMap<>();
            chromePrefs.put("profile.default_content_settings.popups", 0);
            chromePrefs.put("download.default_directory", fileDownloadDirectory + fileSeparator);
            ChromeOptions chromeOptions = new ChromeOptions();
            chromeOptions.setExperimentalOption("prefs", chromePrefs);
            chromeOptions.addArguments("--incognito");
            driver = new ChromeDriver(chromeOptions); //(chromeOptions);
        } else if (browser.equalsIgnoreCase("Firefox")) {
            if (os.contains("win")) {
                System.setProperty("webdriver.gecko.driver", "drivers/geckodriver.exe");
            } else if (os.contains("mac")) {
                System.setProperty("webdriver.gecko.driver", "drivers/geckodriver");
            }
            //driver = new FirefoxDriver();
        } else if (browser.equalsIgnoreCase("Safari")) {
            //driver = new SafariDriver();
        }
        driver.manage().window().setSize(new Dimension(1280, 800));
        driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
        DriverThreadLocal.setDriver(driver);
    }
    

   ```

- Test ENV Setup Information - declare variables to get information - example bellow:

   ```java
      public String testApiBaseUrl = getValues().get("ApiBaseUrl");

      /** this method pulls the variable values based on which environment has been set in settings.properties file
      *
      * @return the environment specific variables
      */
      public Map<String, String> getValues(){
          if(values != null){
              return values;
          }
          values = new HashMap<>();
          if("PROD".equalsIgnoreCase(environment)){
               timeout = 45;
                values.put("ApiBaseUrl", "https://"); //change to prodBaseUrl
          }
          if("STAGING".equalsIgnoreCase(environment)){
              values.put("ApiBaseUrl", "https://");
          }
          return values;
      }

   ```

## SharedMethods.java

- extends FrameworkSetup
- contains most common functions
- is extended in:
- contains ``` click, check, uncheck, clickAndWaitForElement, dragAndDrop, focusActiveElement, focusActiveWindow, focusIframeModal, focusPageContent, getAttributes, getText, hover, hoverAndClick, hoverOver, input, inputSuperClear, inputUrl, pressEnter, pressTab, select, uncheck, waitForAppToLoad, isAlertPresent, isCheckboxChecked, getRandomNumber, getRandomString, getRGB2hex, getSelectedValue, getOptions, element getters, acceptBrowserAlert, closeBrowser, closeBrowserTab, closeBrowserAlert, maximizeWindow, openUrlInNewWindow, readJSON, refreshPage, scroll functions, setBrowserSize, emulateMobileDevice, sleep, switchToTab ```

## ExtendedBy.java

- class with all locators methods
- contains ``` id, className, cssSelector, name, linkText, xpath, href, value, text, title, type, src ```
- initialized in FrameworkSetup as 

    ```java
    public ExtendedBy By = new ExtendedBy();
    ```

## CommonFlows.java

- extends SharedMethods and navigation class if there is any
- all flows in this class should:
  - be in alphabetical order
  - be prefaced with word **go** so each flow reads like a command, e.g. **goDoSomething**
  - call the original workflow
  - when necessary be overloaded for ease of use
- protected void type

```java
    protected void goSearchAndCreateCustomer(Customer customer) {
        new CustomersFlow().searchAndCreateCustomer(customer);
    }
```

## ApiRequestProcessor.java

- for API calls

# Enums

Enums are used to define collections of contants. Enums are special kind of Java classes. Enum can contain constants, methods, etc. 

- all uppercase when defining

```java
public enum TrackSupplier {

    DISALLOW("0"),
    ALLOW("1"),
    REQUIRE("2");

    String id;

    TrackSupplier(String id) {
        this.id = id;
    }

    public String getId() {
        return this.id;
    }
}

// in class where we use it -> 
TrackSupplier.DISALLOW for example
```

# Objects

- instances of classes

```java
public class Inventory {
    private Customer customer = new Customer();
    private Item item = new Item();
    // declare all valiables here also

    public Inventory(){

    }
    // public methods for this object
}
```

# Page Elements

- divided into logical packages
- extends CommonFlows
- always start with **the** keyword
- Naming convention:
  - theContainerNameObjectLabelElement
    - ObjectLabel is the name displayed in the UI
    - Element is type of object - button, icon, dropdown, text field...
    - e.g. the---Filed, the---Dropdown, the---Label, the---Title
- class names are **PageUI**

# Common rules

* comments and dividers

   ```java

    //-------------------- Example Elements - ExtendedBy --------------------//

    //--- Record Tabs ---//
   ```

# Page Workflows

- Workflow classess extend the respective pageElementUI class because they are specific to a single page
- Workflows that cross multiple pages need to be placed in CommonFlows
- Workflows should:
  - be organized in alphabetical order
  - be as small as possible in order to remain modular and reusable
  - remain clean, free of error checks and asserts
  - be confined to the page it is specific to
- Naming convention
  - named after specific function
  - --add
    - --complete
    - --configure
    - --disable
    - --enable
    - --update
    - --validate
- When breaking down workflows into reusable pieces, create **private methods**
  - private methods are placed at the bottom of the class, organized in alphabetical order
  - private methods should be separated visually
  - are only used by public methods
  - limited to being used only within this Flow class

    ```java
       //==================== PRIVATE METHODS ====================//
    ```

Examples:

```java
     /**
     * This example demonstrates:
     * -- how to populate a "select" method
     * -- how to check a checkbox
     */

    public void chooseActiveEvent() {
        //navPlanEvents();
        select("Meeting ID", theSearchTypeDropdown()); //read as: "Select Meeting ID from the Search Type dropdown."
        check(theActiveCheckbox());
    }

     /**
     * CommonFlows
     * - these will only be called by your test classes, but you'll want to know how to create them
     *
     * This example demonstrates:
     * -- how to write a CommonFlow that uses an object
     */

    public void goAddPeopleUserInvoice(Person person) {
        //goAddPrimaryPaymentProcessor();
        //goAddRegPackage(regPackage);
        //goAddPeopleUser(person);
        //new PeopleRecordTransactionsFlow().addInvoice(regPackage);
    }

     /**
     * This example demonstrates:
     * -- how to write a private method
     * -- create a basic workflow using select, inputs, and checks
     */
    private void randomPrivateMethod() {
        select("Meeting ID", theSearchTypeDropdown());
        //input("test@example.com", new CreateRfpEventDetailsUi().theContactEmailField());
        check(theBackButton());
    }
```

# Test Cases

- should appear in the exact same order as the workflows of the respective Flow classes
- 1:1 test methods:public workflows
- Test cases use GIVEN WHEN THEN statements
- Test cases use Asserts
  - Assert that something is on the page
    - ``` Use Assert.assertTrue(isElementPresent(UiClass.ByElement), "String message"); ```
  - Assert that something is NOT on the page
    - ```Assert.assertFalse(isElementPresent(By element), "String message")```
  - Assert that expected value is correctly displayed
    - ```Assert.assertEquals((PageClass.verifyMethod), "String value");```
- Groups and description 
  - **@groups** are used to group test cases
  - **@descrition** is usually Jira ticket link
