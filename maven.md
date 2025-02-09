# Maven

* Software project management, central repository to 
* Artifacts - files, usually a JAR, that gets deployed to a Maven repository
* GroupId - will indentify project uniquely across all projects
* archetype:generate - Generates new project from an archetype

# Installation

* Install maven locally - [Download link](https://maven.apache.org/download.cgi)
   * Copy path to file and add to sys variables as MAVEN_HOME
   * Add path to /bin folder to Path - click and then new
* [Link for maven repository](https://mvnrespository.com)
* [Maven in 5 minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)
* install dependencies in pom.xml
* choose **maven-archetype-quickstart** - for quickstarting projects



# pom.xml

* Dependencies / plugins
   * Maven surefire plugin - executes all test cases - + configuration for testng.xml


      ```xml
              <plugin>
                 <groupId>org.apache.maven.plugins</groupId>
                 <artifactId>maven-surefire-plugin</artifactId>
                 <version>3.0.0-M5</version>
          <configuration>
          <suiteXmlFiles>
            <suiteXmlFile>testng.xml</suiteXmlFile>
          </suiteXmlFiles>
        </configuration>
             </plugin>
      ```
   * Maven surefire commands
      ```bash
         mvn --version
         mvn clean - delete all temporary files - recommended before execution
         mvn compile - check syntax errors
         mvn test - trigger test execution
         mvn -Dtest=TestName test - run a single test
      ```
   * Maven common problems with compiling [Link](https://roufid.com/no-compiler-is-provided-in-this-environment/)
   * Profiling
      * Make <profiles><profile> annotation with id - NAme of them and paste build tag inside to make multiple profiles
         ```xml mvn test -PRegression ```
