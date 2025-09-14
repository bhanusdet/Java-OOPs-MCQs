# Java Design Patterns 🚀

### 🎯 Top 8 Must-Know Patterns 
1. **Singleton** - WebDriver instance, Configuration
2. **Factory** - Browser creation, Test data creation  
3. **Builder** - Test case creation, Complex objects
4. **Page Object Model (POM)** - UI automation standard
5. **Strategy** - Different test execution strategies
6. **Observer** - Test result listeners, Reporting
7. **Command** - Test step execution, Action chains
8. **Template Method** - Test execution workflow

### 🔥 Quick Interview Prep Points
- **Most Asked**: Singleton (WebDriver), Factory (Browser), Strategy (Test execution)
- **Framework Design**: Builder, Observer, Template Method
- **Code Quality**: When NOT to use patterns (over-engineering)

---

## Test Automation Framework Patterns {#framework-patterns}

### 1. 🌐 WebDriver Singleton Pattern
**Problem**: Multiple WebDriver instances cause conflicts  
**Solution**: Single WebDriver instance throughout test execution

```java
public class WebDriverManager {
    private static WebDriver driver;
    private static final Object lock = new Object();

    private WebDriverManager() {}

    public static WebDriver getDriver() {
        if (driver == null) {
            synchronized (lock) {
                if (driver == null) {
                    initializeDriver();
                }
            }
        }
        return driver;
    }

    private static void initializeDriver() {
        String browserType = System.getProperty("browser", "chrome");
        driver = BrowserFactory.createBrowser(browserType);
    }

    public static void quitDriver() {
        if (driver != null) {
            driver.quit();
            driver = null;
        }
    }
}
```

**SDET Interview Points**:
- ✅ Prevents multiple browser instances
- ✅ Thread-safe implementation
- ❌ Difficult to test in parallel
- **Alternative**: ThreadLocal for parallel execution

### 2. 🏭 Browser Factory Pattern
**Problem**: Hard-coded browser initialization  
**Solution**: Dynamic browser creation based on configuration

```java
public class BrowserFactory {
    public static WebDriver createBrowser(String browserType) {
        switch (browserType.toLowerCase()) {
            case "chrome":
                WebDriverManager.setup().chromedriver();
                ChromeOptions chromeOptions = new ChromeOptions();
                chromeOptions.addArguments("--headless", "--no-sandbox");
                return new ChromeDriver(chromeOptions);

            case "firefox":
                WebDriverManager.setup().firefoxdriver();
                FirefoxOptions firefoxOptions = new FirefoxOptions();
                firefoxOptions.setHeadless(true);
                return new FirefoxDriver(firefoxOptions);

            case "edge":
                WebDriverManager.setup().edgedriver();
                return new EdgeDriver();

            default:
                throw new IllegalArgumentException("Browser not supported: " + browserType);
        }
    }
}
```

**SDET Benefits**:
- ✅ Easy browser switching via configuration
- ✅ Centralized browser setup
- ✅ Environment-specific configurations

### 3. 🏗️ Test Builder Pattern
**Problem**: Complex test setup with many optional parameters  
**Solution**: Fluent API for test creation

```java
public class TestCaseBuilder {
    private String testName;
    private String description;
    private String browser;
    private Map<String, Object> testData;
    private List<String> tags;
    private int priority;

    public TestCaseBuilder setTestName(String testName) {
        this.testName = testName;
        return this;
    }

    public TestCaseBuilder setDescription(String description) {
        this.description = description;
        return this;
    }

    public TestCaseBuilder setBrowser(String browser) {
        this.browser = browser;
        return this;
    }

    public TestCaseBuilder addTestData(String key, Object value) {
        if (testData == null) testData = new HashMap<>();
        testData.put(key, value);
        return this;
    }

    public TestCaseBuilder addTag(String tag) {
        if (tags == null) tags = new ArrayList<>();
        tags.add(tag);
        return this;
    }

    public TestCaseBuilder setPriority(int priority) {
        this.priority = priority;
        return this;
    }

    public TestCase build() {
        return new TestCase(testName, description, browser, testData, tags, priority);
    }
}

// Usage in Test
TestCase loginTest = new TestCaseBuilder()
    .setTestName("Valid Login Test")
    .setDescription("Test successful login with valid credentials")
    .setBrowser("chrome")
    .addTestData("username", "testuser@example.com")
    .addTestData("password", "password123")
    .addTag("smoke")
    .addTag("login")
    .setPriority(1)
    .build();
```

### 4. 📄 Page Object Model (Enhanced)
**Problem**: UI elements scattered across test code  
**Solution**: Centralized page element management

```java
// Base Page Class
public abstract class BasePage {
    protected WebDriver driver;
    protected WebDriverWait wait;

    public BasePage(WebDriver driver) {
        this.driver = driver;
        this.wait = new WebDriverWait(driver, Duration.ofSeconds(10));
        PageFactory.initElements(driver, this);
    }

    protected void waitAndClick(WebElement element) {
        wait.until(ExpectedConditions.elementToBeClickable(element));
        element.click();
    }

    protected void waitAndType(WebElement element, String text) {
        wait.until(ExpectedConditions.visibilityOf(element));
        element.clear();
        element.sendKeys(text);
    }
}

// Login Page Implementation
public class LoginPage extends BasePage {
    @FindBy(id = "username")
    private WebElement usernameField;

    @FindBy(id = "password") 
    private WebElement passwordField;

    @FindBy(css = "button[type='submit']")
    private WebElement loginButton;

    @FindBy(css = ".error-message")
    private WebElement errorMessage;

    public LoginPage(WebDriver driver) {
        super(driver);
    }

    public DashboardPage login(String username, String password) {
        waitAndType(usernameField, username);
        waitAndType(passwordField, password);
        waitAndClick(loginButton);
        return new DashboardPage(driver);
    }

    public String getErrorMessage() {
        wait.until(ExpectedConditions.visibilityOf(errorMessage));
        return errorMessage.getText();
    }

    public boolean isLoginPageDisplayed() {
        return usernameField.isDisplayed() && passwordField.isDisplayed();
    }
}
```

### 5. 🎯 Strategy Pattern for Test Execution
**Problem**: Different test execution strategies (sequential, parallel, distributed)  
**Solution**: Interchangeable execution strategies

```java
// Strategy Interface
public interface TestExecutionStrategy {
    void executeTests(List<TestCase> tests);
}

// Sequential Execution
public class SequentialExecution implements TestExecutionStrategy {
    public void executeTests(List<TestCase> tests) {
        for (TestCase test : tests) {
            System.out.println("Executing test sequentially: " + test.getName());
            test.execute();
        }
    }
}

// Parallel Execution
public class ParallelExecution implements TestExecutionStrategy {
    public void executeTests(List<TestCase> tests) {
        tests.parallelStream().forEach(test -> {
            System.out.println("Executing test in parallel: " + test.getName());
            test.execute();
        });
    }
}

// Test Runner Context
public class TestRunner {
    private TestExecutionStrategy strategy;

    public void setStrategy(TestExecutionStrategy strategy) {
        this.strategy = strategy;
    }

    public void runTests(List<TestCase> tests) {
        strategy.executeTests(tests);
    }
}

// Usage
TestRunner runner = new TestRunner();
runner.setStrategy(new ParallelExecution());
runner.runTests(testSuite);
```

### 6. 👁️ Observer Pattern for Test Reporting
**Problem**: Multiple reporting systems need test results  
**Solution**: Observer pattern for result notification

```java
// Observer Interface
public interface TestResultObserver {
    void onTestStart(TestCase test);
    void onTestPass(TestCase test);
    void onTestFail(TestCase test, String reason);
    void onTestSkip(TestCase test, String reason);
}

// Concrete Observers
public class HTMLReporter implements TestResultObserver {
    public void onTestStart(TestCase test) {
        System.out.println("HTML: Test started - " + test.getName());
    }

    public void onTestPass(TestCase test) {
        System.out.println("HTML: ✅ Test passed - " + test.getName());
    }

    public void onTestFail(TestCase test, String reason) {
        System.out.println("HTML: ❌ Test failed - " + test.getName() + ": " + reason);
    }

    public void onTestSkip(TestCase test, String reason) {
        System.out.println("HTML: ⏭️ Test skipped - " + test.getName() + ": " + reason);
    }
}

public class ExtentReporter implements TestResultObserver {
    public void onTestStart(TestCase test) {
        // ExtentReports implementation
        System.out.println("Extent: Test started - " + test.getName());
    }

    public void onTestPass(TestCase test) {
        System.out.println("Extent: ✅ Test passed - " + test.getName());
    }

    public void onTestFail(TestCase test, String reason) {
        System.out.println("Extent: ❌ Test failed - " + test.getName());
    }

    public void onTestSkip(TestCase test, String reason) {
        System.out.println("Extent: ⏭️ Test skipped - " + test.getName());
    }
}

// Test Execution Manager
public class TestExecutionManager {
    private List<TestResultObserver> observers = new ArrayList<>();

    public void addObserver(TestResultObserver observer) {
        observers.add(observer);
    }

    public void removeObserver(TestResultObserver observer) {
        observers.remove(observer);
    }

    private void notifyTestStart(TestCase test) {
        observers.forEach(observer -> observer.onTestStart(test));
    }

    private void notifyTestPass(TestCase test) {
        observers.forEach(observer -> observer.onTestPass(test));
    }

    private void notifyTestFail(TestCase test, String reason) {
        observers.forEach(observer -> observer.onTestFail(test, reason));
    }
}
```

---

## Core Patterns with QA Examples {#core-patterns}

### 🏭 Factory Pattern - Test Data Creation
```java
public class TestDataFactory {
    public static User createUser(String userType) {
        switch (userType.toLowerCase()) {
            case "admin":
                return new User("admin@test.com", "admin123", "ADMIN");
            case "regular":
                return new User("user@test.com", "user123", "USER");
            case "guest":
                return new User("guest@test.com", "", "GUEST");
            default:
                return new User("default@test.com", "default123", "USER");
        }
    }

    public static PaymentMethod createPaymentMethod(String type) {
        switch (type.toLowerCase()) {
            case "creditcard":
                return new CreditCard("4111111111111111", "123", "12/25");
            case "paypal":
                return new PayPal("test@paypal.com", "paypal123");
            default:
                throw new IllegalArgumentException("Payment method not supported");
        }
    }
}
```

### 🔧 Command Pattern - Test Actions
```java
// Command Interface
public interface TestAction {
    void execute();
    void undo();
    String getDescription();
}

// Concrete Commands
public class ClickAction implements TestAction {
    private WebElement element;
    private String elementName;

    public ClickAction(WebElement element, String elementName) {
        this.element = element;
        this.elementName = elementName;
    }

    public void execute() {
        element.click();
        System.out.println("Clicked on: " + elementName);
    }

    public void undo() {
        // Navigate back or restore previous state
        System.out.println("Undoing click on: " + elementName);
    }

    public String getDescription() {
        return "Click on " + elementName;
    }
}

public class TypeAction implements TestAction {
    private WebElement element;
    private String text;
    private String previousText;

    public TypeAction(WebElement element, String text) {
        this.element = element;
        this.text = text;
        this.previousText = element.getAttribute("value");
    }

    public void execute() {
        element.clear();
        element.sendKeys(text);
        System.out.println("Typed: " + text);
    }

    public void undo() {
        element.clear();
        element.sendKeys(previousText);
        System.out.println("Restored previous text: " + previousText);
    }

    public String getDescription() {
        return "Type '" + text + "'";
    }
}

// Test Action Manager
public class TestActionManager {
    private Stack<TestAction> executedActions = new Stack<>();

    public void executeAction(TestAction action) {
        action.execute();
        executedActions.push(action);
    }

    public void undoLastAction() {
        if (!executedActions.isEmpty()) {
            TestAction lastAction = executedActions.pop();
            lastAction.undo();
        }
    }

    public void undoAllActions() {
        while (!executedActions.isEmpty()) {
            undoLastAction();
        }
    }
}
```

### 📋 Template Method - Test Execution Workflow
```java
public abstract class BaseTest {
    // Template method
    public final void runTest() {
        setupTest();
        setupTestData();
        executeTestSteps();
        verifyResults();
        cleanupTest();
    }

    protected void setupTest() {
        System.out.println("🔧 Setting up test environment...");
        // Common setup logic
    }

    protected void setupTestData() {
        System.out.println("📊 Setting up test data...");
        // Common test data setup
    }

    // Abstract methods - must be implemented by subclasses
    protected abstract void executeTestSteps();
    protected abstract void verifyResults();

    protected void cleanupTest() {
        System.out.println("🧹 Cleaning up test environment...");
        // Common cleanup logic
    }
}

// Concrete Test Implementation
public class LoginTest extends BaseTest {
    protected void executeTestSteps() {
        System.out.println("1. Navigate to login page");
        System.out.println("2. Enter username and password");
        System.out.println("3. Click login button");
    }

    protected void verifyResults() {
        System.out.println("✅ Verify user is logged in successfully");
        System.out.println("✅ Verify dashboard is displayed");
    }
}
```

---

## Pattern Implementation Cheat Sheet {#cheat-sheet}

### 🚀 Quick Implementation Guide

| Pattern | When to Use | SDET Example | Code Template |
|---------|-------------|--------------|---------------|
| **Singleton** | Single instance needed | WebDriver, Config | `private static volatile Instance` |
| **Factory** | Object creation varies | Browser, TestData | `switch(type) { case "x": return new X(); }` |
| **Builder** | Complex object creation | TestCase, TestSuite | `return this` for chaining |
| **Strategy** | Algorithm varies | Test execution, Reporting | `interface Strategy { void execute(); }` |
| **Observer** | Event notification | Test results, Logging | `List<Observer> observers` |
| **Command** | Action encapsulation | Test steps, Undo operations | `interface Command { void execute(); }` |
| **Template Method** | Algorithm skeleton | Test workflow | `final void templateMethod()` |
| **Adapter** | Interface compatibility | Third-party tools | `implements Target, wraps Adaptee` |

### 🎯 Pattern Selection for Common SDET Scenarios

| Scenario | Recommended Pattern | Why? |
|----------|-------------------|------|
| WebDriver management | Singleton + Factory | Single instance + multiple browsers |
| Page objects | Factory + Builder | Dynamic page creation + complex setup |
| Test data creation | Factory + Builder | Different data types + optional fields |
| Test execution | Strategy + Template Method | Multiple strategies + common workflow |
| Reporting | Observer + Strategy | Multiple reporters + different formats |
| Test actions | Command | Undo capability + action logging |
| Framework integration | Adapter | Third-party tool compatibility |

---

## Interview Q&A {#interview-qa}

### 🎤 Top SDET Design Pattern Interview Questions

**Q1: How would you implement WebDriver using Singleton pattern? What are the pros and cons?**

**A:** 
```java
// Thread-safe Singleton for WebDriver
public class WebDriverManager {
    private static volatile WebDriver driver;

    public static WebDriver getDriver() {
        if (driver == null) {
            synchronized (WebDriverManager.class) {
                if (driver == null) {
                    driver = new ChromeDriver();
                }
            }
        }
        return driver;
    }
}
```

**Pros:** Single browser instance, memory efficient  
**Cons:** Parallel execution issues, testing difficulties  
**Solution:** Use ThreadLocal for parallel execution

---

**Q2: Explain Factory pattern in test automation with example.**

**A:** Factory creates objects without specifying exact classes.
```java
public class BrowserFactory {
    public static WebDriver createDriver(String browser) {
        switch(browser.toLowerCase()) {
            case "chrome": return new ChromeDriver();
            case "firefox": return new FirefoxDriver();
            default: throw new IllegalArgumentException("Unsupported browser");
        }
    }
}
```

**Benefits:** Easy browser switching, centralized configuration, maintainable code

---

**Q3: How does Page Object Model relate to design patterns?**

**A:** POM combines multiple patterns:
- **Factory**: Creating page instances
- **Singleton**: Shared driver instance  
- **Builder**: Complex page setup
- **Template Method**: Common page operations

---

**Q4: When would you NOT use design patterns in test automation?**

**A:** 
- Simple scripts (over-engineering)
- Proof of concepts
- One-time exploratory testing
- When team lacks pattern knowledge
- Performance-critical scenarios where patterns add overhead

---

**Q5: Explain Observer pattern for test reporting.**

**A:** Multiple reporters observe test execution:
```java
public interface TestObserver {
    void onTestResult(TestResult result);
}

public class TestManager {
    private List<TestObserver> observers = new ArrayList<>();

    public void addObserver(TestObserver observer) {
        observers.add(observer);
    }

    private void notifyObservers(TestResult result) {
        observers.forEach(observer -> observer.onTestResult(result));
    }
}
```

---

## Real Framework Examples {#real-examples}

### 🔧 Selenium Framework with Design Patterns
```java
// Complete framework structure
public class AutomationFramework {

    // Singleton WebDriver Manager
    public class DriverManager {
        private static final ThreadLocal<WebDriver> driverThreadLocal = new ThreadLocal<>();

        public static void setDriver(String browserName) {
            driverThreadLocal.set(BrowserFactory.createDriver(browserName));
        }

        public static WebDriver getDriver() {
            return driverThreadLocal.get();
        }

        public static void quitDriver() {
            WebDriver driver = driverThreadLocal.get();
            if (driver != null) {
                driver.quit();
                driverThreadLocal.remove();
            }
        }
    }

    // Factory for browser creation
    public class BrowserFactory {
        public static WebDriver createDriver(String browser) {
            switch (browser.toLowerCase()) {
                case "chrome":
                    return new ChromeDriver(getChromeOptions());
                case "firefox":
                    return new FirefoxDriver(getFirefoxOptions());
                default:
                    throw new RuntimeException("Browser not supported: " + browser);
            }
        }

        private static ChromeOptions getChromeOptions() {
            ChromeOptions options = new ChromeOptions();
            options.addArguments("--no-sandbox", "--disable-dev-shm-usage");
            if (System.getProperty("headless", "false").equals("true")) {
                options.addArguments("--headless");
            }
            return options;
        }
    }

    // Builder for test configuration
    public class TestConfigBuilder {
        private String browser = "chrome";
        private String environment = "staging";
        private boolean headless = false;
        private int timeout = 30;

        public TestConfigBuilder setBrowser(String browser) {
            this.browser = browser;
            return this;
        }

        public TestConfigBuilder setEnvironment(String environment) {
            this.environment = environment;
            return this;
        }

        public TestConfigBuilder setHeadless(boolean headless) {
            this.headless = headless;
            return this;
        }

        public TestConfig build() {
            return new TestConfig(browser, environment, headless, timeout);
        }
    }
}
```

### 🏗️ TestNG Integration Example
```java
public class BaseTest {
    protected TestConfig config;

    @BeforeClass
    public void setupClass() {
        config = new TestConfigBuilder()
            .setBrowser(System.getProperty("browser", "chrome"))
            .setEnvironment(System.getProperty("env", "staging"))
            .setHeadless(Boolean.parseBoolean(System.getProperty("headless", "false")))
            .build();
    }

    @BeforeMethod
    public void setupTest() {
        DriverManager.setDriver(config.getBrowser());
    }

    @AfterMethod
    public void teardownTest() {
        DriverManager.quitDriver();
    }
}
```

---

## 📚 Key Takeaways for SDET/QA

### ✅ Must Remember Points:
1. **Singleton + ThreadLocal** = Parallel execution support
2. **Factory Pattern** = Easy browser/data switching
3. **Builder Pattern** = Complex test object creation
4. **Page Object Model** = UI automation standard
5. **Observer Pattern** = Multi-reporter support
6. **Strategy Pattern** = Flexible test execution

### 🚨 Common Pitfalls:
1. **Over-engineering** simple test scripts
2. **Singleton without ThreadLocal** in parallel execution
3. **Hard-coded values** instead of Factory pattern
4. **Tight coupling** between test layers
5. **Not considering maintenance** when choosing patterns