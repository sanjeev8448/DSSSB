# Stack in Data Structures

## DSSSB TGT Computer Science – Section B

## 1. Understanding a Stack

A stack is a linear data structure in which insertion and deletion take place at the same end, called the **TOP**.

Think of a stack of plates: you place a new plate on top and remove the topmost plate first.

### Example

```
       TOP
      ┌────┐
      │ 30 │  ← Inserted last
      ├────┤
      │ 20 │
      ├────┤
      │ 10 │
      └────┘
      BOTTOM
```

Suppose we perform these operations:

1. Push 10
    
2. Push 20
    
3. Push 30
    
4. Pop once
    

The stack changes as follows:

```
Push(10) → [10]
Push(20) → [10, 20]
Push(30) → [10, 20, 30]
Pop()    → [10, 20]
```

The removed element is `30`.

**Exam keyword: LIFO — Last In, First Out.**

The element inserted last is the first element removed.

---

## 2. Push — Inserting an Element

The `push()` operation adds an element to the top of the stack.

Suppose the stack initially contains:

`[10, 20]`

After pushing `30`:

`[10, 20, 30]`

Here, `30` is the top element.

### Python Implementation

Python lists do not have a built-in `push()` method. The common approach is to use `append()`.

```
stack = []

stack.append(10)
stack.append(20)
stack.append(30)

print(stack)
```

Output:

```
[10, 20, 30]
```

The end of the Python list represents the top of the stack.

- `append(x)` performs the push operation.
    
- Time complexity: O(1) amortized.
    

**Exam trap:** `push()` is the conceptual stack operation. For a Python-list-based stack, use `stack.append(x)`.

---

## 3. Pop — Removing the Top Element

The `pop()` operation removes and returns the top element of the stack.

Suppose:

`stack = [10, 20, 30]`

Calling `pop()` removes `30`, leaving `[10, 20]`.

### Python Implementation

```
stack = [10, 20, 30]

removed = stack.pop()

print("Removed:", removed)
print("Stack:", stack)
```

Output:

```
Removed: 30
Stack: [10, 20]
```

Remember that `pop()` both removes the element and returns its value.

### Stack Underflow

Stack underflow occurs when a program attempts to remove an element from an empty stack.

```
stack = []
stack.pop()
```

Output: Python raises an `IndexError` because the list is empty.

A safe implementation checks whether the stack contains an element before popping it.

```
stack = []

if stack:
    print(stack.pop())
else:
    print("Stack underflow")
```

Output:

```
Stack underflow
```

**Exam trap:** Underflow means attempting to remove an element from an empty stack. In Python, an unguarded `list.pop()` on an empty list raises `IndexError`.

---

## 4. Peek — Viewing the Top Element

The `peek()` operation returns the top element without removing it.

Example:

```
Stack = [10, 20, 30]

Peek() → 30

Stack remains [10, 20, 30]
```

### Python Implementation

Python lists do not have a built-in `peek()` method. When the end represents the top, `stack[-1]` can be used.

```
stack = [10, 20, 30]

if stack:
    print("Top:", stack[-1])
else:
    print("Stack is empty")

print("Stack:", stack)
```

Output:

```
Top: 30
Stack: [10, 20, 30]
```

Important: Accessing `stack[-1]` when the stack is empty raises `IndexError`.

### Push vs Pop vs Peek

|Operation|Purpose|Removes an Element?|Python Implementation|
|---|---|---|---|
|`push(x)`|Adds an element to the top|No|`stack.append(x)`|
|`pop()`|Removes and returns the top|Yes|`stack.pop()`|
|`peek()`|Reads the top element|No|`stack[-1]`|

---

## 5. Complete Stack Implementation in Python

The following class implements push, pop, peek, checking whether the stack is empty, and finding its size.

```
class Stack:
    def __init__(self):
        self.items = []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        if self.is_empty():
            return "Stack underflow"

        return self.items.pop()

    def peek(self):
        if self.is_empty():
            return "Stack is empty"

        return self.items[-1]

    def is_empty(self):
        return len(self.items) == 0

    def size(self):
        return len(self.items)


s = Stack()

s.push(10)
s.push(20)
s.push(30)

print("Top:", s.peek())
print("Removed:", s.pop())
print("Top now:", s.peek())
print("Size:", s.size())
```

Output:

```
Top: 30
Removed: 30
Top now: 20
Size: 2
```

This class uses a Python list internally. In production code, raising a dedicated exception or returning an explicit status for an empty stack may be preferable to returning a string, because that string could also be a legitimate stack value.

---

## 6. Applications of a Stack

Stacks are used whenever the most recently added or opened item must be handled first.

### 6.1 Function Calls and Recursion

When a function calls another function, execution information is maintained on the call stack. Recursive calls return in reverse order.

### 6.2 Parentheses and Delimiter Matching

A stack checks whether brackets such as `()`, `[]`, and `{}` are correctly nested.

### 6.3 Undo Operations

Text editors can store recent actions and reverse the latest action first. A related stack may store redo actions.

### 6.4 Expression Conversion and Evaluation

Stacks are used with:

- Infix expressions
    
- Postfix expressions
    
- Prefix expressions
    
- Operator handling
    
- Postfix expression evaluation
    

### 6.5 Graph Traversal and Backtracking

Depth-first search (DFS) can be implemented using a stack. Stacks also help algorithms revisit previous decisions during backtracking.

---

## 7. Application: Balanced Parentheses

A stack verifies that every closing bracket matches the most recent unmatched opening bracket.

### Examples

Balanced:

```
{(a+b)*[c-d]}
```

Not balanced:

```
([)]
```

### Python Implementation

```
def balanced(expression):
    stack = []
    pairs = {
        ')': '(',
        ']': '[',
        '}': '{'
    }

    for ch in expression:
        if ch in "([{":
            stack.append(ch)

        elif ch in ")]}":
            if not stack or stack.pop() != pairs[ch]:
                return False

    return len(stack) == 0


print(balanced("{(a+b)*[c-d]}"))
print(balanced("([)]"))
print(balanced("((a+b)"))
```

Output:

```
True
False
False
```

### Why Does `([)]` Fail?

1. `(` is pushed.
    
2. `[` is pushed.
    
3. When `)` appears, the most recent unmatched opening bracket is `[`.
    
4. But `)` requires `(`.
    
5. Therefore, the expression is not balanced.
    

**Exam trap:** Checking only the total number of opening and closing brackets is insufficient. Their nesting order must also be correct.

---

## 8. Application: Postfix Expression Evaluation

In a postfix expression, operators appear after their operands.

Example:

```
Infix:   2 + 3
Postfix: 2 3 +
```

Consider the postfix expression:

```
2 3 + 4 *
```

### Step-by-Step Evaluation

1. Read `2` and push it.
    
2. Read `3` and push it.
    
3. Encounter `+`: pop both values and calculate `2 + 3 = 5`. Push `5`.
    
4. Read `4` and push it.
    
5. Encounter `*`: calculate `5 * 4 = 20`.
    

Result: **20**

### Python Implementation

```
def evaluate_postfix(expression):
    stack = []

    for token in expression.split():
        if token.lstrip("-").isdigit():
            stack.append(int(token))
        else:
            right = stack.pop()
            left = stack.pop()

            if token == "+":
                stack.append(left + right)
            elif token == "-":
                stack.append(left - right)
            elif token == "*":
                stack.append(left * right)
            elif token == "/":
                stack.append(left / right)

    if len(stack) != 1:
        raise ValueError("Invalid postfix expression")

    return stack.pop()


print(evaluate_postfix("2 3 + 4 *"))
```

Output:

```
20
```

This example handles integer operands and the four basic arithmetic operators. It assumes the expression is otherwise valid; a more complete evaluator should validate operand counts, operator tokens, and division by zero.

**Exam trap:** For a binary operator, the first value popped is the right operand, and the second value popped is the left operand. This matters for subtraction and division.

For example, postfix `8 2 -` means `8 - 2`, not `2 - 8`.

---

## 9. Stack Time Complexity

Assume the top of the stack is at the end of a Python list.

|Operation|Typical Time Complexity|Explanation|
|---|---|---|
|Push|O(1) amortized|Append to the end|
|Pop|O(1)|Remove the last element|
|Peek|O(1)|Access the last element|
|Check empty|O(1)|Check the list length|
|Search for an arbitrary element|O(n)|May need to examine all elements|

A push may occasionally take O(n) if the underlying dynamic array needs to resize. Over a sequence of pushes, the amortized cost is typically O(1).

---

## 10. Array-Based Stack vs Linked-List Stack

|Feature|Array/List-Based Stack|Linked-List Stack|
|---|---|---|
|Storage|Dynamic array or list|Nodes connected by references|
|Push at top|Typically O(1) amortized|O(1)|
|Pop at top|O(1)|O(1)|
|Extra memory per element|No node link required|Node references require extra memory|
|Capacity|Dynamic lists can grow|Nodes can be allocated as needed|
|Implementation|Usually simpler|Requires node and reference management|

Both implementations can provide constant-time push and pop when the top is maintained appropriately.

---

## 11. Common DSSSB Exam Traps

1. **LIFO:** Last In, First Out.
    
2. **Push:** Inserts an element at the top.
    
3. **Pop:** Removes and returns the top element.
    
4. **Peek:** Reads the top without removing it.
    
5. **Underflow:** Occurs when removing an element from an empty stack.
    
6. **Python push:** Use `stack.append(x)`.
    
7. **Python pop:** Use `stack.pop()`.
    
8. **Python peek:** Use `stack[-1]` after checking that the stack is not empty.
    
9. **Balanced parentheses:** The order and nesting of brackets matter.
    
10. **Postfix evaluation:** The first popped operand is the right operand.
    
11. **DFS:** A stack can be used to implement depth-first search.
    
12. **Complexity:** Push and pop are typically O(1) amortized and O(1), respectively, for a list-based stack.
    

---

## Final Revision Sheet

|Topic|Must Remember|
|---|---|
|Stack|Linear data structure using LIFO|
|Push|Insert at the top|
|Pop|Remove and return the top element|
|Peek|Inspect the top without removing it|
|Underflow|Attempt to pop an empty stack|
|Python push|`stack.append(x)`|
|Python pop|`stack.pop()`|
|Python peek|`stack[-1]`, after checking non-empty|
|Applications|Recursion, function calls, parentheses, undo, postfix evaluation, DFS|
|Push/pop complexity|Typically O(1) amortized for list-based stacks|

**Highest-priority exam concepts:** LIFO order, push vs pop vs peek, stack underflow, balanced parentheses, and postfix expression evaluation.

**Next Data Structures topic:** Queue — enqueue, dequeue, front/rear, circular queue, and applications.