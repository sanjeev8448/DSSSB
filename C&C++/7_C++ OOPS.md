# 1. Class

A class is a user-defined type that groups data members and member functions into a single unit.

Think of a class as a blueprint for creating objects. For example, a `Student` class can describe each student's roll number and marks, along with operations for displaying them.

```

#include <iostream>
using namespace std;

class Student
{
public:
    int roll;
    float marks;

    void display()
    {
        cout << roll << " " << marks << endl;
    }
};

int main()
{
    Student s1;
    s1.roll = 101;
    s1.marks = 85.5;

    s1.display();
    return 0;
}
```

Output

```
101 85.5
```

Understand the code:

- `class Student` defines the class.
    
- `roll` and `marks` are data members.
    
- `display()` is a member function.
    
- `public:` makes these members accessible from outside the class.
    
- The class definition ends with a semicolon: `};`.
    

A class definition describes a type; it does not by itself create a `Student` object.

# 2. Object

An object is an instance of a class. It has its own identity and, for ordinary non-static data members, its own stored values.

```
Student s1;
Student s2;
```

Here, `s1` and `s2` are separate objects of the same class.

### Class: Student

Defines the members and behavior common to student objects.

Object: `s1`

roll = 101

marks = 85.5

Object: `s2`

roll = 102

marks = 92.0

The two objects share the class definition but have separate non-static data-member values.

Example:

```

#include <iostream>
using namespace std;

class Student
{
public:
    int roll;
};

int main()
{
    Student s1, s2;

    s1.roll = 101;
    s2.roll = 102;

    cout << s1.roll << endl;
    cout << s2.roll << endl;

    return 0;
}
```

Output

```
101
102
```

Exam distinction: A class is a type or blueprint; an object is an instance of that type.

# 3. Constructor

A constructor is a special member function that initializes an object when it is created.

Important properties:

- Its name matches the class name.
    
- It has no return type, not even `void`.
    
- It is called automatically when an object is constructed.
    
- Constructors can be overloaded.
    

For example:

```
class Student
{
public:
    Student()
    {
        cout << "Object created" << endl;
    }
};
```

When a `Student` object is created, the constructor runs automatically.

## 3.1 Default constructor

A default constructor is a constructor that can be called with no arguments.

```

#include <iostream>
using namespace std;

class Student
{
public:
    int roll;

    Student()
    {
        roll = 0;
    }
};

int main()
{
    Student s;

    cout << s.roll << endl;
    return 0;
}
```

Output

```
0
```

The constructor initializes `roll` to zero.

### Important exam trap

If you do not declare any constructor, C++ can implicitly declare a default constructor for the class, subject to the language rules.

However, if you declare a parameterized constructor and do not provide a default constructor, this will generally fail:

```
class Student
{
public:
    Student(int x) {}
};

// Student s;  // Compilation error
```

Why? Declaring `Student(int)` means the compiler does not automatically provide the ordinary no-argument default constructor.

Also, a constructor with default arguments can qualify as a default constructor:

```
Student(int x = 0) {}
```

This constructor can be called without arguments.

## 3.2 Parameterized constructor

A parameterized constructor receives arguments so that an object can be initialized with specified values.

```

#include <iostream>
using namespace std;

class Student
{
public:
    int roll;
    float marks;

    Student(int r, float m)
    {
        roll = r;
        marks = m;
    }
};

int main()
{
    Student s1(101, 88.5f);
    Student s2(102, 91.0f);

    cout << s1.roll << " " << s1.marks << endl;
    cout << s2.roll << " " << s2.marks << endl;

    return 0;
}
```

Output

```
101 88.5
102 91
```

Here, `Student s1(101, 88.5f)` calls the constructor with `r = 101` and `m = 88.5`.

### Constructor initialization list

C++ also lets you initialize members before the constructor body executes.

```
Student(int r, float m) : roll(r), marks(m) {}
```

This is called a member initializer list. It is particularly important for `const` members, reference members, and members whose types do not have a suitable default constructor.

## 3.3 Copy constructor

A copy constructor initializes a new object using an existing object of the same class.

A typical form is:

```
ClassName(const ClassName& other);
```

Example:

```

#include <iostream>
using namespace std;

class Student
{
public:
    int roll;

    Student(int r) : roll(r) {}

    Student(const Student& other)
    {
        roll = other.roll;
        cout << "Copy constructor called\n";
    }
};

int main()
{
    Student s1(101);
    Student s2 = s1;

    cout << s2.roll << endl;
    return 0;
}
```

Output

```
Copy constructor called
101
```

`Student s2 = s1;` constructs a new object, `s2`, by copying `s1`. It invokes the copy constructor.

### Copy construction vs assignment

These are different operations:

```
Student s2 = s1;  // Copy construction: s2 is being created
s2 = s1;          // Assignment: s2 already exists
```

The second line uses the assignment operator, not the copy constructor.

### Shallow copy vs deep copy

A compiler-generated copy constructor copies members individually. If a member is a raw pointer, this copies the pointer value (the address), not the dynamically allocated object it points to.

This can cause problems when objects own resources, such as dynamically allocated memory. A deep copy creates a separate resource rather than making both objects point to the same resource.

For exam purposes, remember:

- Copy constructor: creates a new object from an existing object.
    
- Copy assignment: assigns to an already-existing object.
    
- Compiler-generated copying is memberwise; it is not automatically a deep copy.
    

# 4. Destructor

A destructor is a special member function that performs cleanup when an object's lifetime ends.

Syntax:

```
~ClassName()
{
    // Cleanup
}
```

Properties:

- The name is the class name preceded by `~`.
    
- It has no return type and takes no parameters.
    
- A class can have only one destructor; destructors cannot be overloaded.
    
- It is called automatically when an object's lifetime ends, subject to the object's storage duration and lifetime rules.
    

Example:

```

#include <iostream>
using namespace std;

class Demo
{
public:
    Demo()
    {
        cout << "Constructor\n";
    }

    ~Demo()
    {
        cout << "Destructor\n";
    }
};

int main()
{
    Demo d;
    cout << "Inside main\n";

    return 0;
}
```

Output

```
Constructor
Inside main
Destructor
```

The constructor runs when `d` is created. The destructor runs when `d`'s lifetime ends as `main()` exits.

### Constructor vs destructor

|Constructor|Destructor|
|---|---|
|Initializes an object|Cleans up when an object's lifetime ends|
|Same name as class|Same name with `~` prefix|
|Can be overloaded|Cannot be overloaded|
|Can take parameters|Takes no parameters|
|No return type|No return type|

Exam tip: For ordinary local objects, destructors run in reverse order of completed construction when the objects leave scope.

# 5. Four pillars of OOP

The four commonly taught pillars are encapsulation, abstraction, inheritance, and polymorphism. The next topics explain each one.

## 5.1 Encapsulation

Encapsulation means bundling data and the functions that operate on it into a unit, typically a class, while controlling access to the object's internal state.

For example, a bank account should not let arbitrary code change its balance without rules.

```

#include <iostream>
using namespace std;

class BankAccount
{
private:
    double balance;

public:
    BankAccount(double initial) : balance(initial) {}

    void deposit(double amount)
    {
        if (amount > 0)
            balance += amount;
    }

    double getBalance() const
    {
        return balance;
    }
};

int main()
{
    BankAccount account(1000);

    account.deposit(500);
    cout << account.getBalance() << endl;

    return 0;
}
```

Output

```
1500
```

Why is this encapsulation?

- `balance` is private, so external code cannot directly access it.
    
- `deposit()` controls how the balance is changed.
    
- `getBalance()` provides read-only access to the value.
    

This helps enforce rules and protects the object's state from accidental modification.

## 5.2 Abstraction

Abstraction means exposing essential operations while hiding unnecessary implementation details.

For example, a user can call `car.start()` without needing to know every internal step that starts the engine.

```

#include <iostream>
using namespace std;

class Car
{
private:
    void startEngine()
    {
        cout << "Engine started\n";
    }

public:
    void start()
    {
        startEngine();
        cout << "Car is ready\n";
    }
};

int main()
{
    Car car;
    car.start();

    return 0;
}
```

Output

```
Engine started
Car is ready
```

The user calls the simple public operation `start()`. The implementation detail `startEngine()` remains private.

### Encapsulation vs abstraction

|Encapsulation|Abstraction|
|---|---|
|Bundles data and behavior and controls access|Hides implementation details behind an interface|
|Often uses classes and access specifiers|Often uses public interfaces and abstract classes|
|Focus: protecting and organizing state|Focus: simplifying how a feature is used|

They are related, but they are not interchangeable definitions.

# 6. Inheritance

Inheritance allows a new class (derived class) to acquire accessible members and behavior from an existing class (base class), and extend or specialize them.

For example, `Dog` and `Cat` can inherit common behavior from `Animal`.

## 6.1 Single inheritance

One derived class inherits from one base class.

```

#include <iostream>
using namespace std;

class Animal
{
public:
    void eat()
    {
        cout << "Animal eats\n";
    }
};

class Dog : public Animal
{
public:
    void bark()
    {
        cout << "Dog barks\n";
    }
};

int main()
{
    Dog d;
    d.eat();
    d.bark();

    return 0;
}
```

Output

```
Animal eats
Dog barks
```

`Dog : public Animal` means `Dog` publicly inherits from `Animal`. The derived class can use the accessible public member `eat()`.

## 6.2 Types of inheritance

### Single inheritance

Animal

Dog

### Multilevel inheritance

Animal

Mammal

Dog

### Hierarchical inheritance

Animal

Dog

Cat

### Multiple inheritance

Printer

Scanner

MultifunctionDevice

Hybrid inheritance combines multiple inheritance patterns.

The five commonly taught forms are:

1. Single: One base class, one derived class.
    
2. Multiple: One derived class inherits from multiple base classes.
    
3. Multilevel: A class inherits from another derived class.
    
4. Hierarchical: Multiple derived classes inherit from one base class.
    
5. Hybrid: A combination of inheritance patterns.
    

### Multiple inheritance example

```

#include <iostream>
using namespace std;

class Printer
{
public:
    void print()
    {
        cout << "Printing\n";
    }
};

class Scanner
{
public:
    void scan()
    {
        cout << "Scanning\n";
    }
};

class Machine : public Printer, public Scanner
{
};

int main()
{
    Machine m;
    m.print();
    m.scan();

    return 0;
}
```

Output

```
Printing
Scanning
```

`Machine` inherits accessible operations from both `Printer` and `Scanner`.

### Constructor order in inheritance

Base-class construction happens before derived-class construction. Destruction occurs in the reverse order.

```

#include <iostream>
using namespace std;

class Base
{
public:
    Base()  { cout << "Base constructor\n"; }
    ~Base() { cout << "Base destructor\n"; }
};

class Derived : public Base
{
public:
    Derived()  { cout << "Derived constructor\n"; }
    ~Derived() { cout << "Derived destructor\n"; }
};

int main()
{
    Derived d;
    return 0;
}
```

Output

```
Base constructor
Derived constructor
Derived destructor
Base destructor
```

Exam tip: Base first, derived second during construction; derived first, base second during destruction.

# 7. Polymorphism

Polymorphism means “many forms.” In OOP, the same operation or interface can behave differently depending on the arguments or the actual object involved.

C++ polymorphism is commonly divided into:

- Compile-time polymorphism: Function overloading and operator overloading.
    
- Run-time polymorphism: Virtual functions and overriding through a base-class interface.
    

## 7.1 Compile-time polymorphism

The compiler determines which suitable overloaded function or operator is used based on the available types and arguments.

Example:

```
int add(int a, int b);
double add(double a, double b);
```

Both functions are named `add`, but the parameter types differ.

## 7.2 Run-time polymorphism

Run-time polymorphism commonly uses virtual functions. The function implementation is selected based on the actual type of the object when a virtual function is called through a base-class pointer or reference.

We'll examine virtual functions in detail below.

Exam distinction: Overloading is commonly associated with compile-time polymorphism; virtual-function overriding enables run-time polymorphism.

# 8. Function overloading

Function overloading means defining multiple functions with the same name but different parameter lists.

The functions can differ in the number of parameters, parameter types, or parameter order when the resulting signatures are distinct.

```

#include <iostream>
using namespace std;

int add(int a, int b)
{
    return a + b;
}

int add(int a, int b, int c)
{
    return a + b + c;
}

double add(double a, double b)
{
    return a + b;
}

int main()
{
    cout << add(2, 3) << endl;
    cout << add(2, 3, 4) << endl;
    cout << add(2.5, 3.5) << endl;

    return 0;
}
```

Output

```
5
9
6
```

The compiler selects the matching overload based on the supplied arguments.

### Can functions be overloaded only by return type?

No. These declarations cannot form two distinct overloads:

```
int calculate(int x);
double calculate(int x);  // Invalid overload
```

The parameter list is identical. The return type alone does not distinguish an overload.

Exam trap: Changing the return type alone does not create a valid overload.

# 9. Operator overloading

Operator overloading gives an existing C++ operator a suitable meaning for a user-defined type.

For example, you can define what `+` means when adding two objects of a `Complex` class.

```

#include <iostream>
using namespace std;

class Complex
{
public:
    int real;
    int imag;

    Complex(int r, int i) : real(r), imag(i) {}

    Complex operator+(const Complex& other) const
    {
        return Complex(real + other.real,
                       imag + other.imag);
    }
};

int main()
{
    Complex a(2, 3);
    Complex b(4, 5);

    Complex c = a + b;

    cout << c.real << " + " << c.imag << "i\n";
    return 0;
}
```

Output

```
6 + 8i
```

Here, `operator+` defines the behavior of `+` for `Complex` objects.

The expression:

```
Complex c = a + b;
```

uses the overloaded operator, which adds the real parts and imaginary parts separately.

### Important rules

- You cannot create a brand-new operator symbol; you overload existing operators.
    
- At least one operand must be a user-defined type when overloading an operator.
    
- You cannot change an operator's precedence or associativity.
    
- You cannot change the number of operands an operator takes.
    
- Some operators, including `::`, `.`, `.*`, `?:`, and `sizeof`, cannot be overloaded.
    

### Function overloading vs operator overloading

|Function overloading|Operator overloading|
|---|---|
|Same function name, different parameter lists|Gives an existing operator behavior for user-defined types|
|Example: `add(2, 3)`|Example: `a + b` for `Complex`|
|Compiler selects the matching overload|Compiler selects the suitable operator overload|

# 10. Virtual function

A virtual function is a member function declared with the keyword `virtual` in a base class. It supports run-time polymorphism when called through a base-class pointer or reference.

Consider this example.

```

#include <iostream>
using namespace std;

class Animal
{
public:
    virtual void sound()
    {
        cout << "Animal sound\n";
    }

    virtual ~Animal() = default;
};

class Dog : public Animal
{
public:
    void sound() override
    {
        cout << "Dog barks\n";
    }
};

int main()
{
    Dog d;
    Animal* ptr = &d;

    ptr->sound();

    return 0;
}
```

Output

```
Dog barks
```

Why?

- `ptr` has static type `Animal*`.
    
- It points to an actual `Dog` object.
    
- `sound()` is virtual.
    
- Therefore, the overridden `Dog::sound()` is called.
    

Without `virtual`, the call through `Animal*` would select `Animal::sound()` instead.

### A. What is overriding?

Function overriding occurs when a derived class provides its own implementation of an appropriate virtual function inherited from a base class.

```
class Animal
{
public:
    virtual void sound() { }
};

class Dog : public Animal
{
public:
    void sound() override { }
};
```

The `override` keyword tells the compiler that the derived function is intended to override a virtual base-class function. If it does not, the compiler diagnoses the mismatch.

### B. Pure virtual function and abstract class

A pure virtual function is declared with `= 0`.

```

#include <iostream>
using namespace std;

class Shape
{
public:
    virtual double area() const = 0;
    virtual ~Shape() = default;
};

class Rectangle : public Shape
{
    double width, height;

public:
    Rectangle(double w, double h)
        : width(w), height(h) {}

    double area() const override
    {
        return width * height;
    }
};

int main()
{
    Rectangle r(4, 5);
    cout << r.area() << endl;

    return 0;
}
```

Output

```
20
```

`Shape` is an abstract class because it has a pure virtual function. You cannot create an ordinary `Shape` object directly. A concrete derived class must implement the required pure virtual functions before it can be instantiated.

### Virtual-function revision

- `virtual` enables run-time dispatch for appropriate calls through base pointers or references.
    
- `override` checks the intended override.
    
- `= 0` declares a pure virtual function.
    
- A class with an unimplemented pure virtual function remains abstract.
    
- A polymorphic base class should generally have a virtual destructor when objects may be deleted through base-class pointers.
    

# 11. Friend function

A friend function is a non-member function that is granted access to a class's private and protected members.

It is declared inside the class using the `friend` keyword, but it is not a member function of that class.

```

#include <iostream>
using namespace std;

class Box
{
private:
    int length;

public:
    Box(int l) : length(l) {}

    friend void display(const Box& b);
};

void display(const Box& b)
{
    cout << b.length << endl;
}

int main()
{
    Box b(10);
    display(b);

    return 0;
}
```

Output

```
10
```

Why can `display()` access `b.length`, even though `length` is private? Because the class explicitly declared it as a friend.

### Important properties

- A friend function is not a class member.
    
- It can access the class's private and protected members.
    
- It is called like an ordinary function: `display(b)`, not `b.display()`.
    
- Friendship is not automatically inherited.
    
- Friendship is not automatically reciprocal: if class A declares a function as a friend, that does not automatically give A's functions access to every private member of class B.
    

### Friend function vs member function

|Friend function|Member function|
|---|---|
|Not a class member|Belongs to the class|
|Declared with `friend` inside the class|Declared as a normal class member|
|Called like a normal function|Usually called through an object or class, depending on its type|
|Can access private members when friendship is granted|Can access the class's private members directly|

# 12. Static members

The `static` keyword has different meanings depending on where it is used. For classes, the important concepts are static data members and static member functions.

## 12.1 Static data member

A static data member belongs to the class rather than to each individual object. There is one shared member for that class, not a separate copy in every object.

```

#include <iostream>
using namespace std;

class Student
{
public:
    static int count;

    Student()
    {
        count++;
    }
};

int Student::count = 0;

int main()
{
    Student s1;
    Student s2;
    Student s3;

    cout << Student::count << endl;

    return 0;
}
```

Output

```
3
```

Each constructor increments the shared `count`. After three objects are constructed, the value is `3`.

### Why is `int Student::count = 0;` needed?

For a traditional non-inline static data member, the class declares the member, and one definition is provided outside the class.

Since C++17, an `inline static` data member can instead be initialized inside the class:

```
class Student
{
public:
    inline static int count = 0;
};
```

### 12.2 Static member function

A static member function belongs to the class and can be called without creating an object.

```

#include <iostream>
using namespace std;

class Math
{
public:
    static int square(int x)
    {
        return x * x;
    }
};

int main()
{
    cout << Math::square(5) << endl;
    return 0;
}
```

Output

```
25
```

Notice the class-name call:

```
Math::square(5);
```

A static member function has no `this` pointer, so it cannot directly access a particular object's non-static data members without being given an object or reference.

Exam traps:

- Static data members are shared among objects of the class.
    
- Static member functions can be called using the class name and `::`.
    
- A static member function cannot be declared `virtual`.
    
- Static functions are different from ordinary non-member functions.
    

# 13. Access specifiers

Access specifiers control where class members can be accessed.

C++ has three principal access specifiers:

- `public`
    
- `private`
    
- `protected`
    

## 13.1 Public

Public members are accessible from code that has access to the object or class, subject to other language rules.

```
class Demo
{
public:
    int x;
};
```

Example:

```
Demo d;
d.x = 10;  // Valid
```

## 13.2 Private

Private members are accessible from the class's member functions and its friends, subject to the language rules. They cannot normally be accessed directly from unrelated external code.

```
class Demo
{
private:
    int x;
};
```

This is invalid from ordinary external code:

```
Demo d;
// d.x = 10;  // Compilation error
```

Default access rule: Members of a `class` are private by default.

## 13.3 Protected

Protected members are accessible from the class's member functions and friends, and from suitable derived-class member functions and friends. They are not normally accessible directly through an ordinary external object expression.

```
class Base
{
protected:
    int x = 10;
};

class Derived : public Base
{
public:
    void show()
    {
        cout << x << endl;
    }
};
```

`Derived::show()` can access the inherited protected member `x`.

## 13.4 Access-specifier comparison

|Feature|`public`|`protected`|`private`|
|---|---|---|---|
|Accessible inside the declaring class|Yes|Yes|Yes|
|Accessible directly by unrelated external code|Yes|No|No|
|Accessible in derived-class member code|If inherited access permits|If inheritance access permits|Not directly|
|Default for `class` members|No|No|Yes|
|Default for `struct` members|Yes|No|No|

### Class vs struct defaults

In C++, `class` and `struct` both support member functions, constructors, inheritance, and access specifiers. Their key defaults differ:

```
class A
{
    int x;  // Private by default
};

struct B
{
    int x;  // Public by default
};
```

The default inheritance access also differs:

```
class Derived1 : Base { };  // Private inheritance by default
struct Derived2 : Base { }; // Public inheritance by default
```

# 14. Important OOP comparisons for DSSSB

These distinctions are especially useful for multiple-choice and output-based questions.

|Concepts|Key difference|
|---|---|
|Class vs object|Type definition vs instance|
|Default vs parameterized constructor|Can be called without arguments vs accepts specified arguments|
|Constructor vs destructor|Initializes object vs cleans up at end of lifetime|
|Copy constructor vs assignment|Creates a new object from another vs assigns to an existing object|
|Encapsulation vs abstraction|Organizes and protects state vs hides implementation behind an interface|
|Overloading vs overriding|Same name with different parameter lists vs derived implementation of an inherited virtual function|
|Compile-time vs run-time polymorphism|Overload resolution vs virtual dispatch|
|Structure vs class|C++ `struct` defaults to public; `class` defaults to private|
|Friend vs member function|Non-member with granted access vs class member|
|Static vs non-static member|Shared at class level vs associated with individual objects|
|Public vs protected vs private|External access permitted vs derived/class access vs class/friend access|