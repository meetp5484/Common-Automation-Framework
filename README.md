### **Common Automation Framework**

A comprehensive automation library designed to simplify and unify testing across Web, Mobile ,API and Desktop platforms. This framework encapsulates modular and reusable components, allowing seamless integration into any project.

**Key Features**

->Unified driver factory for Web, Mobile, Api and Desktop automation.

->Data-driven testing support using Excel or JSON files.

->Externalized configuration for flexibility (e.g., environment, credentials, device details).

->Supports multiple frameworks like TestNG, JUnit, and Cucumber for BDD.

->Centralized utility classes for reusable functions across projects.

->Easily extensible for future technologies and platforms.

->Generate interactive Allure Reports with a comprehensive dashboard.

->Automatically send Allure Reports via email after test execution.

->A new CLI command that allows you to generate essential automation files instantly for Web, Mobile, API, and Desktop automation! 🎯With a single command

### **Project structure**

```
project-root/
├── allure-results/  (Generated during test execution)
├── allure-report/   (Generated after running Allure report command)
|──lib/CommonAutomation-1.0-SNAPSHOT.jar
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── PageObject/
│   │   │       └── pageObject.java
│   │   ├── resources/
│   │       ├── TestData/
│   │       │   └── RequestBody.json
│   │       ├── steps.html
│   │       └── application.properties
│   ├── test/
│   │   ├── java/
│   │   │   ├── stepDefination/
│   │   │   │   └── StepDefination.java
│   │   │   └── testRunner/
│   │   │       └── TestRunner.java
│   │   ├── resources/
│   │   │   ├── feature/
│   │   │   │   └── feature.feature
│   │   │   ├── web/
│   │   │   │   └── img.png (auto-generated if screenshot=true in application.properties)
│   │   │   ├── mobile/
│   │   │   │   └── img.png (auto-generated if screenshot=true in application.properties)
│   │   │   ├── desktop/
│   │   │   │   └── img.png (auto-generated if screenshot=true in application.properties)
|─bddGen.bat ( for windows)
|─bddGen.sh ( for Mac/Linux)
|─pom.xml
```

### **How to Use the Framework**

>**Common configuration**
- Configuring JDK 22 for the Project
- Download the JAR file from the provided attachment or link
- If using an IDE like IntelliJ or Eclipse:
- Create a folder inside the project and add the JAR file to the folder.
-  Add Dependency to `pom.xml`
```
   <dependency>    
     <groupId>org.example</groupId>    
     <artifactId>CommonAutomation</artifactId>    
     <version>1.0-SNAPSHOT</version>
   </dependency> 
   <build>
        <resources>
            <resource>
                <directory>${project.basedir}/lib</directory>
                <includes>
                    <include>*.jar</include>
                </includes>
            </resource>
        </resources>
    </build>
 ```
- Ensure your project compiles without errors and the JAR is recognized in your IDE.


### 📌 How to Use One-Command BDD Setup?
### **For Windows Users**
 1️⃣ Create a bat file  under project `(bddGen.bat)` and add the following text:
 **bddGen.bat:**
```
@echo off 
java -jar lib/CommonAutomation-1.0-SNAPSHOT.jar %1 %2  
```

2️⃣Run the command in the terminal:
`.\bddGen <File_Name> <Environment>`

Example:
`.\bddGen Login Web`
After running the command, the following files will be automatically created:
```
Login.feature (Feature file)
LoginDefinition.java (Step Definition file)
LoginObject.java (Page Object file)
```

### **For macOS/Linux Users**
1️⃣ Create a shell script under project`(bddGen.sh)` and add the following text:
```
#!/bin/bash  
java -jar lib/CommonAutomation-1.0-SNAPSHOT.jar $1 $2
```
2️⃣ Grant execute permission:
Command: `chmod +x bddGen.sh`

3️⃣ Run the command:
`.\bddGen.sh <File_Name> <Environment>
`
Example:
`.\bddGen.sh Login Web`
After running the command, the following files will be automatically created:
```
Login.feature (Feature file)
LoginDefinition.java (Step Definition file)
LoginObject.java (Page Object file)
```

> **How to install Allure Reports?**

- To generate and open Allure reports, install Allure Command Line using:
`npm install -g allure-commandline`

> **Prerequisite: Ensure Node.js is installed before running the command.**

- Install Node.js:

1. Download Node.js: https://nodejs.org/en/download
2. Verify installation: Run the following command:
```
node --version  
npm --version  
```
3. Re-run the command if now installed node so:
`npm install -g allure-commandline`

**How to set allure report**
1. Convert json allure-results to viewable allure-report at your project directory path.
`allure generate allure-results --clean -o allure-report`
- allure generate → Converts JSON reports to an HTML report.
- allure-results → Input folder where Allure stores test execution data.
- --clean → Removes old reports before generating a new one.
- -o allure-report → Output folder where the HTML report is saved.
2. To open the Allure report dashboard, run the following command:
`allure open allure-report`


### Configure application.properties
Create an application.properties file in your project's src/main/resources directory and include the following configurations:
**Updated application.properties file:**

```
#Environments setup  -> web|mobile|api
testEnvironment=web

# Web settings -> chrome | firefox | edge
browser=chrome
baseurl=http://google.com

# Mobile settings -> android | ios
platformName= android
appPath=Path/to/apk
#If you want to reinstall the application on your mobile, select "true." Otherwise, select "false."
reinstallApp=false
#Flags will be dynamically set based on connected devices
runOnDevice1=true
runOnDevice2=false
appPackage=com.google.calculator
appActivity=com.google.calculator.MainActivity
#IOS-> XCUITest
bundleId=?
udid=00 D0 Db EF 21 B9 20 BF D2 83 71 00 6B C0 4F 81 CX


# API settings
apiBaseUri= https://reqres.in/
apiBasePath= /Test/
Token=Bearer Token
#If you want to open the browser to see how many APIs passed and failed, select "True." Otherwise, select "False."
openBrowserForApi=true

#Desktop settings
imageBasePath=path/to/resource_page
openanysoftware=notepad



#Screenshot true | false
#If you want to capture a screenshot of a failed step, you can achieve it by using a simple true/false value for the screenshot configuration below.
#This approach allows easy screenshot capturing for both web and mobile applications.
screenshot= true
screenshot.path=src/test/resources

#The test report is sent only when the full test suite runs via `testRunner.TestRunner` and `EnableEmail` is set to `true`; otherwise, no email is sent.
EnableEmail=true
#The report path should be the same as the test runner file.
report.path=C:/Users/public/Desktop
mail.smtp.host=smtp.office365.com
mail.smtp.port=587
mail.smtp.auth=true
mail.smtp.starttls.enable=true
#Enter Email details
FromEmail=Test123@gmail.com
Password=Test@12345
ToEmail=Test456@gmail.com
Subject=Allure Test Execution Report
BodyText=Please find the attached Allure test execution report.
```

### **🌐 Web Automation Features**

>Cross-Browser Testing

->Supports Chrome, Firefox and Edge.

->Configurable through external properties files.

>Dynamic Element Handling

->Wait utilities for dynamic elements (e.g., waitForElementToBeClickable, waitForVisibility).

>Screenshot Utility

->Automatic screenshots on failure for debugging.

>Environment Management

->Switch between QA, Staging, and Production with a single configuration change.

>Custom Reporting

->HTML and log reports for test execution summaries.

 **Web Automation example**

Change the value of `testEnvironment` to `'web'` in the `application.properties` file.

- Feature file:

```
Feature: Testfile

  Scenario: Check the browser and all hook workign or not
    Given open browser link and click on continue
    And search test player into gang  
```
- StepDefination file:

```
package stepDefination;

import io.cucumber.java.en.And;
import io.cucumber.java.en.Given;
import pageObject.WebObject;

public class webDefination {
    private WebObject webObject;

    public webDefination(WebObject webObject) {
        this.webObject = webObject;
    }

    @Given("open browser link and click on continue")
    public void open_Browser_Link_And_Click_On_Continue() throws InterruptedException {
        webObject.openBrowserLinkAndClickOnContinue();
    }

    @And("search test player into gang")
    public void searchTestPlayerIntoGang() {
        webObject.breakpoint();
    }
}
```

PageObject file:
```
package pageObject;

import core.utils.WebUtils;
import hooks.TestHooks;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;

public class WebObject {

private final WebDriver driver;

    public WebObject() {
        this.driver = TestHooks.getWebDriver();
    }

    public void openBrowserLinkAndClickOnContinue() throws InterruptedException {
        driver.get("https://www.google.com/");
        Thread.sleep(2000);
    }

    public void breakpoint() {
        WebElement example= driver.findElement(By.xpath("TestElement"));
        WebUtils.waitForElementToBeVisible(driver, example,20);
    }
}
```
...................................................


### **📱 Mobile Automation Features**

>Cross-Platform Mobile Automation

->Unified framework for Android and iOS devices.

->Supports both real devices and emulators/simulators.

>Device Management

->Dynamic detection of connected devices from adb.

->one by one execution on multiple devices.

>App Lifecycle Management

->Install, launch, and uninstall apps during test execution.

>Comprehensive Reporting

->HTML reports execution details.

>Screenshot Utility

->Automatic screenshots on failure for debugging.

**Mobile Automation example**

Change the value of `testEnvironment` to `'mobile'` in the `application.properties` file.

Feature file:
```
Feature: Mobile testing
  Scenario: here i was checking the mobile setup
    Given i am on login page
```
StepDefination file:
```
package stepDefination;

import io.cucumber.java.en.Given;
import pageObject.MobileObject;

public class mobileDefination {
private MobileObject mobileObject;

    public mobileDefination(MobileObject mobileObject) {
        this.mobileObject = mobileObject;
    }

    @Given("i am on login page")
    public void iAmOnLoginPage() throws InterruptedException {
        mobileObject.loginpage();
    }
}
```
PageObject file:
```
package pageObject;

import hooks.TestHooks;
import io.appium.java_client.AppiumDriver;
import org.openqa.selenium.By;

public class MobileObject {
    private final AppiumDriver driver;

    public MobileObject() {
        this.driver = TestHooks.getMobileDriver();
    }
    public void loginpage() throws InterruptedException {
        Thread.sleep(3000);
        driver.findElement(By.xpath("//android.widget.Button[@content-desc=\"EINLOGGEN\"]")).click();
        Thread.sleep(3000);
    }
}
```


### 🔗 API Automation Features

>Token-Based Authentication

->Background API calls to retrieve tokens for secure authentication.

>Parameterized Testing

->Read input data from Excel or JSON for dynamic API tests.

>Built-in Validation

->Verify status codes, response payloads, and headers with predefined utilities.

>Customizable API Paths

->Dynamically pass API paths through properties or feature files.

>Integrated Reporting

->Automatically logs request/response details and generates HTML reports.

>Environment Flexibility

->Separate base URIs for testing environments.

>Open Browser while run api feature/sceanrios.

->The user sets the value of `'OpenBrowserforApi'` to `'true'` in the `'application.properties'` file, enabling the browser to open while a feature or scenario is running.
>
> **Api Automation example**

Change the value of `testEnvironment` to `'api'` in the `application.properties` file.

Feature file:
```
Feature:api tesitng check
  Scenario: Open api and setup
    Given user able to see api
    And setup the name of api
    And setup the name of params
    When setup the name of method
    And setup the name of response
    Then check the openapi version

  Scenario: Open api and setup2
    Given user able to see api
    And setup the name of api
    And setup the name of params
    When setup the name of method
    And setup the name of response
    Then check the openapi version
```

StepDefination file:
```
package stepDefination;

import io.cucumber.java.en.And;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;
import pageObject.ApiObject;

public class apiDefination {
private ApiObject apiObject;

    public apiDefination(ApiObject apiObject) {
        this.apiObject = apiObject;
    }
    @Given("user able to see api")
    public void userAbleToSeeApi() {
        apiObject.userCallGetApi();
    }

    @And("setup the name of api")
    public void setupTheNameOfApi() {
        apiObject.userSetupNameOfApi();
    }

    @And("setup the name of params")
    public void setupTheNameOfParams() {
        apiObject.userSetupNameOfParams();
    }

    @When("setup the name of method")
    public void setupTheNameOfMethod() {
        apiObject.userSetupNameOfMethod();

    }

    @And("setup the name of response")
    public void setupTheNameOfResponse() {
        apiObject.userSetupNameOfResponse();

    }

    @Then("check the openapi version")
    public void checkTheOpenapiVersion() {
        apiObject.userCheckOpenapiVersion();
    }
}
```
PageObject:
```
package pageObject;

import hooks.TestHooks;
import io.appium.java_client.AppiumDriver;
import org.openqa.selenium.By;

public class MobileObject {
    private final AppiumDriver driver;

    public MobileObject() {
        this.driver = TestHooks.getMobileDriver();
    }
    public void loginpage() throws InterruptedException {
        Thread.sleep(3000);
        driver.findElement(By.xpath("//android.widget.Button[@content-desc=\"LOGIN\"]")).click();
        Thread.sleep(3000);
    }
}
```
### 🔗 Desktop Automation Features
> Dynamic Screen Handling

-> Adapts to different screen resolutions and UI scaling.

-> Supports multi-monitor setups by detecting the active screen.


> Robot Framework Integration

-> Uses Java’s Robot class to simulate keyboard and mouse actions.

-> Handles key combinations (e.g., Ctrl+C, Alt+Tab) and special keys like Enter or Esc.

> Custom Utility Functions

-> getImagePattern(): Retrieves screen elements dynamically based on images.

-> openCustomApplication(): Launches desktop applications using configurations.

-> captureScreen(): Takes and stores screenshots for debugging.

> Cross-Platform Support

-> Runs on Windows, macOS, and Linux.

-> Adapts to different OS-specific shortcuts and application behaviors.

> **Desktop Automation example**

- Feature file:

```
Feature: Here We are testing the desktop
  Scenario: open notepad for write something
    Given I am on the desktop
    When open to click on "1737552512019.png".
    And I write "Hello, World!"
    Then save and close "close_icon.png" notepad
```

- StepDefination file:
```
package stepDefination;

import io.cucumber.java.en.And;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;
import org.sikuli.script.FindFailed;
import pageObject.DesktopObject;

import java.awt.*;

public class desktopDefination {

    private DesktopObject desktopObject;

    public desktopDefination(DesktopObject desktopObject) {
        this.desktopObject = desktopObject;
    }

    @Given("I am on the desktop")
    public void iAmOnTheDesktop() {
        desktopObject.iAmOnTheDesktop();

    }
    @When("open to click on {string}.")
    public void openNotToClieckOn(String arg0) throws FindFailed, InterruptedException, AWTException {
        desktopObject.openNotToClieckOn(arg0);
    }

    @And("I write {string}")
    public void iWrite(String arg0) throws FindFailed {
        desktopObject.iWrite(arg0);

    }

    @Then("save and close {string} notepad")
    public void saveAndCloseNotepad(String arg0) throws FindFailed {
        desktopObject.saveAndCloseNotepad(arg0);
    }
}
```

PageObject file:

```
package pageObject;

import core.utils.DesktopUtils;
import hooks.TestHooks;
import org.sikuli.hotkey.Keys;
import org.sikuli.script.FindFailed;
import org.sikuli.script.Key;
import org.sikuli.script.Pattern;
import org.sikuli.script.Screen;

import java.awt.*;
import java.awt.event.KeyEvent;

import static core.utils.CommonUtils.logInfo;

public class DesktopObject {
    private Screen screen;
    private Robot robot;

    public DesktopObject() {
        this.screen = TestHooks.getScreen();
        this.robot = TestHooks.getRobot();
    }

    public void iAmOnTheDesktop() {
        logInfo("Desktop Automation");
    }

    public void openNotToClieckOn(String arg0) throws FindFailed {

        Pattern pattern = DesktopUtils.getImagePattern(arg0);   // I used a desktop utility that requires me to enter the image path only once..
        robot.keyPress(KeyEvent.VK_WINDOWS);
        robot.keyPress(KeyEvent.VK_D);
        robot.keyRelease(KeyEvent.VK_D);
        robot.keyRelease(KeyEvent.VK_WINDOWS);

        //open the existing notepad file
        screen.doubleClick(pattern);
      
    }

    public void iWrite(String arg0) throws FindFailed {
        Pattern notepad = DesktopUtils.getImagePattern(arg0);
        //Text entered in notepad file
        screen.type(notepad, "Hello");
    }

    public void saveAndCloseNotepad(String arg0) throws FindFailed {
        screen.type("s", Key.CTRL);
        Pattern closeNotepad = DesktopUtils.getImagePattern(arg0);

        //Close the notepad file
        screen.click(closeNotepad);
    }
}
```


- **Common TestRunner file:**

```
package testRunner;

import core.listener.TestListener;
import io.cucumber.testng.AbstractTestNGCucumberTests;
import io.cucumber.testng.CucumberOptions;
import org.testng.annotations.Listeners;



@CucumberOptions(
        features = "src/test/resources/feature/simple.feature",
        glue = {"hooks", "stepDefination"},
        plugin = {
                "pretty",
                "io.qameta.allure.cucumber7jvm.AllureCucumber7Jvm"
        },
        monochrome = true
)
@Listeners(TestListener.class)
public class TestRunner extends AbstractTestNGCucumberTests {
}
```

### 📥 Downloads and Releases
Find the latest releases and JAR files here:
📦 GitHub Releases

### 📧 Support
For any issues or questions, please open an issue on GitHub or contact us at meetp5484@gmail.com.
