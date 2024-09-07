# Software Testing and Quality Assurance

## Course Overview
This course delves into advanced principles and practices of software testing and quality assurance. It covers in-depth testing techniques, tools, and quality assurance practices essential for ensuring high-quality software systems.

## Course Content

### **1. Introduction to Software Testing**

#### **Testing Fundamentals**
- **Unit Testing**: Essential for testing individual components in isolation.
- **Integration Testing**: Focuses on verifying that combined components function as expected.

**Python Example (Advanced Unit Testing with `pytest`):**
```python
# advanced_tests.py
import pytest

def divide(a, b):
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

def test_divide():
    assert divide(6, 3) == 2
    with pytest.raises(ValueError):
        divide(6, 0)
```

**Java Example (Advanced Unit Testing with JUnit and Mockito):**
```java
import org.junit.Test;
import org.mockito.Mockito;

import static org.junit.Assert.assertEquals;
import static org.mockito.Mockito.*;

public class CalculatorTest {
    public int divide(int a, int b) {
        if (b == 0) throw new IllegalArgumentException("Cannot divide by zero");
        return a / b;
    }

    @Test
    public void testDivide() {
        Calculator calculator = new Calculator();
        assertEquals(2, calculator.divide(6, 3));
        try {
            calculator.divide(6, 0);
        } catch (IllegalArgumentException e) {
            assertEquals("Cannot divide by zero", e.getMessage());
        }
    }
}
```

#### **Testing Lifecycle**
- **Test Planning**: Create a detailed strategy that includes objectives, scope, and resource allocation.
- **Test Design**: Develop and review test cases for comprehensive coverage.
- **Test Execution**: Implement and execute tests, documenting the results and issues found.
- **Test Closure**: Analyze test results, report on issues, and refine testing processes.

**Practical Exercise:**
- **Create a Detailed Test Plan**: For a new feature, including objectives, scenarios, cases, and metrics.

### **2. Testing Techniques**

#### **Black-box Testing**
- **Definition**: Testing based on requirements and functionality without considering internal code structure.

**Python Example (Black-box Testing with Property-Based Testing using `hypothesis`):**
```python
# black_box_test.py
from hypothesis import given, strategies as st

def add(a, b):
    return a + b

@given(st.integers(), st.integers())
def test_add(a, b):
    assert add(a, b) == a + b
```

**Java Example (Black-box Testing with Randomized Testing using JUnit and QuickCheck):**
```java
import org.junit.Test;
import org.quicktheories.QuickTheory;

public class MathOperationsTest {
    @Test
    public void testAdd() {
        QuickTheory.qt()
            .forAll(arbIntegers(), arbIntegers())
            .check((a, b) -> add(a, b) == a + b);
    }
}
```

#### **White-box Testing**
- **Definition**: Testing based on knowledge of the internal code structure and logic.

**Python Example (White-box Testing with Code Coverage and `coverage`):**
```python
# code.py
def is_positive(number):
    return number > 0

# test_code.py
import coverage

cov = coverage.Coverage()
cov.start()

# Run your tests
import test_code

cov.stop()
cov.save()
cov.report()
```

**Java Example (White-box Testing with Code Coverage using JaCoCo):**
```xml
<!-- pom.xml -->
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.7</version>
    <executions>
        <execution>
            <id>prepare-agent</id>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>verify</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

#### **Regression Testing and Performance Testing**
- **Regression Testing**: Use automated regression test suites to ensure no new defects are introduced.
- **Performance Testing**: Includes load testing, stress testing, and benchmarking.

**Python Example (Performance Testing with `locust`):**
```python
# locustfile.py
from locust import HttpUser, task

class WebsiteUser(HttpUser):
    @task
    def index(self):
        self.client.get("/")
```

**Java Example (Performance Testing with JMH):**
```java
import org.openjdk.jmh.annotations.Benchmark;
import org.openjdk.jmh.annotations.State;
import org.openjdk.jmh.annotations.Scope;

@State(Scope.Thread)
public class PerformanceTest {
    @Benchmark
    public void testSort() {
        List<Integer> list = Arrays.asList(3, 1, 4, 1, 5, 9);
        Collections.sort(list);
    }
}
```

**Practical Exercise:**
- **Implement a Regression Test Suite**: For a medium-sized project.
- **Conduct Performance Testing**: Analyze the performance impact of a feature or service.

### **3. Automated Testing**

#### **Test Frameworks and Tools**

- **JUnit**: Essential for automated unit testing in Java.
- **Selenium**: Used for automated browser testing.

**Python Example (Advanced Automated Testing with `pytest` and `selenium`):**
```python
# test_selenium.py
from selenium import webdriver

def test_google_search():
    driver = webdriver.Chrome()
    driver.get("https://www.google.com")
    assert "Google" in driver.title
    driver.quit()
```

**Java Example (Advanced Automated Testing with Selenium and TestNG):**
```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.0.0</version>
</dependency>
<dependency>
    <groupId>org.testng</groupId>
    <artifactId>testng</artifactId>
    <version>7.4.0</version>
</dependency>
```

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.Test;

public class SeleniumTest {
    @Test
    public void testGoogleTitle() {
        WebDriver driver = new ChromeDriver();
        driver.get("https://www.google.com");
        assert driver.getTitle().contains("Google");
        driver.quit();
    }
}
```

#### **Continuous Integration and Delivery (CI/CD)**
- **CI/CD Pipelines**: Automate the build, test, and deployment processes to ensure continuous delivery of software.

**Python Example (CI/CD with GitHub Actions):**
```yaml
# .github/workflows/python-app.yml
name: Python application

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Run tests
      run: |
        pytest
```

**Java Example (CI/CD with Jenkins and Maven):**
```groovy
// Jenkinsfile
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn deploy'
            }
        }
    }
}
```

**Practical Exercise:**
- **Build a CI/CD Pipeline**: Implement a pipeline that includes testing and deployment automation.

### **4. Quality Assurance Practices**

#### **Code Quality Metrics**
- **Code Complexity**: Measure using metrics such as cyclomatic complexity, which indicates the number of independent paths through the code.

**Python Example (Code Complexity with `radon`):**
```bash
# Install radon
pip install radon

# Measure cyclomatic complexity
radon cc my_code.py -a
```

**Java Example (Code Complexity with SonarQube):**
```xml
<!-- Add to pom.xml -->
<plugin>
    <groupId>org.sonarsource.scanner.maven</groupId>
    <artifactId>sonar-maven-plugin</artifactId>
    <version>3.9.0.2155</version>
</plugin>
```

#### **Static and Dynamic Analysis**
- **Static Analysis**: Tools that analyze code without executing it.
- **Dynamic Analysis**: Tools that analyze code during execution.

**Python Example (Static Analysis with `flake8`):**
```bash
# Install flake8
pip install flake8

# Run flake8 on a Python file
flake8 my_code.py
```

**Java Example (Static Analysis with FindBugs):**
```xml
<!-- Add to pom.xml -->
<plugin>
    <groupId>com.google.code.findbugs</groupId>
    <artifactId>findbugs-maven-plugin</artifact

Id>
    <version>3.0.5</version>
    <executions>
        <execution>
            <goals>
                <goal>check</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

#### **Bug Tracking and Management**
- **Bug Tracking Systems**: Use tools like Jira or Bugzilla to manage and prioritize bugs.

**Practical Exercise:**
- **Setup a Bug Tracking System**: Create and manage bugs in a project using a bug tracking system.

### **5. Advanced Topics in Testing**

#### **Security Testing**
- **Vulnerability Scanning**: Automate security vulnerability assessments in applications.

**Python Example (Security Testing with `bandit`):**
```bash
# Install bandit
pip install bandit

# Run bandit on a Python file
bandit -r my_code.py
```

**Java Example (Security Testing with OWASP ZAP):**
```bash
# Run OWASP ZAP
zap.sh
# Use OWASP ZAP to scan a web application
```

#### **Usability Testing**
- **User Experience (UX)**: Evaluate and improve user experience based on real user feedback.

**Practical Exercise:**
- **Conduct Usability Testing**: Perform usability testing on a web application and analyze results.

#### **Test-Driven Development (TDD) and Behavior-Driven Development (BDD)**
- **TDD**: Write tests before implementing features. Follow Red-Green-Refactor cycle.
- **BDD**: Write scenarios in natural language that describe the behavior of the application.

**Python Example (TDD with `pytest`):**
```python
# test_calculator.py
def test_addition():
    assert add(1, 2) == 3

def test_subtraction():
    assert subtract(5, 3) == 2
```

**Java Example (BDD with Cucumber):**
```gherkin
# features/calculator.feature
Feature: Calculator
  Scenario: Addition
    Given I have two numbers 5 and 3
    When I add them
    Then the result should be 8
```

**Practical Exercise:**
- **Implement TDD/BDD**: Write and execute test cases using TDD or BDD methodologies for a given feature.

## **Assessment**

- **Weekly Testing Assignments**: Implement and report on various testing techniques and tools.
- **Automated Testing Project**: Create a project that includes automated tests and integrates with a CI/CD pipeline.
- **Final Exam**: Assess understanding of testing principles, techniques, and tools.

## **Resources**

- **"Software Testing: A Craftsman's Approach" by Paul C. Jorgensen**: Comprehensive coverage of testing principles and techniques.
- **"Continuous Delivery: Reliable Software Releases through Build, Test, and Deployment Automation" by Jez Humble, David Farley**: Essential reading for understanding CI/CD practices.
