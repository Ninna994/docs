# Jenkins

## Installation

* Download Jenkins .war [Link](https://www.jenkins.io/download/)
* cmd-command ```bash java -jar jenkins.war --httpPort=8085```
* save generated password
* access Jenkins using localhost:8085 and providing temp password
* Manage Jenkins > Global Tool Configuration > setup JAVA_HOME and MAVEN_HOME - uncheck install automatically
* Paste project in .jenkins file under Users folder
* Directory - ${JENKINS_HOME}/Maven
* Build > Invoke top-level Maven targets
   * Goals -> commands -> test -PRegression

## Schedule

```bash MINUTE (0-59), HOUR (0-23), DAY (1-31), MONTH (1-12), DAY OF THE WEEK (0-6) ```

# Extent Reports

* [Link for maven repository](https://mvnrepository.com/artifact/com.aventstack/extentreports)
   ```java
   // How to make Extent tests code>>>>>
 
   public class test {
    ExtentReports extent;
    @BeforeTest
    public void config() {
   // ExtentReports , ExtentSparkReporter
        String path = System.getProperty("user.dir") + "\\reports\\index.html";
        ExtentSparkReporter reporter = new ExtentSparkReporter(path);
        reporter.config().setReportName("Web Automation Results");
        reporter.config().setDocumentTitle("Test Results");
        extent = new ExtentReports();
        extent.attachReporter(reporter);
        extent.setSystemInfo("Tester", "Rahul Shetty");
    }
    @Test

    public void initialDemo() {
        ExtentTest test = extent.createTest("Initial Demo");
        System.setProperty("webdriver.chrome.driver", "C:\\Program Files\\Drivers\\chromedriver.exe");
        WebDriver driver = new ChromeDriver();
        driver.get("https://rahulshettyacademy.com");
        System.out.println(driver.getTitle());
        driver.close();
//test.fail("Result do not match");
        extent.flush();
    }

}
   ```
