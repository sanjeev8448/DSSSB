## 1. Understanding a stack

Think of a stack of plates: you place a new plate on top, and you usually remove the topmost plate first.

### Stack example

### 30

Top

### 20

### 10

Bottom

Here, `30` was inserted last, so it will be removed first.

Suppose we perform these operations:

1. Push `10`
    
2. Push `20`
    
3. Push `30`
    
4. Pop once
    

The stack changes as follows:

```
Push(10)  → [10]
Push(20)  → [10, 20]
Push(30)  → [10, 20, 30]
Pop()     → [10, 20]
```

The removed element is `30`.

Exam keyword: LIFO = Last In, First Out.

## 2. `push()` — inserting an element

The `push()` operation adds an element to the top of the stack.

Consider a stack initially containing `[10, 20]`.

### Try pushing an element

Stack (bottom → top)

### 20

TOP

### 10

Value to push

PushClear stack

The top is shown above the other elements. Each push adds an element to the top.

### Python implementation

Python lists do not have a built-in `push()` method. The common approach is to use `append()`.

```
stack = []stack.append(10)stack.append(20)stack.append(30)print(stack)
```

Output:

```
[10, 20, 30]
```

The end of the list represents the top of the stack.

- `append(x)` performs the push operation.
    
- The operation is typically \(O(1)\) amortized for a Python list.
    

Exam trap: For a Python-list-based stack, use `append()` to push. `push()` is the conceptual stack operation, not a standard method of Python's built-in list.

## 3. `pop()` — removing the top element

The `pop()` operation removes and returns the top element of the stack.

Suppose:

```
Stack = [10, 20, 30]
```

Calling `pop()` removes `30`, leaving `[10, 20]`.

### Python implementation

```
stack = [10, 20, 30]removed = stack.pop()print("Removed:", removed)print("Stack:", stack)
```

Output:

```
Removed: 30
Stack: [10, 20]
```

Remember that `pop()` both removes the element and returns its value.

### Interactive example

### Pop the top element

3 elements

### 30

TOP — removed first

### 20

### 10

PopReset example

### Stack underflow

Stack underflow occurs when a program attempts to remove an element from an empty stack.

```
stack = []stack.pop()
```

Output: Python raises an `IndexError` because the list is empty.

A safe implementation checks whether the stack contains an element before popping it.

```
stack = []if stack:    print(stack.pop())else:    print("Stack underflow")
```

Output:

```
Stack underflow
```

Exam trap: Underflow is a condition or error associated with trying to remove an element when the stack is empty. In Python, an unguarded `list.pop()` on an empty list raises `IndexError`.

## 4. `peek()` — viewing the top element

The `peek()` operation returns the top element without removing it.

For example:

```
Stack = [10, 20, 30]
Peek() → 30
Stack remains [10, 20, 30]
```

Python list implementation:

```
stack = [10, 20, 30]if stack:    print("Top:", stack[-1])else:    print("Stack is empty")print("Stack:", stack)
```

Output:

```
Top: 30
Stack: [10, 20, 30]
```

Python lists do not have a built-in `peek()` method. When the end represents the top, `stack[-1]` is a simple way to peek.

### `push()` vs `pop()` vs `peek()`

|Operation|Purpose|Removes an element?|Typical Python-list implementation|
|---|---|---|---|
|`push(x)`|Adds an element to the top|No|`stack.append(x)`|
|`pop()`|Removes and returns the top|Yes|`stack.pop()`|
|`peek()`|Reads the top element|No|`stack[-1]`|

Important: Peeking at an empty stack must be handled. In Python, evaluating `stack[-1]` when the stack is empty raises `IndexError`.

## 5. Complete stack implementation in Python

Here is a simple stack class that implements all three operations and handles an empty stack.

```
class Stack:    def __init__(self):        self.items = []    def push(self, item):        self.items.append(item)    def pop(self):        if self.is_empty():            return "Stack underflow"        return self.items.pop()    def peek(self):        if self.is_empty():            return "Stack is empty"        return self.items[-1]    def is_empty(self):        return len(self.items) == 0    def size(self):        return len(self.items)s = Stack()s.push(10)s.push(20)s.push(30)print("Top:", s.peek())print("Removed:", s.pop())print("Top now:", s.peek())print("Size:", s.size())
```

Output:

```
Top: 30
Removed: 30
Top now: 20
Size: 2
```

This class uses a Python list internally. In a production implementation, raising a dedicated exception or returning an explicit status for an empty stack may be preferable to returning a string, because the string could also be a legitimate stack value.

## 6. Applications of a stack

Stacks are used whenever the most recently added or opened item must be handled first.

![Stack of books on black background](https://images.openai.com/static-rsc-4/Ny5VS9X0kKHmim0yTtOFDopA4_oUkdqLTaVgMbksDAxTquVYaBqk7KVygg2QkZ1NSKUd5QklCwe8yRqKrwdIqHFKSlJfFXRFNJJG4_3NGlu42YWfZJtHH2Sx9IdI2uPbR0TWZiHoVMOG6419pbo3mhiuxRqln4fBeMDnSiZ76NHkK6_Cm2HUfSpAP682g9mr?purpose=inline)

1. Function calls and recursion

When a function calls another function, execution information is maintained on the call stack. Recursive calls create nested execution contexts that return in reverse order.

![Coding : Checking Balanced Brackets in JavaScript | by Monu Kumar Modi | The Fresh Writes | Medium](https://images.openai.com/static-rsc-4/fxGsjsLdhMnwlmD24mdRx5nnBRCnQzag0fVXTOWupm5OtjlcyGWYrxUVloyzE78Q23ZkqwTllKdMh_JQVg-__KGayFipuuhrgP_GbMQ_VwZonvNhrSSiMJrO6iXScJhFhJ-LQjT3adlBihIRQMk0m1GQE8qXFnit1mqhUEI1nKU?purpose=inline)

2. Parentheses and delimiter matching

A stack can check whether brackets such as `()`, `[]`, and `{}` are correctly nested.

![Apryse SDK Adds Undo/Redo to DOCX Editor | Apryse](https://images.openai.com/static-rsc-4/Nr-WD5DPNlFB1VnXpVYa7PiQ8_3TEcy1iK36rmdQmOgZ64KadvBrJWNXqsaW_pNNepypiW2geaFiG_r3dr-SS-XtvfetsSc06RWmiB5APAbEZH7CDi6fc88c9FDMl4_KP6crR9aaSaY1VL-gpVKVKEd-mBrfbGPi5Pui1CLA4Vg?purpose=inline)

3. Undo operations

Text editors can store recent actions and reverse the latest action first. A related stack may store redo actions.

![Stack in Python: Definition, Implementations and Examples](https://images.openai.com/static-rsc-4/e-J1uNUVNZRv-Rgmejonwxd1puoOoF20aQSxUUkyjucGX-RyrSMQh_PP8wkOX8UeTLqBAripBvxJPDaV97AF422AvwL6rh2FTxfNebbORNz6jBvw_He2rjLbxMqGj0p89ngqbM8ffP_UYHEE6yJ8-M6SvxcrkHKRozEvflqCskA?purpose=inline)

4. Expression conversion and evaluation

Stacks are used with infix, postfix, and prefix expressions, including operator handling and evaluation of postfix expressions.

![Virtual Labs](https://images.openai.com/static-rsc-4/MxiX0A8Izbxpw9P5Wu9KB4sGbcE4vK59MvJIs1IZxS3kG5y93nvQqCLf6Ae__tlEM1NZKMvHvav8gfXYDBelBm2ncVOTUqOhnNtAF-4KoBHpTdh7V4ZeeJiVTxP4qp-OH0-9WEjnI7YjscVZDh5FCU0jofrxzhoZV_9Lc0FmOfA?purpose=inline)

5. Graph traversal and backtracking

Depth-first search (DFS) can be implemented using a stack. Stacks also help algorithms revisit previous decisions during backtracking.

### 6.1 Application: Balanced parentheses

A stack helps verify that every closing bracket matches the most recent unmatched opening bracket.

Example:

```
Expression: {(a+b)*[c-d]}
Result: Balanced
```

But:

```
Expression: ([)]
Result: Not balanced
```

Python implementation:

```
def balanced(expression):    stack = []    pairs = {')': '(', ']': '[', '}': '{'}    for ch in expression:        if ch in "([{":            stack.append(ch)        elif ch in ")]}":            if not stack or stack.pop() != pairs[ch]:                return False    return len(stack) == 0print(balanced("{(a+b)*[c-d]}"))print(balanced("([)]"))print(balanced("((a+b)"))
```

Output:

```
True
False
False
```

Why does `([)]` fail? When `)` is encountered, the most recent unmatched opening bracket is `[`, but `)` requires `(`. The order is incorrect.

Exam trap: Checking only the total number of opening and closing brackets is insufficient. Their nesting order must also be correct.

### 6.2 Application: Postfix evaluation

In a postfix expression, operators appear after their operands.

Example:

```
Infix:  2 + 3
Postfix: 2 3 +
```

For the postfix expression:

```
2 3 + 4 *
```

Steps:

1. Push `2`.
    
2. Push `3`.
    
3. On `+`, pop both and compute `2 + 3 = 5`; push `5`.
    
4. Push `4`.
    
5. On `*`, compute `5 * 4 = 20`.
    

Result: `20`.

Exam trap: For a binary operator, the first value popped is the right operand, and the second popped is the left operand. This matters for subtraction and division.

## 7. Stack time complexity

Assume the top of the stack is at the end of a Python list.

|Operation|Typical time complexity|Explanation|
|---|---|---|
|Push|\(O(1)\) amortized|Append to the end|
|Pop|\(O(1)\)|Remove the last element|
|Peek|\(O(1)\)|Access the last element|
|Check empty|\(O(1)\)|Check the list length|
|Search for an arbitrary element|\(O(n)\)|May need to examine all elements|

A push may occasionally take \(O(n)\) if the underlying dynamic array needs to resize. Over a sequence of pushes, the amortized cost is typically \(O(1)\).

## 8. Array-based stack vs linked-list stack

|Feature|Array/list-based stack|Linked-list stack|
|---|---|---|
|Storage|Dynamic array or list|Nodes connected by references|
|Push at top|Typically \(O(1)\) amortized|\(O(1)\)|
|Pop at top|\(O(1)\)|\(O(1)\)|
|Extra memory per element|No node link required|Node references require extra memory|
|Capacity|Dynamic lists can grow|Nodes can be allocated as needed|
|Implementation|Usually simpler|Requires node and reference management|

Both implementations can provide constant-time push and pop when the top is maintained appropriately.

## Final revision sheet

|Topic|Must remember|
|---|---|
|Stack|Linear data structure using LIFO|
|Push|Insert at the top|
|Pop|Remove and return the top element|
|Peek|Inspect the top without removing it|
|Underflow|Attempt to pop an empty stack|
|Python push|`stack.append(x)`|
|Python pop|`stack.pop()`|
|Python peek|`stack[-1]`, after checking the stack is non-empty|
|Applications|Recursion, function calls, parentheses, undo, postfix evaluation, DFS|
|Push/pop complexity|Typically \(O(1)\) amortized for list-based stacks|

Highest-priority exam concepts: LIFO order, `push()` vs `pop()` vs `peek()`, stack underflow, balanced parentheses, and postfix expression evaluation.

Next Data Structures topic: Queue — enqueue, dequeue, front/rear, circular queue, and applications.