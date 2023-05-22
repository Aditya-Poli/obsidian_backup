# Stack

Stack is an ordered list of elements whose memory locations are allocated sequentially all the insertions and deletions will be done at single end called top. It is also called **LIFO** (Last In First Out) data structure.

###### requirements:

The basic operations are push and pop.

###### Additional Requirements

Top, is_empty, is_full, length

### Implementation:

```python
class stack:
  def __init__(self, size):
    self.stack = []
    self.size = size
  def top(self):
      print(self.top())
      0#return stack.top()
  def size(self):
      return len(self.stack)
  def push(self, element):
    if len(self.stack)==self.size:
      print("Stack Overflow")
    else:
      self.stack.append(element)
  def pop(self):
    if len(self.stack)==0:
      print("Stack Underflow")
    else:
      self.stack.pop()
  def isEmpty(self):
    if len(self.stack) == 0:
      print(1)
    else:
      print(0)
  def isFull(self):
    if len(self.stack)==self.size:
      print(1)
    else:
      print(0)
```

### Applications of Stack:

Infix Notation --> (A + B) * C

Postfix Notation --> A B + C *

Prefix Notation --> * C + B A

To convert one notation to another we use stack.

###### Infix to Postfix Notation

1. Scan the infix notation from left to right.

2. If element == operand, Print it to the output screen.

3. If element == operator
   
   - If precedence of element is greater than the precedence of stack top the push it into the stack.
   
   - else: Pop all the operators in the stack which are having higher precedence than this operator.

4. If element == "(", Push it into the stack.

5. If element == ")", Pop all the elements from the stack until we get an open brace.

6. Repeat the above steps until all the elements in the infix notation are scanned.

###### Postfix to Infix Notation

1. Scan the expression from left to right.

2. If element == operand, Print it into the stack.

3. If element == operator then pop the top two values of the stack and place this operator in between them.

4. Push the obtained new expression into the stack again.

5. Repeat this until all the elements are scanned.

###### Postfix to Prefix Notation

1. Scan the expression from left to right.

2. If element == operand, Push it into the stack.

3. If element == operator
   
   - Pop the top element from the stack, let it be S1.
   
   - Pop the next top element from the stack, let it be S2.
   
   - Arrange as ---> (Operator   S2   S1)

4. Repeat the above steps until all the elements in the expression are scanned.

###### Prefix to Postfix Notation

1. Scan the expression from right to left.

2. If element == operand, Push it into the stack.

3. If element == operator
   
   - Pop the top element from the stack, let it be S1.
   
   - Pop the next top element from the stack, let it be S2.
   
   - Arrange as ---> (S1   S2   Operator)

4. Repeat the above steps until all the elements in the expression are scanned.
