# Installing Selenium

1. Install Java and validate that Java is installed by going to "C://ProgramFiles/Java"
   * Java 8+
   * setup Environment variables - JAVA_HOME (path to JRE)
   * 
1. Install IDE of choice (IJ or Eclipse)
1. Setup Maven project
1. Install dependencies [Maven repository](https://mvnrepository.com)
   * [Selenium](https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java/4.1.2)
   * [TestNG](https://mvnrepository.com/artifact/org.testng/testng)
1. 

# Classes and objects used in Selenium

1. driver - as mentioned on driver setting
1. dropdown
   ```java
      WebElement name = driver.findElement(By.id("ID"));
      Select dropdown =  new Select(name);
   ```

# Properties file
* src/data.properties

   ```java
        // data.properties
      browser=chrome
     url="rahulshettyacademy.com"
        // class
      public static void main(String[] args) throws IOException {
        Properties prop = new Properties();
        FileInputStream fis = new FileInputStream("C:\\Users\\inani\\OneDrive\\Desktop\\Selenium\\src\\data.properties");
        prop.load(fis);
        System.out.println(prop.getProperty("browser"));

      //set property locally
      prop.setProperty("browser", "firefox");
      
      // set property back into file
      prop.setProperty("browser", "firefox");

       FileOutputStream  fos = new FileOutputStream("C:\\Users\\inani\\OneDrive\\Desktop\\Selenium\\src\\data.properties");
       prop.store(fos, null);
    }
   ```


# Drivers

1. Chrome driver
   * Download chromedriver for current version of Chrome
   * [Link for download](https://chromedriver.chromium.org/downloads)

   ```java
    System.setProperty("webdriver.chrome.driver", "C:\\Program Files\\Drivers\\chromedriver.exe");
    WebDriver driver = new ChromeDriver();
   ```
1. Firefox driver
   * Download geckodriver for current version of Firefox
   * [Link for download](https://github.com/mozilla/geckodriver/releases)

   ```java
        System.setProperty("webdriver.gecko.driver", "C:\\Program Files\\Drivers\\geckodriver.exe");
        WebDriver driver = new FirefoxDriver();
   ```
1. Edge driver 
   * Download msedgedriver for current version of Edge
   * [Link for download](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)
   ```java
        System.setProperty("webdriver.edge.driver", "C:\\Program Files\\Drivers\\msedgedriver.exe");
        WebDriver driver = new EdgeDriver();
   ```
1. Chrome driver to invoke DEV tools
   ```java
      ChromeDriver driver = new ChromeDriver();
      DevTools devTools  = driver.getDevTools();
      // create session
      devTools.createSession();
   ```
1. Chrome headless
   ```java
      // chrome headless
            ChromeOptions options = new ChromeOptions();
            options.addArguments("headless");
            //execute in Chrome driver
            System.setProperty("webdriver.chrome.driver", System.getProperty("user.dir") +"\\src\\main    \\java\\resources\\drivers\\chromedriver.exe");
            driver = new ChromeDriver(options);
   ```


# Webdriver methods

1. get() - by default waits for page to load
1. navigate().to("URL") - navigate while in script
   ```java
      driver.navigate().to("https://rahulshettyacademy");
      // browser back and forward
      driver.navigate().back();
      driver.navigate().forward();
   ```
1. getCurrentUrl()
1. close() and quit()
   * Close and quit are doing seeminglz the same thing but there are certain differences. 
   * close() method closes only the originally opened window by selenium
   * quit() method closes ALL opened windows that are created by Selenium
1. sendKeys() - type into filed
1. click()
1. getText()
1. manage() - configurations
   ```java
      // max, min, fullscreen
      driver.manage().window().maximize();
      driver.manage().deleteAllCookies() // or delete cookie with name, delete only one cookie... 
   ```
1. keyDown(Keys.KEY) - Simulate pressing the key
1. .switchTo().defaultContent(); - to switch to default content on page 


# Dropdown methods / Checkboxes

1. selectByIndex()
1. selectByValue() - what is the exact value of option
1. selectByVisibleText() - what we see as users
1. getFirstSelectedOption()
1. isSelected() - returns true or false

* snippet for listing all elements of list and clicking on one particular
   ```java
      List<WebElement> options = driver.findElements(By.cssSelector(".ui-menu-item a"));

        for (WebElement option :options){
            if(option.getText().equalsIgnoreCase("India")){
                option.click();
                break;
            }
        }
   ```

* Static dropdown selection
   ```java
          WebElement staticDropdown = driver.findElement(By.id("exampleFormControlSelect1"));
           Select dropdown = new Select(staticDropdown);
   ```

# Selenium Relative locators

* above()
* below()
* toLeftOf()
* toRightOf()

```java
import static org.openqa.selenium.support.locators.RelativeLocator.*;

  driver.findElement(with(By.tagName("label")).above(nameEditBox));
```


# Selectors

## ID

```java
driver.findElement(By.id("inputUsername"));
```

## Class name

```java
driver.findElement(By.className("inputUsername"));
```

## CSS Selectors

```java
driver.findElement(By.cssSelector(".inputUsername"));
driver.findElement(By.cssSelector("#inputUsername"));
driver.findElement(By.cssSelector("#inputUsername:nth-child(5)"));
//contains text - =*

```

## Link text - works only for <a> tags

```java
driver.findElement(By.linkText("Forgot your password?"));
```

## XPath

* Install SelectorsHub plugin [Download link](https://selectorshub.com/?_gl=1%2Aymop6k%2A_ga%2AMTQ2Nzg3NzYzMi4xNjQ1ODI1NjUw%2A_ga_QWQKMJK5M3%2AMTY0NTgyNTY0OS4xLjAuMTY0NTgyNTY0OS4w%2A_ga_912NBDY7JJ%2AMTY0NTgyNTY0OS4xLjAuMTY0NTgyNTY0OS4w)
* //tagname[@attribute='value'][index]
* div > p -> //div/p
* bytext - //button[text()='Log Out']
* sibling to sibling -> //header/div/button/following-sibling::TAGNAME[INDEX]
* child to parent (reverse)-> //header/div/button/parent::TAGNAME[INDEX].
* second occurance of xpath -> (xpath)[2]
* parent to child -> //xpath SPACE //xpath


```java
driver.findElement(By.cssSelector(".inputUsername"));
```

# Actions / Child Windows / iFrames

## Actions - Class that handles actions in Selenium

```java
  // contextClick() - right click
  Actions a = new Actions(driver);
  a.moveToElement(element).contextClick().build().perform();
  a.moveToElement(element).click().keyDown(Keys.SHIFT).sendKeys("hello").doubleClick().build().perform();
  a.dragAndDrop(element, elementDestination).build().perform();
```

## Child Windows - tabs, new windows

* switching to child windows and back
   ```java
      //        how many windows is opened in Selenium - get all of them and set them in collection Set
          Set<String> windows = driver.getWindowHandles(); //[parentId, childId]
           Iterator<String> it = windows.iterator();
           String parentId = it.next(); // [0] index
           String childId = it.next(); //[1] index, for all additional we can add more variables and type       it.next();
   //        we need to switch to child window
           driver.switchTo().window(childId);
   ```

* invoking child windows

   ```java
      driver.switchTo().newWindow(WindowType.TAB);
      driver.switchTo().newWindow(WindowType.WINDOW);
   ```
 

## iFrames

```java
 driver.switchTo().frame(driver.findElement(By.cssSelector("")));
driver.switchTo().frame(0); //by index
```


# Assertions

## TestNG assertions

1. Assert.assertEquals(actual, expected);
1. .assertFalse, .assertTrue
1. SOFT ASSERTIONS - test continues after failing until finished. 
   ```java
       SoftAssert soft = new SoftAssert();
       soft.assertTrue(responseCode < 400, "The link with text" + link.getText() + " is broken with code " + responseCode);
       // after all code executed, outside all loops
       soft.assertAll();
   ```


# Common errors and solutions

* ALERT switching and methods
   ```java
      driver.switchTo().alert();
      // .accept(), .getText(), .dismiss()  
   ```
* Synchronization in Selenium
   * **Implicit Wait** - *set globally* - wait for X seconds before failing test. If content is loaded before X seconds test continues - it does not wait for X seconds to pass first
      ```java
          driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(2))
      ```
   * **Explicit Wait** - target specific element or scenario and set wait period
       ```java
          WebDriverWait w = new WebDriverWait(driver,Duration.ofSeconds(5));
          w.until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector("span.promo-info")));
      ```
   * **Thread.sleep** - part of Java, no actions during that time - explicit - it will wait for exactly X seconds
   * **Fluent wait** - keeps repeatedly finding of element at _regular intervals_ of time until the object gets found. Webdriver Wait keeps finding element for every millisecond until object gets found. [Link for information](https://www.selenium.dev/selenium/docs/api/java/org/openqa/selenium/support/ui/FluentWait.html)

* Change/Limit SCOPE of driver

```java
WebElement footerDriver = driver.findElement(By.id("gf-BIG"));
// use footerDriver as regular driver
```

* SSL Certificate hack

```java
        ChromeOptions options = new ChromeOptions();
        // FirefoxOptions options = new FirefoxOptions();
        options.setAcceptInsecureCerts(true);
        
        System.setProperty("webdriver.chrome.driver", "C:\\Program Files\\Drivers\\chromedriver.exe");
        WebDriver driver = new ChromeDriver(options);    
```

* Screenshots in Selenium

```java
        File src = ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
        Files.copy(src,new File("C:/Users/Ina/Desktop/screenshots/screenshot.png"));
        
        // partial screenshots of WebElements
 File file =  nameField.getScreenshotAs(OutputType.FILE);

        FileUtils.copyFile(file, new File("C:/Users/inani/OneDrive/Desktop/logo.png"));

// importujemo klase: 
import org.apache.commons.io.FileUtils;
import java.io.File;
import org.openqa.selenium.OutputType;
```



* Scan all links and check if there are any broken ones

```java
        List<WebElement> links = driver.findElements(By.cssSelector("li[class='gf-li'] a"));
        SoftAssert soft = new SoftAssert();
        for (WebElement link : links) {

            String url = link.getAttribute("href");
            HttpURLConnection conn = (HttpURLConnection) new URL(url).openConnection();
            conn.setRequestMethod("HEAD");
            conn.connect();
            int responseCode = conn.getResponseCode();
            soft.assertTrue(responseCode < 400, "The link with text" + link.getText() + " is broken with code " + responseCode);

        }
        soft.assertAll();
```

* Get height and width of element

   ```java
    nameField.getRect().getDimension().getWidth()
   ```

# Selenium Grid TODO

Smart proxy server that makes running tests in parallel on multiple machines

* [Documentation](https://www.selenium.dev/documentation/grid/)
* [Download JAR](https://www.selenium.dev/downloads/) - Selenium Server(Grid)
* To start hub - ```bash java -jar selenium-server-<version>.jar hub```
* Check webdrivers - ```bash java -jar selenium-server-4.1.2.jar node --detect-drivers true ```
   ![image](https://user-images.githubusercontent.com/17597140/156654651-88d01171-93f5-45b3-8cdd-7615513c6550.png)


## CDP - Chrome DevTools Protocol

* [Link](https://chromedevtools.github.io/devtools-protocol/)
* Selenium methods wrap CDP protocols to grant access to Chrome DevTools directly from automated tests
* ```java driver.send(); ```
* ```java driver.

## POM

Explanation behind this method - collect all objects referred to one page and put them in one file. After that make Test cases and take necessary items from those object files. 

1. Page Object Classes - Define objects and make contructor for current Object Class. Then return all those in separate functions
   ```java
    // Object Model  
    WebDriver driver;

    public RediffLoginPage(WebDriver driver) {
        this.driver = driver;
       // if Page Factory is used bellow line is necessary
       PageFactory.initElements(driver, this);
    }
    
    By username = By.id("login1");
    
    public WebElement EmailId(){
        return driver.findElement(username);
    }
   ```
   ```java
      // Class
     //  define drivers as usual
     RediffLoginPage rdLogin = new RediffLoginPage(driver);
    access all methods via rdLogin
   ```
1. Page Factory
   ```java
      @FindBy(id = "login1")
      WebElement username;

      public WebElement homeLink(){
        return  username;
    }
   ```
1. New method for POM - cleaner way. 

## Framework steps from scratch

1. Create Maven project
   * create from archetype - quickstart
   * install dependencies TestNG and Selenium
1. Make packages in main/java
   * pageObjects
   * resources
1. Make main/resources/base class and data.properties file inside resources 
1. In all classes in test folder add **extends base**
1. Add testng.xml and import it into maven pom.xml
1. Add log4j for logging
1. Add listeners for screenshots on fail
   ```java
      public class Listeners implements ITestListener {
      }

   ```
   * [Link for TestNg Wiki](https://github.com/Ninna994/docs/wiki/TestNG)












   


