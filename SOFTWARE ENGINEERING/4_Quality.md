
## 1. Software Quality Assurance (SQA)

**Definition:** Software Quality Assurance (SQA) is a planned and systematic set of activities used to provide confidence that software development processes and products meet specified quality requirements.

In simple words, SQA focuses on preventing defects and ensuring that appropriate processes are followed throughout software development.

### Objectives of SQA

- Ensure compliance with software requirements and standards.
    
- Prevent defects by improving development processes.
    
- Improve software reliability, maintainability, and overall quality.
    
- Ensure appropriate documentation and reviews.
    
- Monitor whether established processes are being followed.
    
- Promote continuous process improvement.
    

### SQA Activities

|Activity|Purpose|
|---|---|
|Quality planning|Define quality objectives, standards, and responsibilities.|
|Process audits|Check compliance with established procedures.|
|Reviews and inspections|Identify defects in requirements, design, and code.|
|Standards enforcement|Ensure agreed coding and documentation practices are followed.|
|Quality metrics|Measure defects, test coverage, and other quality indicators.|
|Process improvement|Identify recurring problems and improve development practices.|

### Example

A company develops a banking application. Its SQA team establishes coding standards, requires design reviews, audits development procedures, and monitors defect trends.

The goal is not merely to find bugs at the end; it is to prevent defects throughout development.

### SQA vs. Software Quality Control (SQC)

|SQA|SQC|
|---|---|
|Primarily process-oriented|Primarily product-oriented|
|Aims to prevent defects|Aims to identify defects|
|Includes process audits and standards|Includes product testing and inspections|
|Evaluates how software is developed|Evaluates whether software meets requirements|

**Exam tip:** SQA is associated with quality assurance and defect prevention. Testing is an important quality-control activity, although it can also contribute to broader quality assurance.

## 2. Verification

**Definition:** Verification determines whether software work products meet specified requirements and design specifications.

It answers the question:

**“Are we building the product right?”**

Verification checks whether software is being developed according to its specifications. It can take place before executable software is available.

### Verification Activities

- Requirement reviews
    
- Design reviews
    
- Code reviews
    
- Walkthroughs
    
- Formal inspections
    
- Static analysis
    

These activities can identify mistakes without executing the program.

### Example

Suppose the requirement states that a password must contain at least eight characters. During a design or code review, the team checks whether the specification and implementation logic correctly enforce that rule.

The team is checking conformance to the stated requirement.

### Static Testing

Verification commonly uses static testing, which examines work products without executing the software.

Examples include:

- Reviewing source code.
    
- Checking requirements documents.
    
- Using static-analysis tools.
    

**Exam keyword:** Specifications, reviews, inspections, and static testing.

## 3. Validation

**Definition:** Validation determines whether the developed software satisfies user needs and its intended purpose.

It answers the question:

**“Are we building the right product?”**

Validation checks whether the resulting software actually solves the problem it was intended to solve.

### Validation Activities

- Executing test cases
    
- Functional testing
    
- System testing
    
- User Acceptance Testing (UAT)
    
- Evaluating software against real user workflows
    
- Collecting feedback from intended users
    

### Example

A college requests a student management system. The system passes its technical tests, but college staff discover that its reports do not provide the information they need.

Validation helps determine whether the software meets the actual needs of the college, not merely whether it follows its written technical specification.

### Dynamic Testing

Validation commonly involves dynamic testing, in which software is executed with selected inputs and its behavior is evaluated.

Examples include functional testing, system testing, and acceptance testing.

**Important distinction:** Verification and validation are broader activities. They are not defined exclusively by static and dynamic testing, respectively.

**Exam keyword:** User needs, intended purpose, and suitability.

## 4. Verification vs. Validation — Most Important Comparison

|Basis|Verification|Validation|
|---|---|---|
|Main question|Are we building the product right?|Are we building the right product?|
|Focus|Conformance to specifications|Satisfaction of user needs|
|Typical approach|Reviews, inspections, static analysis|Executing software and evaluating its behavior|
|Execution required?|Not necessarily|Commonly involves execution|
|Examples|Requirement review, design review, code inspection|Functional testing, system testing, UAT|
|Objective|Detect errors in work products|Determine whether the intended product is suitable|

### Easy Memory Trick

- **Verification =** Product conforms to specifications.
    
- **Validation =** Product meets user needs.
    

Remember that both are necessary. A product can conform perfectly to a specification yet still fail to meet the user's real needs if the specification itself was incomplete or incorrect.

## 5. How SQA, Verification, and Validation Work Together

### Software Quality Assurance (SQA)

Establishes and improves quality processes throughout development.

### Verification

Checks whether the work conforms to specifications.

### Validation

Checks whether the software meets user needs.

SQA provides the broader quality framework, while verification and validation are complementary activities within software quality management.

## 6. Last-Minute Revision

- **SQA:** Process-oriented; focuses on preventing defects and improving quality processes.
    
- **SQC:** Product-oriented; focuses on evaluating software quality and identifying defects.
    
- **Verification:** “Are we building the product right?”
    
- **Validation:** “Are we building the right product?”
    
- **Static testing:** Examines work products without executing the software.
    
- **Dynamic testing:** Executes software and evaluates its behavior.
    
- **Verification examples:** Reviews, inspections, and static analysis.
    
- **Validation examples:** Functional testing, system testing, and UAT.
    

**DSSSB exam priority:** Learn the definitions, the verification-versus-validation comparison, SQA-versus-SQC differences, and the examples of static and dynamic testing.