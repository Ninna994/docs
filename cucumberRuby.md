# Cucumber and Ruby

## Table of Contents

- [Cucumber and Ruby](#cucumber-and-ruby)
  - [Table of Contents](#table-of-contents)
  - [Cucumber folder structure](#cucumber-folder-structure)
  - [.feature file structure](#feature-file-structure)
  - [Cucumber keywords](#cucumber-keywords)
  - [Cucumber functionalities](#cucumber-functionalities)
  - [Ruby and Appium methods](#ruby-and-appium-methods)
  - [Functionalities in Ruby](#functionalities-in-ruby)
  - [Appium commands](#appium-commands)
  - [Debugging](#debugging)
  - [Terminal commands](#terminal-commands)
  - [UI Automator Viewer](#ui-automator-viewer)

## Cucumber folder structure

```ruby
  folder_name
    features - required folder
      area.feature
      area2.feature
      step_definition - required folder
        area_step.rb
        area2_step.rb
      support
        env.rb - file in which we set parameters for testing
        hooks.rb - file in which we create hooks
```

## .feature file structure

```ruby
  Feature: Description
    Background: Steps to be executed in every Scenario in this feature file 
  Scenario: Description
  # Steps with keywords --> Steps are reusable accross feature files
  Given step
  When step
  And step
  Then step
  But step
```

## Cucumber keywords

Cucumber keywords are **Given**, **When**, **Then**, **And**, **But**. They are userd to make logical sense between steps. We can use any prefix we wan and the step will work because cucumber does **not** add prefix as part of step.

## Cucumber functionalities

1. Set parameter in feature file

   ```ruby
    Given Description "parameter"
   ```

1. Make Scenario Outline when you need to execute multiple steps with many values

   ```ruby
    Scenario Outline:
      #Steps
    Given
    When I type "<value1_name>"
    Then I should see "<value2_name>"
    And See also "<value3_name>"
    Examples:
    |value1_name|value2_name|value3_name|
    |val1       |val2       |val3       |
    |val1       |val2       |val3       |

   ```

1. **@Tags** Are used for grouping tests in Cucumber

   ```ruby
    @name
    Scenario or Step or Feature
   ```

1. **Hooks** are used  to execute anything we need to do before or after Test Scenario. Two hooks cucumber has are **Before** and **After**

   ```ruby
    Before do
      # anything that needs to be done before Test Scenario
      # launch Appium for example
    end
    After do |scenario|
      # anything that needs to be done after Test Scenario
      # kill Appium for example
      # Send screenshots of device if test fails for example
    end
    After Configuration do
    #what to do after every scenario
    end
   ```

1. **Profiles** are placed in same level as features folder. Profiles file is : _cucumber.yml_. 

   ```yml
    <!-- Creates profile name and mames report in report.html file and reports to console  -->
     name: -t @tag --format html --out report.html --format pretty
   ```



## Ruby and Appium methods

1. _puts_ - command that prints message

   ```ruby
    puts("message")
   ```

1. _|arg|_ - local variable that lives between do and end

   ```ruby
    |var|
    puts(var)
   ```

1. *find_element(id: "id")* - find element by resource id
1. *find_element(accessibility_id: "content desc")* - used when we target element with content description
1. *find_elements(id: "id")* - find multiple elements by resource id
1. *find_elements(accessibility_id: "content desc")* - find multiple elements by resource id
1. *find_elements(criteria)[index]* - finds element that is on INDEX index inside array
1. *find_element(id: "id").find_element(xpath: "//class[@text='']")* - find element inside container by resourcing its class and then text inside that specific element
1. *text("text")* - used when we need to find element by text
1. *.click* - for click event in Appium
1. *.send_keys(value)* - when we want to write inside element
1. *.text* - gets text from element
1. *fail("Message")* - method that executes when test failed. Inside brackets goes optional message
1. *.split("criteia")* - split any array by any criteria
1. *.each*  - iterate through array of data
1. *.enabled?* - returns boolean true if state is enabled and false if its state is disabled
1. *.failed?* - return boolean true if test failed and false if test passed
1. *.tap* - click on screen
1. *.swipe* - scroll on screen
1. *.times{}* - repeat some code number of times
1. *.exists{what}* - used to check if there is that element on page
1. *.get_source* - return all values of that page in XML
1. *Time.now(strftime("%d-%m-%Y_%H.%M.%S"))* - Time function formatting
1. *File* - Class for File manipulation
1. *.to_i* - transforms string to integer(for indexes --> .to_i-1)
1. *biniding pry* - calls pry and pauses test execution and gives control to us

## Functionalities in Ruby

1. Taking parameter as part of step

   ```ruby
    Then('condition {string} or "([^"]*)"') do |arg|
      puts("message" + arg)
    end
   ```

1. Taking parameter as part of step ex 1st, 2nd, 3rd

   ```ruby
    Then('condition (\d+)(?:st|rd|th)?') do |arg|
      puts("message" + arg)
    end
   ```

1. Set key values that can be accepted

   ```ruby
    Given(Description (option1|option2|option3)) do |state|
    end
   ```

1. **if elsif** statement

   ```ruby
      if state == "option1"
        do this
      elsif state == "option2"
        do this
      end
   ```

1. **fail** function in _multiple lines_

   ```ruby
    if Condition != expected
      fail("Message")
    end
   ```

1. **fail** function _one line_

   ```ruby
    fail("Message if failed") if Condition != expected
   ```

1. Pass variable inside string with **#{var}**

   ```ruby
    Then('condition {string} or "([^"]*)"') do |arg|
      puts("message #{string}")
    end
   ```

1. **Arrays []** are data type in ruby that has indexes. Indexing starts at 0.

1. **each** loop for going through array of data

   ```ruby
    array.each do |var|
    end
   ```

1. For repeating Ruby code for number X of times we use **.times**

   ```ruby
    X.times{code}
   ```

1. Loop through data **until** some condition isn't met

   ```ruby
    until condition do
      # what needs to be done every time
    end
   ```

1. Functions are made so one piece of code could be executed multiple times. We make functions inside **env.rb** file.

   ```ruby
    def functionName(parameters)
      # what needs to be executed multiple times
    end
   ```

## Appium commands

1.When we need to click on element by its coordinates x and y Z of times we use **TouchAction**, **.tap** and **.perform** event

   ```ruby
    Appium::TouchAction.new.tap(x:X.xx, y:Y.yy, count: Z).perform
   ```

1. When we need to scroll on page with Appium we use **TouchAction**, **.swipe** and **.perform** for some **duration** of time

   ```ruby
    Appium::TouchAction.new.swipe(start_x:X.xx, start_y:Y.yy, end_x:X.xx, end_y:Y.yy, duration:X ms).perform
   ```

## Debugging

Pry is tool that can be called if we want to pause our test execution and take over control over test at any time we want.

## Terminal commands

1. _cucumber_ - executes every test scenario in every .feature file
1. _cucumber -t @name_ - executes scenario or feature file with @name tag
1. _cucumber --dry-run_ - executes scenarios without Ruby code, checks for step definitions
1. _cucumber -t @tag1, @tag2_ - executes every scenario that either has @tag1 or @tag2
1. _cucumber -t @tag1 -t @tag2_ - executes every scenario that has both @tag1 and @tag2
1. _cucucmber -p profile-name_ -executes test scenario with this profile name
1. _adb device_ - which device is connected to computer
1. _uiautomatorviewer_ - starts automator viewer
1. _irb_ - starts ruby console

## UI Automator Viewer

1. Takes screenshot of device. On the right side are elements and their properties. If we don't have any **resource_id** we can target element by **content description**. Or in edge cases by **text**.