## 1. Software characteristics

### What is software engineering?

Software engineering is the systematic, disciplined, and measurable approach to developing, operating, testing, and maintaining software.

Software is a collection of programs, procedures, and related data or documentation used to perform tasks on a computer.

Examples: Operating systems, banking applications, web browsers, payroll systems, and mobile applications.

### Characteristics of software

|Characteristic|Explanation|
|---|---|
|Intangible|Software is logical rather than a physical product.|
|Developed, not manufactured|Most cost is incurred in design and development; copying software costs comparatively little.|
|Does not physically wear out|Software does not wear out like hardware, although defects and obsolescence can make it unreliable or outdated.|
|Complex|Large systems can contain many interacting components and dependencies.|
|Changeable|Software can be modified to meet new requirements.|
|Maintainable|Good design and documentation make corrections and improvements easier.|
|Mostly custom-built, sometimes reused|Software may be developed specifically for a need or assembled using reusable components.|
|Quality-dependent|Reliability, security, usability, efficiency, and maintainability affect its quality.|

Exam trap: Hardware can physically wear out. Software does not physically wear out, but repeated changes can introduce new defects and increase complexity.

### Software quality attributes

- Correctness: Produces the expected results.
    
- Reliability: Performs consistently without failure under stated conditions.
    
- Efficiency: Uses resources such as CPU time and memory effectively.
    
- Usability: Is easy to learn and use.
    
- Maintainability: Is easy to correct, modify, or improve.
    
- Portability: Can be moved to another platform with limited effort.
    
- Security: Protects data and resources from unauthorized access.
    
- Reusability: Components can be used in multiple systems.
    

## 2. SDLC — Software Development Life Cycle

The SDLC is a structured process used to develop and maintain software, from identifying a need to operating and improving the finished system.

1. Planning and feasibility

2. Requirement analysis

3. System design

4. Implementation / coding

5. Testing

6. Deployment

7. Maintenance

This is a common simplified sequence. Real development models may revisit earlier phases or overlap activities.

### SDLC phases and their outputs

|Phase|Main activity|Typical output|
|---|---|---|
|Planning|Define goals, scope, cost, time, and resources|Project plan|
|Feasibility study|Assess whether the project is practical|Feasibility report|
|Requirement analysis|Determine what users need|SRS document|
|Design|Decide how the system will work|Architecture and design specifications|
|Implementation|Write and integrate code|Source code and executable components|
|Testing|Find defects and verify requirements|Test cases, defect reports, test results|
|Deployment|Release software for actual use|Installed or released software|
|Maintenance|Fix, adapt, and improve software|Updated versions and patches|

### Feasibility study

A feasibility study checks whether a project is viable.

Remember TELOS:

- T — Technical: Is the required technology and expertise available?
    
- E — Economic: Are the benefits worth the cost?
    
- L — Legal: Does the project comply with laws and regulations?
    
- O — Operational: Will the system work within the organization and be accepted by users?
    
- S — Schedule: Can it be completed within the available time?
    

Example: Before developing a college management system, the team checks the budget, technical skills, legal requirements for student data, staff readiness, and deadline.

### Common SDLC models

![Top 11 Software Development Models in 2025 Explained | Binariks](https://images.openai.com/static-rsc-4/cMs2wN98TkBVqITbHcAVXVOVRqH0HKrp4oC--L1OHsdq9DhBpYcR01Vko9-P0IB3TsNokIRdbmDNHzSVOwoVvsDV5wl6QHz8zHoeGZHmkRWOur2rCIanjB5hyjLEEnrsfxcXLgg75_u8Aji4T1xctkByvBol5NdBy33BGO0LJSM?purpose=inline)

Waterfall model

Phases are generally performed sequentially. It works best when requirements are reasonably stable. Late changes can be expensive.

![SDLC methodologies — which one to choose for your project?](https://images.openai.com/static-rsc-4/7ssLXFdL7xeFqprqqJI3Pl7SYaZcBjTIt261LWMt4s0h0qu0MmCCqYPJKOvLUlE9dtKuXWicPJCbnksMTBc0bMVWpzDfZ6AAqmL6266S11HSDRDHwzSsmtcw6A9dHKGxxlyZR7TOWW96DZq248mtkvZo2vI5_zEXWnEP1qFA4os?purpose=inline)

Iterative and incremental models

The system is developed and improved through repeated cycles or delivered in smaller functional increments.

![Software Development Life Cycle Models Explained | Softkit](https://images.openai.com/static-rsc-4/4Xh0YKgKMPIkstpd9IF7KZ2G-ysN3ZdncgpAcsCH3p7vfx-vlyV5ps7qb1GYbNjtNtGV3f8_3mayNR-FCGTw-JLH-AwucOH-SG06UBeqWdV3xICwgb1FnmkcMd_N1-D3C9HKcyEK45c34_dw1zZzmfghyinXeinrBs-3wN2ZGw4?purpose=inline)

Spiral model

Development proceeds through repeated cycles with explicit risk analysis. It is useful for large, complex, high-risk projects.

![What is iteration? - CircleCI](https://images.openai.com/static-rsc-4/Fwyckt-hU_bkQ72Jwr06ZiHkf-3MrEkmt3T-2XUsSgcv8SK1Tc-pZZScWOoX7Vsaag0uPufOZLnsrsYc7j6XpKGWna7bk77HQVZ6yG_hm3BWJIb-B0NYhcCnE5RI7gS_48XxOIjEmwfS8tvgsTXXcVp9JcFjk5WjXUpvs2dcH-M?purpose=inline)

Agile model

Software is developed in short iterations with frequent feedback and adaptation to changing requirements.

Remember: Waterfall = sequential; Spiral = risk-focused; Agile = iterative and feedback-driven.

## 3. Requirement analysis

Requirement analysis identifies, studies, documents, and validates what users expect from a software system.

### Types of requirements

A. Functional requirements

Describe what the system must do.

Examples:

- A user can log in using a username and password.
    
- The system calculates student marks.
    
- An ATM allows cash withdrawal.
    

B. Non-functional requirements

Describe how well the system must operate or the constraints under which it operates.

Examples:

- The page should load within two seconds under specified conditions.
    
- Only authorized users may access confidential records.
    
- The system should support 10,000 concurrent users.
    

### Functional vs non-functional requirements

|Functional|Non-functional|
|---|---|
|Describes system behavior|Describes quality or constraints|
|Login, payment, search|Performance, security, usability|
|Often expressed as features or use cases|Often expressed as measurable quality targets|

### SRS — Software Requirements Specification

An SRS is a document that describes the software requirements clearly and systematically.

Typical contents include:

- Functional and non-functional requirements
    
- System interfaces
    
- Constraints and assumptions
    
- External interfaces
    
- Performance and security requirements
    
- Acceptance criteria
    

A good SRS should be clear, complete, consistent, verifiable, and traceable.

### Requirement gathering techniques

- Interview: Direct discussion with stakeholders.
    
- Questionnaire: Collects information from many people.
    
- Observation: Studies how users perform existing tasks.
    
- Document analysis: Examines existing forms, policies, and systems.
    
- Prototyping: Creates an early model to clarify requirements.
    
- Workshops: Multiple stakeholders discuss and agree on requirements.
    

Exam point: The SRS primarily describes what the system should do, not the detailed internal design of how it will be implemented.

## 4. Software design

Software design transforms requirements into a blueprint for implementation.

### Levels of design

|Design level|Meaning|Example|
|---|---|---|
|High-level design (HLD)|Overall architecture and major components|Frontend, backend, database, API structure|
|Low-level design (LLD)|Internal details of modules and components|Class methods, algorithms, database operations|

### Important design concepts

- Modularity: Divide the system into smaller, manageable modules.
    
- Abstraction: Show essential features while hiding unnecessary implementation details.
    
- Encapsulation: Bundle data and related operations together, controlling access to internal state.
    
- Cohesion: How closely related the responsibilities within one module are. Higher cohesion is generally desirable.
    
- Coupling: How strongly one module depends on another. Lower coupling is generally desirable.
    
- Information hiding: Hide internal implementation details behind well-defined interfaces.
    

Memory trick: Good software design generally aims for high cohesion and low coupling.

### Architectural design examples

- Layered architecture: Separates responsibilities into layers, such as presentation, business logic, and data access.
    
- Client-server architecture: Clients request services from servers.
    
- MVC: Separates Model, View, and Controller responsibilities.
    

## 5. Implementation

Implementation is the phase in which the design is converted into executable software through coding and integration.

### Main activities

1. Select programming languages, tools, and frameworks.
    
2. Write code according to the design and requirements.
    
3. Follow coding standards and naming conventions.
    
4. Perform code reviews and static analysis where appropriate.
    
5. Test individual modules.
    
6. Integrate modules into the complete system.
    
7. Maintain source code and version history.
    

### Coding errors

|Error type|Meaning|Example|
|---|---|---|
|Syntax error|Violates language grammar|Missing `:` after a Python `if` statement|
|Runtime error|Occurs during execution|Division by zero|
|Logical error|Program runs but produces an incorrect result|Using addition instead of multiplication|

Example of a logical error:

```
length = 5width = 4area = length + width  # Incorrect
```

The program executes, but the correct rectangle area is `length * width`, which is `20`, not `9`.

Exam point: Coding is only one part of software development. Good implementation also involves reviews, integration, documentation, and verification.

## 6. Software testing

Software testing evaluates software to identify defects and check whether it satisfies specified requirements.

### Testing levels

1. Unit testing

Tests an individual function, method, or module.

Example: Check whether a function correctly calculates GST.

2. Integration testing

Tests interactions between combined modules.

Example: Verify that an online store correctly passes an order from the checkout module to the payment module.

3. System testing

Tests the complete integrated system against its requirements.

Example: Test the entire online shopping application.

4. Acceptance testing

Checks whether the software meets user or business acceptance criteria.

Example: College staff verify that the student management system meets their needs before accepting it.

A common sequence is Unit → Integration → System → Acceptance. Some projects use different workflows.

### Black-box vs white-box testing

|Black-box testing|White-box testing|
|---|---|
|Focuses on inputs and outputs|Examines internal code and logic|
|Does not require knowledge of internal implementation|Requires knowledge of internal structure|
|Examples: functional and many acceptance tests|Examples: statement and branch coverage tests|

Grey-box testing combines aspects of both, using partial knowledge of internal workings.

### Other important testing types

- Smoke testing: A basic check that the main functions work after a build.
    
- Sanity testing: A focused check of a specific change or area.
    
- Regression testing: Checks that changes have not broken existing functionality.
    
- Retesting: Runs a failed test again after a defect is fixed.
    
- Performance testing: Evaluates speed, responsiveness, and stability.
    
- Load testing: Tests behavior under expected or specified workloads.
    
- Stress testing: Tests beyond normal operating conditions to identify limits or failure behavior.
    
- Security testing: Checks for vulnerabilities and security weaknesses.
    
- Usability testing: Evaluates ease of use.
    

### Verification vs validation

|Verification|Validation|
|---|---|
|Are we building the product right?|Are we building the right product?|
|Checks conformance to specifications|Checks whether user needs are met|
|Includes reviews and inspections|Often includes executing software and user evaluation|

### Alpha vs beta testing

- Alpha testing: Early evaluation in a controlled environment, often by the developer's organization.
    
- Beta testing: Evaluation by selected external users or real-world users before wider release.
    

### Important testing principle

Testing can reveal the presence of defects, but it cannot prove that software is completely defect-free.

## 7. Software maintenance

Software maintenance refers to modifying software after delivery to correct defects, adapt to changes, or improve the system.

### Four types of maintenance

|Type|Purpose|Example|
|---|---|---|
|Corrective|Fix defects|Correct an incorrect tax calculation|
|Adaptive|Adjust to a changed environment|Update software to support a new operating system|
|Perfective|Improve performance, usability, or functionality|Add a requested report or speed up a slow query|
|Preventive|Reduce future problems and improve maintainability|Refactor complex code to make future defects less likely|

Memory trick: CAPP

- Corrective = Correct a defect
    
- Adaptive = Adapt to change
    
- Perfective = Perfect or improve the product
    
- Preventive = Prevent future problems
    

### Maintenance vs development

Development creates and initially delivers software. Maintenance takes place after delivery to keep it useful, correct, compatible, and maintainable.

Maintenance can sometimes be expensive because existing software may have complex dependencies, limited documentation, or outdated technology.

## Quick revision sheet

| Topic                      | Must remember                                                                          |
| -------------------------- | -------------------------------------------------------------------------------------- |
| Software characteristics   | Intangible; developed rather than manufactured; does not physically wear out           |
| SDLC                       | Planning → requirements → design → implementation → testing → deployment → maintenance |
| Feasibility                | TELOS                                                                                  |
| SRS                        | Documents software requirements                                                        |
| Functional requirement     | What the system does                                                                   |
| Non-functional requirement | Quality attribute or constraint                                                        |
| Good design                | High cohesion, low coupling                                                            |
| Testing levels             | Unit → integration → system → acceptance                                               |
| Black-box testing          | Inputs and outputs                                                                     |
| White-box testing          | Internal code and logic                                                                |
| Verification               | Building the product right                                                             |
| Validation                 | Building the right product                                                             |
| Maintenance                | Corrective, adaptive, perfective, preventive                                           |