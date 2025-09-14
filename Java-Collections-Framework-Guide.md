# Java Collections Framework 

## Collections Hierarchy

### Collections Framework Structure

```
Collection (Interface)
├── List (Interface) - Ordered, allows duplicates
│   ├── ArrayList - Resizable array, fast access
│   ├── LinkedList - Doubly-linked list, fast insertion
│   └── Vector - Synchronized ArrayList (legacy)
│
├── Set (Interface) - No duplicates
│   ├── HashSet - Hash table, no ordering
│   ├── LinkedHashSet - Hash table + insertion order
│   └── TreeSet - Red-black tree, sorted
│
└── Queue (Interface) - FIFO operations
    ├── PriorityQueue - Heap-based priority queue
    ├── ArrayDeque - Resizable array deque
    └── LinkedList - Also implements Queue

Map (Interface) - Key-value pairs, not part of Collection
├── HashMap - Hash table, no ordering
├── LinkedHashMap - Hash table + insertion/access order
├── TreeMap - Red-black tree, sorted by keys
└── ConcurrentHashMap - Thread-safe HashMap
```

## List Implementations

### ArrayList - Most Used in Test Automation

**When to Use:**
- Storing test data (user credentials, test URLs)
- Test result collections
- Dynamic test suite creation
- Frequent random access to elements

```java
// Test Data Management Example
public class TestDataManager {
    private List<User> testUsers;
    private List<String> testUrls;

    public TestDataManager() {
        testUsers = new ArrayList<>();
        testUrls = new ArrayList<>();
        loadTestData();
    }

    public void loadTestData() {
        // Add test users
        testUsers.add(new User("admin@test.com", "admin123", "ADMIN"));
        testUsers.add(new User("user@test.com", "user123", "USER"));
        testUsers.add(new User("guest@test.com", "", "GUEST"));

        // Add test URLs
        testUrls.add("https://staging.example.com");
        testUrls.add("https://dev.example.com");
        testUrls.add("https://qa.example.com");
    }

    public User getRandomUser() {
        Random random = new Random();
        return testUsers.get(random.nextInt(testUsers.size()));
    }

    public List<User> getUsersByRole(String role) {
        return testUsers.stream()
                .filter(user -> user.getRole().equals(role))
                .collect(Collectors.toList());
    }

    // Common ArrayList operations in test automation
    public void demonstrateOperations() {
        List<String> testSteps = new ArrayList<>();

        // Adding elements
        testSteps.add("Open browser");
        testSteps.add("Navigate to URL");
        testSteps.add("Login with credentials");
        testSteps.add("Verify dashboard");

        // Accessing elements
        String firstStep = testSteps.get(0); // O(1) - Fast access

        // Iterating through elements
        for (String step : testSteps) {
            System.out.println("Step: " + step);
        }

        // Checking if element exists
        boolean hasLoginStep = testSteps.contains("Login with credentials");

        // Removing elements
        testSteps.remove("Verify dashboard");
        testSteps.remove(0); // Remove by index

        // Size operations
        int totalSteps = testSteps.size();
        boolean isEmpty = testSteps.isEmpty();

        // Converting to array (useful for assertions)
        String[] stepsArray = testSteps.toArray(new String[0]);
    }
}
```

**ArrayList Key Points:**
- ✅ Fast random access O(1)
- ✅ Dynamic sizing
- ✅ Maintains insertion order
- ✅ Allows null values
- ❌ Slow insertion/deletion in middle O(n)
- ❌ Not thread-safe

### LinkedList - For Sequential Operations

**When to Use:**
- Test step execution with frequent insertion/deletion
- Queue-like operations in test execution
- Building dynamic test flows

```java
// Test Step Execution Example
public class TestStepManager {
    private LinkedList<TestStep> testSteps;

    public TestStepManager() {
        testSteps = new LinkedList<>();
    }

    public void addStep(TestStep step) {
        testSteps.add(step); // O(1) - efficient
    }

    public void addStepAtBeginning(TestStep step) {
        testSteps.addFirst(step); // O(1) - very efficient
    }

    public void insertStepAfter(TestStep newStep, TestStep afterStep) {
        int index = testSteps.indexOf(afterStep);
        if (index != -1) {
            testSteps.add(index + 1, newStep); // O(n) to find, O(1) to insert
        }
    }

    public void executeSteps() {
        Iterator<TestStep> iterator = testSteps.iterator();
        while (iterator.hasNext()) {
            TestStep step = iterator.next();
            try {
                step.execute();
            } catch (Exception e) {
                // Remove failed step for retry logic
                iterator.remove(); // O(1) - efficient removal
                handleStepFailure(step, e);
            }
        }
    }

    // LinkedList as Queue for test execution
    public void executeAsQueue() {
        while (!testSteps.isEmpty()) {
            TestStep step = testSteps.poll(); // Remove and return first element
            step.execute();
        }
    }

    // LinkedList as Stack for rollback operations
    public void rollbackSteps() {
        while (!testSteps.isEmpty()) {
            TestStep step = testSteps.pop(); // Remove and return last element
            step.rollback();
        }
    }
}
```

**LinkedList Key Points:**
- ✅ Fast insertion/deletion at ends O(1)
- ✅ Implements both List and Queue interfaces
- ✅ Good for sequential access
- ✅ No capacity limitations
- ❌ Slow random access O(n)
- ❌ Higher memory overhead (node pointers)

### ArrayList vs LinkedList Comparison

| Operation | ArrayList | LinkedList | Best Choice |
|-----------|-----------|------------|-------------|
| **Access by index** | O(1) | O(n) | ArrayList |
| **Add at end** | O(1) amortized | O(1) | Both equal |
| **Add at beginning** | O(n) | O(1) | LinkedList |
| **Add in middle** | O(n) | O(n) to find + O(1) to insert | Similar performance |
| **Remove by index** | O(n) | O(n) to find + O(1) to remove | Similar performance |
| **Remove by iterator** | O(n) | O(1) | LinkedList |
| **Memory usage** | Lower | Higher (node overhead) | ArrayList |
| **Cache performance** | Better | Worse (non-contiguous) | ArrayList |

## Set Implementations

### HashSet - Unique Test Data

**When to Use:**
- Removing duplicate test data
- Fast lookup operations O(1)
- Storing unique test identifiers
- Email validation in forms

```java
// Test Data Deduplication Example
public class UniqueTestDataManager {
    private Set<String> executedTestIds;
    private Set<User> uniqueUsers;
    private Set<String> validEmails;

    public UniqueTestDataManager() {
        executedTestIds = new HashSet<>();
        uniqueUsers = new HashSet<>();
        validEmails = new HashSet<>();
    }

    public boolean isTestExecuted(String testId) {
        return executedTestIds.contains(testId); // O(1) average case
    }

    public void markTestExecuted(String testId) {
        boolean added = executedTestIds.add(testId);
        if (!added) {
            System.out.println("Test " + testId + " was already executed");
        }
    }

    public void addUniqueUser(User user) {
        if (uniqueUsers.add(user)) { // add() returns false if already exists
            System.out.println("Added new unique user: " + user.getEmail());
        } else {
            System.out.println("User already exists: " + user.getEmail());
        }
    }

    public List<String> removeDuplicateEmails(List<String> emails) {
        // Convert to Set to remove duplicates, then back to List
        Set<String> uniqueEmails = new HashSet<>(emails);
        return new ArrayList<>(uniqueEmails);
    }

    // Set operations for test data validation
    public void validateTestData() {
        Set<String> requiredFields = new HashSet<>();
        requiredFields.add("username");
        requiredFields.add("password");
        requiredFields.add("email");

        Set<String> actualFields = new HashSet<>();
        actualFields.add("username");
        actualFields.add("email");

        // Check if all required fields are present
        Set<String> missingFields = new HashSet<>(requiredFields);
        missingFields.removeAll(actualFields); // Set difference

        if (!missingFields.isEmpty()) {
            System.out.println("Missing fields: " + missingFields);
        }
    }
}
```

**HashSet Key Points:**
- ✅ O(1) average time for add, remove, contains
- ✅ No duplicates allowed
- ✅ Allows one null value
- ✅ Best performance for lookup operations
- ❌ No ordering guarantee
- ❌ Not thread-safe

### TreeSet - Sorted Test Data

**When to Use:**
- Sorted test execution order
- Priority-based test selection
- Maintaining sorted test results
- Range queries on test data

```java
// Priority Test Execution Example
public class PriorityTestManager {
    private TreeSet<TestCase> priorityTests;
    private TreeSet<Integer> testScores;

    public PriorityTestManager() {
        // TreeSet with custom comparator for priority
        priorityTests = new TreeSet<>((t1, t2) -> {
            int priorityCompare = Integer.compare(t1.getPriority(), t2.getPriority());
            if (priorityCompare != 0) return priorityCompare;
            return t1.getName().compareTo(t2.getName()); // Secondary sort by name
        });

        testScores = new TreeSet<>();
    }

    public void addTest(TestCase test) {
        priorityTests.add(test);
    }

    public void executeTestsInPriorityOrder() {
        for (TestCase test : priorityTests) { // Automatically sorted
            System.out.println("Executing: " + test.getName() + 
                             " (Priority: " + test.getPriority() + ")");
            test.execute();
        }
    }

    public TestCase getHighestPriorityTest() {
        return priorityTests.first(); // O(log n)
    }

    public TestCase getLowestPriorityTest() {
        return priorityTests.last(); // O(log n)
    }

    // Range operations for test score analysis
    public void analyzeTestScores(List<Integer> scores) {
        testScores.addAll(scores);

        // Get scores in a specific range
        NavigableSet<Integer> passingScores = testScores.subSet(70, true, 100, true);
        NavigableSet<Integer> failingScores = testScores.headSet(70); // scores < 70
        NavigableSet<Integer> excellentScores = testScores.tailSet(90); // scores >= 90

        System.out.println("Passing scores: " + passingScores);
        System.out.println("Failing scores: " + failingScores);
        System.out.println("Excellent scores: " + excellentScores);

        // Closest values
        Integer closestToTarget = testScores.floor(75); // Largest <= 75
        Integer nextHigher = testScores.ceiling(75);    // Smallest >= 75
    }
}
```

**TreeSet Key Points:**
- ✅ Sorted order (natural or custom comparator)
- ✅ O(log n) for add, remove, contains
- ✅ Range operations support
- ✅ NavigableSet interface methods
- ❌ Slower than HashSet for basic operations
- ❌ No null values allowed
- ❌ Elements must be Comparable or use Comparator

### LinkedHashSet - Insertion Order Preservation

**When to Use:**
- Maintaining order of test execution
- Preserving order of form field validation
- Ordered unique collections

```java
// Test Execution Order Manager
public class OrderedTestManager {
    private LinkedHashSet<String> testExecutionOrder;

    public OrderedTestManager() {
        testExecutionOrder = new LinkedHashSet<>();
    }

    public void addTestsInOrder(String... tests) {
        for (String test : tests) {
            testExecutionOrder.add(test);
        }
    }

    public void executeTestsInOrder() {
        for (String test : testExecutionOrder) {
            // Tests execute in insertion order
            System.out.println("Executing: " + test);
        }
    }
}
```

### Set Implementations Comparison

| Feature | HashSet | LinkedHashSet | TreeSet |
|---------|---------|---------------|---------|
| **Ordering** | No order | Insertion order | Sorted order |
| **Performance** | O(1) average | O(1) average | O(log n) |
| **Null values** | One null allowed | One null allowed | No null |
| **Memory usage** | Lowest | Medium (extra pointers) | Highest (tree structure) |
| **Thread safe** | No | No | No |
| **Use case** | Fast lookups | Ordered unique items | Sorted unique items |

## Map Implementations

### HashMap - Configuration & Test Data Storage

**When to Use:**
- Test configuration properties
- Key-value test data pairs
- Caching test results
- Browser capabilities mapping
- User session data

```java
// Test Configuration Manager
public class TestConfigManager {
    private Map<String, String> testProperties;
    private Map<String, List<String>> browserCapabilities;
    private Map<String, TestResult> testResults;
    private Map<String, User> userCache;

    public TestConfigManager() {
        testProperties = new HashMap<>();
        browserCapabilities = new HashMap<>();
        testResults = new HashMap<>();
        userCache = new HashMap<>();
        loadConfigurations();
    }

    private void loadConfigurations() {
        // Test properties
        testProperties.put("base.url", "https://example.com");
        testProperties.put("timeout", "30");
        testProperties.put("browser", "chrome");
        testProperties.put("headless", "false");
        testProperties.put("environment", "staging");

        // Browser capabilities
        browserCapabilities.put("chrome", Arrays.asList("--no-sandbox", "--disable-gpu", "--headless"));
        browserCapabilities.put("firefox", Arrays.asList("-headless", "--width=1920", "--height=1080"));
        browserCapabilities.put("edge", Arrays.asList("--headless", "--disable-extensions"));
    }

    public String getProperty(String key) {
        return testProperties.get(key);
    }

    public String getProperty(String key, String defaultValue) {
        return testProperties.getOrDefault(key, defaultValue);
    }

    public void setProperty(String key, String value) {
        testProperties.put(key, value);
    }

    public List<String> getBrowserCapabilities(String browser) {
        return browserCapabilities.getOrDefault(browser, new ArrayList<>());
    }

    // Test result caching
    public void cacheTestResult(String testName, TestResult result) {
        testResults.put(testName, result);
    }

    public TestResult getCachedResult(String testName) {
        return testResults.get(testName);
    }

    public boolean hasTestResult(String testName) {
        return testResults.containsKey(testName);
    }

    // User caching for test data
    public User getOrCreateUser(String userId) {
        return userCache.computeIfAbsent(userId, id -> createNewUser(id));
    }

    private User createNewUser(String id) {
        return new User(id + "@test.com", "password123", "USER");
    }

    // Bulk operations
    public void updateProperties(Map<String, String> newProperties) {
        testProperties.putAll(newProperties);
    }

    public Map<String, String> getAllProperties() {
        return new HashMap<>(testProperties); // Return defensive copy
    }

    // Common HashMap operations in testing
    public void demonstrateOperations() {
        Map<String, String> formData = new HashMap<>();

        // Adding key-value pairs
        formData.put("username", "testuser");
        formData.put("password", "secret123");
        formData.put("email", "test@example.com");

        // Accessing values
        String username = formData.get("username");
        String phone = formData.get("phone"); // Returns null if not found
        String phoneWithDefault = formData.getOrDefault("phone", "N/A");

        // Checking existence
        boolean hasUsername = formData.containsKey("username");
        boolean hasValue = formData.containsValue("testuser");

        // Iterating over map
        for (Map.Entry<String, String> entry : formData.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }

        // Keys and values
        Set<String> keys = formData.keySet();
        Collection<String> values = formData.values();

        // Removing elements
        String removedValue = formData.remove("password");
        formData.remove("email", "test@example.com"); // Remove only if value matches
    }
}
```

**HashMap Key Points:**
- ✅ O(1) average time for get, put, remove
- ✅ Allows one null key and multiple null values
- ✅ Best general-purpose Map implementation
- ✅ No ordering of elements
- ❌ Not thread-safe
- ❌ Iteration order not guaranteed

### ConcurrentHashMap - Thread-Safe Operations

**When to Use:**
- Parallel test execution
- Shared test data across threads
- Thread-safe caching
- Multi-threaded test reporting

```java
// Thread-Safe Test Result Manager
public class ThreadSafeTestManager {
    private ConcurrentHashMap<String, TestResult> testResults;
    private ConcurrentHashMap<String, AtomicInteger> testCounts;

    public ThreadSafeTestManager() {
        testResults = new ConcurrentHashMap<>();
        testCounts = new ConcurrentHashMap<>();
    }

    public void recordTestResult(String testName, TestResult result) {
        // Thread-safe put operation
        testResults.put(testName, result);

        // Atomic increment for test counts
        testCounts.computeIfAbsent(testName, k -> new AtomicInteger(0))
                  .incrementAndGet();
    }

    public TestResult getTestResult(String testName) {
        return testResults.get(testName);
    }

    public int getTestCount(String testName) {
        AtomicInteger count = testCounts.get(testName);
        return count != null ? count.get() : 0;
    }

    // Bulk operations that are thread-safe
    public Map<String, TestResult> getPassedTests() {
        return testResults.entrySet().parallelStream()
                .filter(entry -> entry.getValue().getStatus() == Status.PASSED)
                .collect(Collectors.toConcurrentMap(
                    Map.Entry::getKey,
                    Map.Entry::getValue
                ));
    }

    // Safe iteration during concurrent modification
    public void printAllResults() {
        testResults.forEach((testName, result) -> {
            System.out.println(testName + ": " + result.getStatus());
        });
    }
}
```

**ConcurrentHashMap Key Points:**
- ✅ Thread-safe operations
- ✅ Better performance than synchronized HashMap
- ✅ Supports atomic operations
- ✅ Segmented locking for better concurrency
- ❌ No null keys or values allowed
- ❌ Higher memory overhead

### TreeMap - Sorted Key-Value Storage

**When to Use:**
- Sorted test configuration
- Time-based test data storage
- Range queries on test results
- Ordered reporting data

```java
// Sorted Test Configuration Manager
public class SortedConfigManager {
    private TreeMap<String, String> sortedConfig;
    private TreeMap<Date, TestResult> timeBasedResults;

    public SortedConfigManager() {
        sortedConfig = new TreeMap<>();
        timeBasedResults = new TreeMap<>();
        loadSortedConfig();
    }

    private void loadSortedConfig() {
        sortedConfig.put("timeout", "30");
        sortedConfig.put("browser", "chrome");
        sortedConfig.put("environment", "prod");
        sortedConfig.put("baseUrl", "https://example.com");
        // Keys will be automatically sorted: baseUrl, browser, environment, timeout
    }

    public void printConfigInOrder() {
        sortedConfig.forEach((key, value) -> {
            System.out.println(key + ": " + value);
        });
    }

    // Time-based test result analysis
    public void recordTimedResult(Date timestamp, TestResult result) {
        timeBasedResults.put(timestamp, result);
    }

    public Map<Date, TestResult> getResultsInTimeRange(Date startTime, Date endTime) {
        return timeBasedResults.subMap(startTime, true, endTime, true);
    }

    public TestResult getLatestResult() {
        return timeBasedResults.isEmpty() ? null : timeBasedResults.lastEntry().getValue();
    }

    public TestResult getEarliestResult() {
        return timeBasedResults.isEmpty() ? null : timeBasedResults.firstEntry().getValue();
    }
}
```

### Map Implementations Comparison

| Feature | HashMap | LinkedHashMap | TreeMap | ConcurrentHashMap |
|---------|---------|---------------|---------|-------------------|
| **Ordering** | None | Insertion/Access order | Sorted by key | None |
| **Performance** | O(1) average | O(1) average | O(log n) | O(1) average |
| **Null handling** | One null key, multiple null values | Same as HashMap | No null keys | No nulls |
| **Thread safe** | No | No | No | Yes |
| **Memory usage** | Lowest | Low-Medium | Highest | Medium-High |
| **Use case** | General purpose | Order preservation | Sorted keys | Concurrent access |

## Performance Comparison

### Time Complexity Summary

| Operation | ArrayList | LinkedList | HashSet | TreeSet | HashMap | TreeMap |
|-----------|-----------|------------|---------|---------|---------|---------|
| **Add** | O(1) amortized | O(1) | O(1) average | O(log n) | O(1) average | O(log n) |
| **Remove** | O(n) | O(1) if position known | O(1) average | O(log n) | O(1) average | O(log n) |
| **Search/Contains** | O(n) | O(n) | O(1) average | O(log n) | O(1) average | O(log n) |
| **Access by index** | O(1) | O(n) | N/A | N/A | N/A | N/A |

### Space Complexity
- **ArrayList**: O(n) - compact storage
- **LinkedList**: O(n) - extra memory for node pointers
- **HashSet/HashMap**: O(n) - hash table overhead
- **TreeSet/TreeMap**: O(n) - tree structure overhead

## Thread Safety Summary

### Thread-Safe Collections
- **Vector** (legacy, use ArrayList instead)
- **Hashtable** (legacy, use HashMap instead)
- **ConcurrentHashMap** (modern choice)
- **Collections.synchronizedXxx()** wrapper methods

### Making Collections Thread-Safe

```java
// Synchronized wrappers
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
Map<String, String> syncMap = Collections.synchronizedMap(new HashMap<>());

// Modern concurrent collections
ConcurrentHashMap<String, String> concurrentMap = new ConcurrentHashMap<>();
CopyOnWriteArrayList<String> cowList = new CopyOnWriteArrayList<>();
```

## Best Practices for SDET/QA

### 1. Choose Right Collection Based on Use Case

```java
// For test data with frequent random access
List<TestCase> testCases = new ArrayList<>();

// For unique test IDs with fast lookup
Set<String> executedTests = new HashSet<>();

// For configuration key-value pairs
Map<String, String> config = new HashMap<>();

// For ordered test execution
LinkedHashSet<String> orderedTests = new LinkedHashSet<>();

// For sorted priority tests
TreeSet<TestCase> priorityTests = new TreeSet<>(Comparator.comparing(TestCase::getPriority));
```

### 2. Initialize with Proper Capacity

```java
// Avoid frequent resizing if you know approximate size
List<String> testData = new ArrayList<>(1000); // Initial capacity
Map<String, String> config = new HashMap<>(50); // Initial capacity
Set<String> uniqueIds = new HashSet<>(200); // Initial capacity
```

### 3. Use Diamond Operator for Cleaner Code

```java
// Before Java 7
Map<String, List<String>> oldStyle = new HashMap<String, List<String>>();

// Java 7+ Diamond operator
Map<String, List<String>> newStyle = new HashMap<>();
```

### 4. Defensive Copying for Thread Safety

```java
public class TestConfigManager {
    private final Map<String, String> config = new HashMap<>();

    public Map<String, String> getConfig() {
        return new HashMap<>(config); // Return defensive copy
    }

    public void setConfig(Map<String, String> newConfig) {
        this.config.clear();
        this.config.putAll(newConfig); // Don't expose internal reference
    }
}
```

### 5. Use Appropriate Methods for Bulk Operations

```java
// Efficient bulk operations
List<String> testIds = Arrays.asList("test1", "test2", "test3");
Set<String> uniqueIds = new HashSet<>(testIds); // Bulk constructor

// Add multiple elements
Collection<String> moreTests = Arrays.asList("test4", "test5");
uniqueIds.addAll(moreTests);

// Remove multiple elements
Collection<String> testsToRemove = Arrays.asList("test1", "test2");
uniqueIds.removeAll(testsToRemove);
```

### 6. Iterator vs Enhanced For Loop

```java
List<String> tests = new ArrayList<>();

// Enhanced for loop (preferred for read-only)
for (String test : tests) {
    System.out.println(test);
}

// Iterator (required for safe removal)
Iterator<String> iterator = tests.iterator();
while (iterator.hasNext()) {
    String test = iterator.next();
    if (test.startsWith("obsolete")) {
        iterator.remove(); // Safe removal during iteration
    }
}
```

### 7. Null Safety

```java
// Check for null before operations
if (testList != null && !testList.isEmpty()) {
    processTests(testList);
}

// Use Optional for better null handling
Optional<String> config = Optional.ofNullable(getConfigValue("key"));
config.ifPresent(value -> processConfig(value));

// Default values
String browser = configMap.getOrDefault("browser", "chrome");
```

### 8. Memory Efficient Operations

```java
// Trim ArrayList to reduce memory usage
ArrayList<String> tests = new ArrayList<>();
// ... populate list
tests.trimToSize(); // Reduce capacity to actual size

// Clear collections when done
testResults.clear(); // Help GC
```

## Common Pitfalls to Avoid

### 1. Modifying Collection During Iteration
```java
// ❌ Wrong - ConcurrentModificationException
List<String> tests = new ArrayList<>();
for (String test : tests) {
    if (condition) {
        tests.remove(test); // Throws exception
    }
}

// ✅ Correct - Use iterator
Iterator<String> iterator = tests.iterator();
while (iterator.hasNext()) {
    String test = iterator.next();
    if (condition) {
        iterator.remove(); // Safe removal
    }
}
```

### 2. Using == Instead of equals()
```java
// ❌ Wrong
String test1 = "test";
String test2 = new String("test");
if (test1 == test2) { // false - different objects
    // This won't execute
}

// ✅ Correct
if (test1.equals(test2)) { // true - same content
    // This will execute
}
```

### 3. Not Overriding equals() and hashCode()
```java
public class TestCase {
    private String name;
    private int priority;

    // ✅ Must override both for proper collection behavior
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        TestCase testCase = (TestCase) obj;
        return priority == testCase.priority && 
               Objects.equals(name, testCase.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, priority);
    }
}
```

### 4. Wrong Collection Choice
```java
// ❌ Wrong - LinkedList for frequent random access
List<String> tests = new LinkedList<>();
for (int i = 0; i < 1000; i++) {
    String test = tests.get(i); // O(n) operation - very slow!
}

// ✅ Correct - ArrayList for frequent random access  
List<String> tests = new ArrayList<>();
for (int i = 0; i < 1000; i++) {
    String test = tests.get(i); // O(1) operation - fast!
}
```