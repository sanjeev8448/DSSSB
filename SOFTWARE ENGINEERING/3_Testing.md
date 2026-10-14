# SOFTWARE TESTING — DSSSB TGT COMPUTER SCIENCE

Software testing is the process of evaluating software to identify defects and determine whether it meets specified requirements.

For DSSSB preparation, understand two classifications:

- **Testing techniques:** Black-box testing and white-box testing.
    
- **Testing levels:** Unit, integration, system, and acceptance testing.
    

These classifications are related but different. Black-box and white-box describe _how_ software is tested, while unit, integration, system, and acceptance describe the _scope or level_ of testing.

## 1. Black-Box Testing

**Definition:** Black-box testing tests software functionality by providing inputs and checking outputs without requiring knowledge of the internal source code.

### Example: Login page

Suppose a login page requires a password of at least eight characters.

A tester tries:

- A valid username and password — login should succeed.
    
- An incorrect password — login should be rejected.
    
- An empty password — an appropriate error should appear.
    

The tester checks the results without inspecting the internal code.

### Common black-box techniques

- **Equivalence partitioning:** Divides inputs into groups expected to behave similarly and tests representative values.
    
- **Boundary value analysis:** Tests values at and around the limits.
    
- **Decision table testing:** Tests combinations of conditions and their expected outcomes.
    
- **State transition testing:** Checks behavior when a system moves between states.
    

**Boundary value analysis example:** If valid ages are 18–60, useful test values include 17, 18, 19, 59, 60, and 61.

### Advantages

- Does not require access to source code.
    
- Tests software from the user's perspective.
    
- Can identify missing functionality and incorrect outputs.
    

### Limitations

- Does not directly reveal which internal code path caused a failure.
    
- Some internal logic may remain untested if test cases are incomplete.
    

**Exam keyword:** Inputs and outputs; internal implementation is not examined.

## 2. White-Box Testing

**Definition:** White-box testing examines internal program logic, structure, control flow, and execution paths.

It is also known as **structural testing** or **clear-box testing**.

### Example

```
def check_age(age):
    if age >= 18:
        return "Eligible"
    else:
        return "Not eligible"
```

A white-box tester examines the condition `age >= 18` and checks whether both branches execute.

- Input `20` executes the `if` branch.
    
- Input `16` executes the `else` branch.
    

### Common white-box techniques

- **Statement coverage:** Measures whether executable statements have been executed.
    
- **Branch coverage:** Measures whether decision outcomes, such as true and false branches, have been exercised.
    
- **Path testing:** Tests execution paths through the code.
    
- **Condition coverage:** Checks whether individual Boolean conditions evaluate to both true and false, where applicable.
    

### Statement coverage vs. branch coverage

|Statement coverage|Branch coverage|
|---|---|
|Focuses on executable statements.|Focuses on decision outcomes.|
|A statement can execute without every branch being tested.|Requires each applicable branch outcome to be exercised.|
|Does not guarantee branch coverage.|Usually requires more comprehensive tests.|

For the function above, testing only `age = 20` does not cover the `else` branch. Testing both `20` and `16` covers both branches.

### Advantages

- Helps identify logic errors and untested branches.
    
- Supports measurement of code coverage.
    
- Can expose defects hidden within complex conditions.
    

### Limitations

- Usually requires source-code access and programming knowledge.
    
- High code coverage does not guarantee defect-free software.
    
- Exhaustive path testing can be impractical for complex programs.
    

**Exam keyword:** Internal code, control flow, statements, and branches.

## 3. Unit Testing

**Definition:** Unit testing checks an individual, smallest testable component of software, such as a function, method, or module.

It is commonly performed by developers during implementation.

### Example

```
def add(a, b):
    return a + b

assert add(2, 3) == 5
assert add(-1, 1) == 0
```

These tests check the `add()` function independently.

### Important points

- Focuses on individual components.
    
- Often automated using testing frameworks.
    
- Helps locate defects close to their source.
    
- May use stubs or drivers when other components are unavailable.
    

**Stub:** A simplified component that simulates a called component.

**Driver:** A test component that calls the component being tested.

**Exam keyword:** Individual function, module, or component.

## 4. Integration Testing

**Definition:** Integration testing checks whether two or more combined modules interact and communicate correctly.

Individual modules may pass unit tests but still fail when connected.

### Example: Online shopping application

1. The cart module prepares an order.
    
2. The payment module processes the payment.
    
3. The order module records the purchase.
    

Integration testing checks whether data flows correctly between these modules.

### Integration testing approaches

**A. Top-down integration**

- Testing starts with higher-level modules.
    
- Lower-level modules are gradually integrated.
    
- **Stubs** may be used for modules that are not yet available.
    

**B. Bottom-up integration**

- Testing starts with lower-level modules.
    
- Higher-level modules are gradually integrated.
    
- **Drivers** may be used to call the modules being tested.
    

**C. Big-bang integration**

- Many or all modules are combined before integration testing begins.
    
- Failures can be difficult to isolate because many components are integrated at once.
    

**Exam trap:** Stubs are commonly associated with top-down integration; drivers are commonly associated with bottom-up integration.

**Exam keyword:** Interaction between modules.

## 5. System Testing

**Definition:** System testing evaluates the complete, integrated software system against its specified requirements.

It tests the system as a whole rather than individual functions or only connections between modules.

### Example: College management application

System testing may verify that:

- Students can log in.
    
- Teachers can enter marks.
    
- Attendance is recorded.
    
- Fees are calculated correctly.
    
- Reports are generated.
    
- Unauthorized users cannot access restricted features.
    

### Types of system testing

- **Functional testing:** Checks whether required features work correctly.
    
- **Performance testing:** Measures response time, throughput, and resource usage.
    
- **Security testing:** Evaluates security controls and vulnerabilities.
    
- **Recovery testing:** Checks recovery after failures.
    
- **Usability testing:** Evaluates ease of use.
    

System testing may include both functional and non-functional testing, depending on the test plan.

**Exam keyword:** Complete integrated system.

## 6. Acceptance Testing

**Definition:** Acceptance testing determines whether software meets user, customer, or business requirements and is ready for acceptance or release.

It is often performed by customers, end users, or business representatives, although other authorized team members may participate.

### Example: College management system

A college receives a student management system. Its staff check whether the application correctly handles admissions, attendance, marks, fees, and reports according to the agreed requirements.

If the acceptance criteria are met, the college may accept the system.

### Types of acceptance testing

- **User Acceptance Testing (UAT):** Checks whether the system meets users' operational and business needs.
    
- **Alpha testing:** Evaluation in a controlled environment, commonly involving the developer's organization.
    
- **Beta testing:** Evaluation by selected external users in realistic conditions before a wider release.
    

**Exam keyword:** Customer requirements and readiness for acceptance.

## 7. Comparison of All Six Testing Concepts

|Concept|What is tested?|Main focus|
|---|---|---|
|Black-box|Software behavior without inspecting internal code|Inputs and outputs|
|White-box|Internal program structure|Statements, branches, and paths|
|Unit testing|Individual component|Component correctness|
|Integration testing|Combined modules|Interfaces and interactions|
|System testing|Complete integrated system|Overall requirements|
|Acceptance testing|Software against user/business acceptance criteria|Whether the system is acceptable|

**Important:** Black-box and white-box techniques can be used at different testing levels. For example, unit testing can include both black-box and white-box tests.

## 8. Commonly Confused Concepts

|Pair|Key difference|
|---|---|
|Unit vs. integration|Individual component vs. interactions between components|
|Integration vs. system|Connections between modules vs. complete system|
|System vs. acceptance|Overall system conformance vs. user/business acceptance|
|Black-box vs. white-box|External behavior vs. internal structure|
|Stub vs. driver|Simulates a called component vs. calls the component under test|
|Alpha vs. beta|Controlled evaluation vs. selected external users in realistic conditions|
|Statement vs. branch coverage|Executed statements vs. exercised decision outcomes|

### Simplified testing sequence

[  
\boxed{\text{Unit}\rightarrow\text{Integration}\rightarrow\text{System}\rightarrow\text{Acceptance}}  
]

This is a useful exam convention, although real projects may organize testing differently.

## 9. Last-Minute Revision

- **Black-box:** Tests functionality without examining internal code.
    
- **White-box:** Tests internal structure and logic.
    
- **Unit:** Tests an individual component.
    
- **Integration:** Tests interaction between modules.
    
- **System:** Tests the complete integrated application.
    
- **Acceptance:** Checks whether the software meets customer or business acceptance criteria.
    
- **Top-down integration:** Commonly uses stubs.
    
- **Bottom-up integration:** Commonly uses drivers.
    
- **Statement coverage:** Checks executed statements.
    
- **Branch coverage:** Checks decision outcomes.
    
- **Equivalence partitioning:** Groups similar inputs.
    
- **Boundary value analysis:** Tests values near input limits.
    

**Recommended next step:** Practice MCQs that ask you to identify the testing technique or level from a short scenario. DSSSB-style questions often test the distinction between similar concepts.