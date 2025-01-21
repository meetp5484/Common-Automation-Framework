### **Common Automation Framework**

A comprehensive automation library designed to simplify and unify testing across Web, Mobile and API platforms. This framework encapsulates modular and reusable components, allowing seamless integration into any project.

**Key Features**

->Unified driver factory for Web, Mobile, and Api automation.

->Data-driven testing support using Excel or JSON files.

->Externalized configuration for flexibility (e.g., environment, credentials, device details).

->Supports multiple frameworks like TestNG, JUnit, and Cucumber for BDD.

->Centralized utility classes for reusable functions across projects.

->Easily extensible for future technologies and platforms.

### **Project structure**

```
project-root/
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
│   └── test/
│       ├── java/
│       │   ├── stepDefination/
│       │   │   └── StepDefination.java
│       │   └── testRunner/
│       │       └── TestRunner.java
│       ├── resources/
│       │   ├── feature/
│       │   │   └── feature.feature
│       │   ├── web/
│       │   │   └── img.png (auto-generated if screenshot=true in application.properties)
│       │   └── mobile/
│       │       └── img.png (auto-generated if screenshot=true in application.properties)
```

### **How to Use the Framework**

>**Common configuration**

- Download the JAR file from the provided attachment or link
- If using an IDE like IntelliJ or Eclipse:
-  Right-click on the JAR file → Add as `Library`.
-  If not using a build tool like Maven or Gradle, manually add the JAR to the project’s build path.
-  Add Dependency to `pom.xml`
```
   <dependency>    
     <groupId>org.example</groupId>    
     <artifactId>CommonAutomation</artifactId>    
     <version>1.0-SNAPSHOT</version>
   </dependency> 
 ```
- Ensure your project compiles without errors and the JAR is recognized in your IDE.


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

- **Common TestRunner file:**

```
package testRunner;

import io.cucumber.testng.AbstractTestNGCucumberTests;
import io.cucumber.testng.CucumberOptions;

@CucumberOptions(
        features = "src/test/resources/feature/simple.feature", // Path to your feature files
        glue = {"hooks","stepDefination"},      // Path to your step definitions and hooks
        plugin = {
                "pretty",                              // Prints Gherkin steps in the console
                "json:target/cucumber-reports/Cucumber.json", // JSON report
                "html:target/cucumber-reports/Cucumber.html"  // HTML report
        }
        )
public class TestRunner extends AbstractTestNGCucumberTests {
}
```
