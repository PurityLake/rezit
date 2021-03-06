# Rezit
Compiled, statically typed, object oriented programming language. 

## Design
All aspects of the language are represented as objects including files of which the contents are wrapped in a class of the same name as file
file. Literals in the code will be translated to objects at compile time so they can be acted upon by functions e.g.`"hello world".toUpperCase()`,
`3.forEach(func(i) -> { print(i) })`. Literal objects will share the same memory address for each time they are used and are as a result considered
immutable i.e. there will be no methods that alter their state, returning a new object as required. 

# Reference
## Assignment
### Variable Assignment
```
let x = 10;
let y: Int;
```
Assignments use type inference to determine types in the case of an inline assignment like `line 1` where as if the value of a variable is not
known upon definition then, a type is required as referred to in `line 2`.

### Assignment Destructuring
```
let t = (10, 20); # 2-tuple literal
let (a, b) = (10, 20);
let (c, _) = (10, 20);
let (d, e) = t;
let [f:g:rest] = [ 1, 2, 3, 4, 5 ]; # array literal
```
In the case of this example assignment is inferred. In `line 2`, `a` is assigned the value `10` and `b` is assigned the value `20`. For this assignment
to take place then right hand side must have the same dimensions as the assignee of the left, in this case a 2-tuple. 

`Line 3` shows that the underscore character is a wild card that will ignore whatever value it is passed. 

`Line 4` is an example of a variable `t` being used instead of a tuple literal.

`Line 5` is an example of destructuring an array, each variable is seperated by colon character. In this example `f` is assigned the value 1, 
`g` is assigned the value 2 and `rest` is given the remaining elements of the array i.e. `[3, 4, 5]`.

### Public assignments
```
public let p = 20;
```
As each global variable is considered a part of a class, all `let` statements are considered private by default to stop code outside of the class 
from changing interasl values. In Rezit it is recommened to create getter and setter methods to access internals of the file that need to be accessed
as apposed to allowing users free reign of interals.

## Control Flow
### if Statement
```
let x = true;
if x {
  Console.println("true");
} else if 10 < 20 {
  print("10 < 20");
} else {
  Console.println("false");
}
```
If statements can be used as expected to allow branching paths depending on a boolean expression. If you are using an if statement to change flow of control,
you must end every statement with a `;` character.

### if Expression
```
let y = if true {
  10
} else {
  20
}
```
On the other hand and if can be treated as an expression returning the last non-semicolon terminated line. Tne result can be given to a variable or returned at
the end of a function definition. 

NOTE:
The return value of the if expression must return the same type of result. The type of `y` must be known at compile time so both statements have to match type-wise.

```
# this is considered a compile time error
let y = if true {
  10
} else {
  "a string"
}
```

The previous example is an illustration of what constitutes a compile time error in Rezit.

### for loop
```
let arr = [1, 2, 3, 4, 5];
for num in [1, 2, 3, 4, 5] {
  print(num);
}
```
A for loop in Rezit uses iterator objects to loop over collections of data like `arr`, iterators will be elaborated on in a different document. A let statement is not required
in a foor loop as the variable is declared in a separate scope unique to the for loop.

## Function Declaration
```
func add2(x: Int, y: Int) : Int {
  Console.printf("%d + %d = %d\n", x, y, x + y);
  x + y
}
```

## Class Declaration
```
class Foo {
  let x: Int;
  let y: Int;
  
  constructor(x: Int, y: Int() {
    this.x = x;
    this.y = y;
  }
  
  private func privateFunc() {
    # implementation
  }
  
  func publicFunc() {
    # implementation
  }
}
```
