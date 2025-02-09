# TestNG
- **Test Suite** - collection of TestNG tests
- TestNG does not let us define the test suites inside the test code or the main testing source code. We need to create
  TestNG XML file to execute
- testng.xml file handles multiple test classes, target test run, set test dependency, include or exclude any test,
  class, package, set priority etc.
- testng.xml tags
```xml
    <suite> - The suite tag can be given any name and denotes the test suite name.
    <test> - The test tag can be given any name and indicates your test sets.
    <classes> - This is the combination of your package name and test case name and cannot write anything else.
```

### **TestNG Annotations** in Hierarchy:

- @BeforeSuite
- @BeforeTest
- @BeforeClass
- @BeforeMethod
- @Test
- @AfterMethod
- @AfterClass
- @AfterTest
- @AfterSuite

### **Priorities** in TestNG

- Tests are executed in alphabetical order by default
- The priorities are an additional option that we can put to use with the test annotations. This priority check happens
  AFTER the annotation check
- The larger the priority number, the lower is its priority. So a method with priority 1 will run after the test with
  priority 0.
- The test cases without the priority attribute are given the "priority" and executed before the methods with priority.
- One method, one priority
- if two or more methods have the same priorities in TestNG, then their running test sequence is alphabetic
- With a method with no priority, the priority is set to 0 by default.
- Skipping test without priority - ```@Test (enabled = false)```

### TestNG Groups

Combine the tests into groups and let the tester choose which ones to run and which ones to ignore. We can combine
different groups in TestNG, use a REGEX...

- Running the group in a single command. It does not matter if tests are in different classes.
- Groups are declared in testng.xml file inside ```<test>``` or ```<suite>``` tags.
- Groups declared inside ```<test>``` tag apply only to that particular test tag, and groups declared
  inside ```<suite``` tag apply to all ```<test>``` tags in the XML file
- Nested groups
```xml
     <groups>
          <define name = "SuperGroup">
             <include name = "demo"/>
          </define>
          <run>
               <include name = "SuperGroup"/>
          </run>
     </groups>
```
- Including and excluding groups with ```<include name="">``` and ```<exclude name="">``` tags
- Using REGEX in ```<include><exclude>``` tags
    - STRING.* - searches the string which is starting with string keyword and has anything after that

### **Dependent Tests** TestNG

- To denote that testB is dependent on testA - if we want tests to run in particular order
- Dependent tests in TestNG determine the dependency of a test on a single or group of tests
- Two ways of declaring dependency:
    - ```@Test(dependsOnMethods={METHOD_NAMES})``` - depends on another method / test
    - ```@Test(dependsOnGroups={GROUP_NAMES})```   - depends on group
        - in xml
          ```xml
             <groups>
                 <group depends-on= "openbrowser" name= "login"/>
             </groups>
          ```

### Reporting

- To enable test_output creation in IntelliJ - [Screenshot 1](https://prnt.sc/c8TFUc4iDFad)
  , [Screenshot 2](https://prnt.sc/WhEZo9oCcQbx)
- We can use Reporter.log() for logging in information like ```java Reporter.log("text");```

### Parameters

- TestNG Parameters are run through the TestNG XML file and not from the test case files directly.
- in xml
   ```xml
         <parameter name="val1" value="2" />
   ```
- in Tests ```@Parameters ({"val1", "val2"})```
- Parameters can be declared on test and on suite level but TestNG gives preference to the Parameters defined at the
  test level over the parameters set at the suite level.
- Optional parameters - So, if no parameter value is specified, the optional parameter value is taken.

### Data Providers

- Data Providers pass different values to the TestNG Test Case in a single execution and in the form of TestNG
  Annotations.
    - ```java
          @DataProvider (name = "name_of_dataprovider")
           public Object[][] dpMethod() {
                return new Object [][] { values}
           }
           @Test (dataProvider = "data-provider")
           public void myTest (String val) {
               System.out.println("Passed Parameter Is : " + val);
           }
      ```
- Data Provider returns 2D list of objects
- The method then performs a data-driven test foe each value that was specified
- Unlike parameters in TestNG, the data providers can be run directly through the test case file.
- **Asserts**
    - Assertions in TestNG are a way to verify that the expected result and the actual result matched or not.
    - General approach ```Assert.Method(actual, expected, message)```
    - message - A string message to display only in case of an error when assert fails.
    - **Hard Asserts**
        - Hard Asserts are those asserts that stop the test execution when an assert statement fails, and the subsequent
          assert statements are therefore not validated.
    - **Soft Asserts**
        - the subsequent assertions keep on running even though one assert validation fails, i.e., the test execution
          does not stop.
        - Soft assert does not include by default in TestNG. For this, you need to include the package
          org.testng.asserts.Softassert.
        - We use soft asserts when we do not care about the failure of specific validations and want the test execution
          to proceed and also want to see the exception errors.
        - Soft asserts are also known as "Verify"
        - Soft assert requires the external import of the package import org.testng.asserts.SoftAssert;
        - An object of the SoftAssert runs the assert statements.
        - object.assertAll() statement is required to see the exceptions; otherwise, the tester won't know what passed
          and what failed.
    - **Most common TestNG Assertions**
        - ```Assert.assertEqual(String actual, String expected, String message)```
        - ```Assert.assertEquals(boolean actual, boolean expected, message)```
        - ```Assert.assertTrue(condition, message)```
        - ```Assert.notEquals(conditon, message)```
        - ```Assert.fail(message)```

### Parallel Test Execution

- Methods - run the parallel tests on all @Test methods in TestNG
- Tests - run all the test cases present inside the ```<test>``` tag
- Classes - run all the test cases present inside the classes that exist in the XML
- Instances - run all the tests cases parallel inside the same instance
- ``` <test name = "Parallel Tests" parallel = "methods">```
- **Threads** - number of instances of browser that run during test execution
    - The TestNG has a default value of thread = 5 for parallel testing
    - if there are three methods and two threads, one will have to wait until one thread is free and takes up that
      method for execution
    - ```thread-count = "2"```
    - in TestNG, we also get the liberty to run a single test method parallel by configuring it inside the test code
      itself.
        - ``` @Test(threadPoolSize = 4, invocationCount = 4, timeOut = 1000)```
            - threadPoolSize: The number of threads we would like to create and run the test parallel.
            - invocationCount: The number of times we would like to invoke this method.
            - timeOut: The maximum time a test execution should take. If exceeded, the test fails automatically.

### Listeners

- TestNG listeners are the piece of code that listens to the events occurring in the TestNG
- TestNG Listeners are applied as interfaces in the code because "Listeners" is a "class" in TestNG.
- **ITestListener**
    - most used listener in TestNG and Selenium
    - implements and overrides methods
    - onStart, onFinish, onTestStart, onTestSuccess, onTestFailure, onTestSkipped,
      onTestFailedButWithinSuccessPercentage
    - ```<listeners> <listener class-name = "ListenersTestNG"></listener></listeners>```
- **IReporterListener**
    - The IReporter interface in the TestNG Listener provides us with a medium to generate custom reports (i.e.,
      customize the reports generated by TestNG). The interface contains a method called generateReport() which we
      invoke when all the suites have run. This method takes three arguments:
        - xmlSuite: This is the list of suites that exist in the XML file for execution.
        - suites: This is an object which contains all the information about the test execution and suite related
          information. This information may include the package names, class names, test method names, and the test
          execution results.
        - outputDirectory: It contains the path to the output folder where the generated reports will be available.

### Retrying failed tests

Failures can happen for different reasons:

- Random browser issues or browser becoming unresponsive
- Random machine issues
- Server issues like unexpected delay in the response from server

**IRetryAnalyzer** interface
- returns ```true``` if method has to be retried
- more information on [Link](https://toolsqa.com/testng/retry-failed-tests-testng/)

### Configuring TestNG

* [Link](https://testng.org/doc/index.html)
* [Installation process](https://www.toolsqa.com/testng/install-testng/)
* @Test annotation followed by methods is required in order to run TestNG tests without main class
* If test case takes a long time to execute and fails other tests
   ```xml
      @Test(timeout= 4000)
   ```   



