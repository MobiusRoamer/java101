# Quick Quizzes

A collection of quiz questions in lectures. 

## Arrays
**1. If a reference variable is declared and not assigned, it is undefined.**
- True
- More precisely, local variables must be explicitly initialized
```java
String s;
System.out.println(s); // compile error - not initialized
 
```

**2. Arrays are mutable reference types**
- True

**3. Elements of an array of reference type are consecutively stored.**
- False
- References are consecutive but the objects are scattered in the heap
- Only references are consecutive, not objects themselves!
```java
arr[0] -> object at heap address 0x1000
arr[1] -> 0x8AB4
arr[2] -> 0x9271
```
**4. Elements of an array are stored on the heap**
- True
- All objects are stored in heaps in java

**5. Elements of an array are stored in the stack**
- False
- Only local variables pointing to the arrays are stored on stack

---

## Recursion & Maps
**1. Any time a function calls itself, it is structural recursion.**
- False
- Structural recursion is where the recursive calls directly mirror the structure of a data type.
- All structural recursions are recursions but not all recursions are structural!
- For example
```java
int multiply(int n) {
    n * multiply(n-1);
}
// is a structural recursion because it follows the factorial structure

// But this is not structural recursion
int f(int n) {
  return f(n - 2);  // Not consuming the structure properly
}
```

**2. Functions can be structurally recursive without a recursive data type**
- True
- Note recursive data types refer to, for example, lists that has a (head, tail) recursive structure, binary trees that has (left, root, right), etc. (As long as it has  abase case, a recursive case, functions
defined on it follows the same patter)
- But we don't always need a recursive data type to construct structural recursion. For example
```java
int sumTo(int n) {
    if (n == 0) return 0;
    return n + sumTo(n - 1);
}
```
**3. A key appears only once in a map.**
- True
- Map guarantees unique keys
```java
map.put("x", 1);
map.put("x", 2); // replaces 1 
```

**4. Maps may or may not contain a value for a key.**
- True

**5. Maps are always based on lists**
- False
- In java, 
- HashMap → hash buckets 
- TreeMap → red-black tree 
- LinkedHashMap → hash table + doubly linked list

---
## Imperative Programming
**1. Calling a function with the same arguments always returns the same results.**
- False
- Side effects change result
```java
int counter = 0;
int next() { return counter++; }

next(); // 0
next(); // 1  (same argument list: none)

```
**2. Functions may have results, but they may also have side-effects.**
- True
- See previous

**3. Order of evaluation does not matter**
- False

**4. Mutable state allows remembering without passing arguments.**
- True
```java
int total = 0;
void add(int x) { total += x; }
```

---
## Mutable States
**1. The scope of a variable is from where it was defined to the end of the block in which it was defined**
- True

**2. `new` creates a new thing on the heap**
- True
- In Java, objects are primarily stored on a heap!
- Only the local reference to the variable lives on stack 

**3. The scope of a variable is anywhere after it was defined.**
- False
- A variable exists only inside the block where it was declared
```java
if (true) {
    int x = 10;
}
System.out.println(x); // ERROR – x is out of scope
```

**4. A variable ALWAYS represents the same value within its scope.**
- False
- They are mutable
```java
int x = 3;
x = 10;   // Changed inside its scope 
```
**5. New creates a new thing on the stack.**
- False
- No java object ever goes on the stack, only references do

---
## Generics
**1. Casts are the best way to deal with potential information loss.**
- False. 
- Casts are unsafe and can throw ClassCastException. 
- Prefer generics (type parameters, bounds, wildcards) to model types safely at compile time.

**2. `x instanceof String` crashes the program if x is not a String at run time.**
- False
- It returns false. It’s a cast like `(String) x` that can crash with `ClassCastException`.

**3. A list always knows what its element type is.**
- False
- False. Due to type erasure, at runtime a List<String> is just a List; it doesn’t retain the element type.

**4. Generic type variables can be declared within a method’s code block**
- True
- We can declare method type parameters whose scope is the method body
- Example

**5. If G is a generic type, and A is a subtype of B, then `G<A>` is a subtype of `G<B>`**
- False
- Java generics are invariant.
- `List<Integer>` is not a subtype of `List<Number>`. Use wildcards (List<? extends Number>) if need variance.

```java
public static <T> T id(T x) { return x; }
```
## Abstract Data Types
**1. The Java standard library uses parameterized abstract classes to express the concept of an ADT.**
- Partially true
- This is feasible but not the common practice
- The main way ADTs are expressed in the standard library is through generic interfaces, not abstract classes
```java 
List<E>, Set<E> // E = generics
```
**2. The Java standard library uses generic interfaces to express the concept of an ADT**
- True
- See previous

**3. The Java standard library uses parameterized sealed interfaces to express the concept of an ADT**

- False
- The core standard library ADTs (List, Set, etc.) are not sealed — they’re open for extension

**4. The Java standard library does not provide any ADT implementations.**
- False
- The standard library provides many concrete ADT implementations, for example:
```
Interface	Implementation
List<E>   	ArrayList<E>, LinkedList<E>
Set<E>	        HashSet<E>, TreeSet<E>
Queue<E>	PriorityQueue<E>, ArrayDeque<E>
Map<K,V>	HashMap<K,V>, TreeMap<K,V>
```

**5. The Java standard library provides a bunch of high-quality ADT implementations. It is generally a good practice to reuse these in our programs (if their functionality fits the purpose).**
- True
- For example, instead of implementing your own linked list or hash map, you use ArrayList, HashMap, etc.



---

## Classes and Objects
**1.  are class members**
- Methods
- static methods
- constructors
- fields
- nested classes
...

**2. These are Not class members**
- Objects: they are not inside the class — instead created at runtime and stored in memory (heap), not within the class definition. 
- Values (see example below)
```java
class A {
  int x = 10;
}
// x is a class member (field), but 10 is not a class member — it is a value stored inside x
```

**3. Classes are data descriptions**
- True
**4. Classes are compilation units**
- True
- Even though Java files are compilation units (.java files), classes are also compilation units in the following sense:
- Every class is compiled separately into a .class file. 
- Each .class file is a compilation unit for the JVM.

---
## Interfaces 
**1. A concrete class may only implement (override) a subset of the methods of an interface. Thus, one can add methods to an interface without changing the definition of any concrete classes that implement the interface.**
- False
- Concrete classes must implement all non-default methods
- If we change the interface, adding an abstract method, we need to modify all concrete classes implementing it

**2. If a class only implements a partial subset of the methods of an interface, it must be declared as an abstract class**
- True

**3. Interfaces are another kind of reference type declaration. Thus one can have variables, function parameters, and return values of functions declared to be of an interface type**
- True

**4. Interfaces can be instantiated as they are implicitly concrete by definition.**
- False
- It is a contract of behaviour, no instantiation!

**5. A class may implement multiple interfaces. However, it can only extend a single class**
- True
- Multiple inheritance of types (interfaces) → allowed 
- Single inheritance of implementation (classes) → enforced

---
## Graphs
**1. Lists and trees are graphs.**
- True
- A list is just a graph where each node has at most one next node.
  A tree is just a connected acyclic graph.

**2. The only difference between trees and graphs is that graphs have loops.**
- False
- Trees differ from general graphs by: Having exactly n−1 edges for n nodes. Being connected. Being acyclic. Having a unique path between any two ...
- Also, graphs may not always have loops

**3. BFS naturally provides shortest paths from the initial vertex to any other (reachable) vertex in the graph.**
- True
- For unweighted graphs only

**4. BFS provides all possible shortest paths from the initial vertex and a given vertex.**
- False
- Default BFS keeps exactly one parent per node, so it outputs only one shortest path.

**5. The standard iterative implementations of DFS and BFS differ only in that one uses a stack and the other uses a map.**
- False
- Not even close, BFS uses a queue. Finding other differences left as an exercise for the reader

---

## Hash Functions

**1. Any function can be a hash function.**
- False
- A proper hash function must be deterministic: same input -> same output

**2. A good hash function distributes its return values evenly across its range.**
- True.

**3. A hash function must return different values for different inputs.**
- False
- Collisions can be unavoidable

**4. A hash function must return equal values for equal inputs.**
- True
- By definition of deterministic

**5. A function that always returns the same value is a valid hash function.*
 - True: it is deterministic
 - BUT Terrible

---


## Hash Tables
**1. If we know an identifier for each object, we can look it up instantly in an array.**

- True
- This is talking about direct addressing: If we have a unique integer ID k, and our array is large enough to index k, then the mapping is bijective


**2. There are multiple ways to deal with hash collisions.**
- True
- Chaining, open addressing, double hashing...

**3. When re-sizing a hash table, every element already in it stays in the same place.**
- False
- Resizing changes the capacity of the underlying array.
  Since `index = hash(key) % capacity`, changing capacity means: (a) Most elements get new bucket indices (b) Every element must be rehashed (c) The entire hash table is rebuilt

**4. When adding or removing an element to/from the hash table, every element already in it stays in the same place**
- This depends
- It is true for HashMaps, but when adding elements trigger a resize when load factor is exceeded, every element is rehashed, and none of them stay in the same place


---
## Tree Traversal

**1. DFS and BFS are the only two possible ways to traverse the nodes of a tree.**
- False.

**2. There are three variants of DFS for tree traversals**
- True (for binary trees)
- E.g. Inorder, Postorder, Preorder

**3. There cannot be two different trees for which DFS and BFS traverse the tree nodes in the same order.**
- False
- Example
```
Tree A: a chain 1→2→3
Preorder DFS: [1,2,3], BFS: [1,2,3]

Tree B: a star with root 1 and children 2,3 (left child first)
Preorder DFS: [1,2,3], BFS: [1,2,3]
Different structures; same DFS and BFS orders.
```
**5. Preorder DFS can only be implemented recursively.**
- False
- Iterative DFS using a stack

**6. BFS can be implemented iteratively with the help of a queue.**
- True

---
## Autoboxing 
**1. int and Integer can be automatically converted to each other.**
- True. 
- By definition.
```java
int a = 5;
Integer b = a;   // autoboxing
// The compiler inserts .valueOf() and .intValue() automatically.
Integer c = 10;
int d = c;       // unboxing
 
```
**2. If x and y are ints, and both represent the same number, x == y will always return true.**
- True
- For primitive int values: They store the numeric value directly, so `==` compares numeric equality. Java caches small integers:
Integers from –128 to 127 come from a shared cache. Integers outside this range are new objects. So 
```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b);   // true  (cached)

Integer c = 200;
Integer d = 200;
System.out.println(c == d);   // false (different objects)

```

**3. If x and y are Integers, and both represent the same number, x == y will always return true.**
- False.
- `Integer == Integer` compares object references, not numeric value.

**4. If x is an int, you can call x.toString()**
- False.
- `int` is a primitive.
  We cannot call methods on a primitive type.

**5. If x is an Integer, you can call x.toString().**
- True.
- Integer is an object.

---
## Functional Interface & Closures

**1. Two functional interfaces that specify a method with the same argument and return types can always be used interchangeably.**

- False.
- a lambda must match the exact functional interface type, not just the shape of the abstract method.
- Example
```java
@FunctionalInterface
interface A {
    int run(int x);
}

@FunctionalInterface
interface B {
    int run(int x);
}

A a = (x) -> x + 1;   // OK
B b = a;             // Compile error (A is not B)
```
**2. You can define your own functional interfaces.**
- True. 
- This is what they are created for.

**3. Every Lambda expression you write has to either have an explicit or Functional Interface type or be able to infer it from context**
- True. 
- Examples
```java
// explicit declaration
Runnable r = () -> System.out.println("hi");

// inferred from method params
public void doWork(Runnable r) {}
doWork(() -> System.out.println("hi"));  // Type inferred as Runnable

// inferred from generics
<T> void runAction(Supplier<T> s) {}
runAction(() -> 42);  // inferred as Supplier<Integer>

// But this is not okay
var x = () -> 5;   // ERROR: Java cannot infer functional interface 
// however it can be fixed as
Supplier<Integer> x = () -> 5;
// or 
var x = (Supplier<Integer>) (() -> 5);
```
**4. A lambda does capture local variables from the surrounding scope — but only if those variables are effectively final.**
- True
- A closure is a function (like a lambda) that “remembers” values from the environment in which it was created.
- Example
```java
int base = 10;   // effectively final

Supplier<Integer> s = () -> base + 5; // The lambda closes over the value 10 and stores it inside its compiled form.
```
**5. A lambda expression can mutate local variables defined in its context.**

- False.
- any local variable captured by a lambda must be effectively final.
- The following will not compile
```java
int x = 10;

Runnable r = () -> {
  x = x + 1;  // Compile error: x is not effectively final
};
// Local variables live on the stack, but lambdas may outlive the stack frame (e.g., used in another thread).
```
- But this compiles (Why? Because the referential link is effectively final although the internal state is mutable)
```java
int[] x = {10};     // array reference is final, but contents are mutable

Runnable r = () -> x[0]++;  // allowed

//also the following works too
class Box { int value; }

Box b = new Box();
Runnable r = () -> b.value++;  // allowed

```

---
## Complexity
**1. Studying the time complexity of an algorithm amounts to modelling how much time it spends when run on a particular computer**

- False.
- Time complexity is machine-independent.
  It measures how running time grows with input size, not how long it takes on a real computer.

**2. We use Big O notation to express the time and memory complexity of an algorithm**

- True. 
- Remember it expresses asymptotic complexities.

**3. An algorithm with two nested loops always has quadratic time complexity**

- False.
- Counterexamples: Inner loop that breaks early. Inner loop over constants. Inner loop depending on something other than n. Geometric halving loops → O(n log n) or O(n) like binary search

**4. An algorithm that performs a vast amount of operations independently of problem size has exponential time complexity**
- False.
- It is constant time.

**5. If an algorithm performs 8 times as many operations when we double problem size, it has O(n³) time complexity**
- True.
- If the runtime is such that `T(2n) = k * T(n)`, then `k = 2^d, d = log₂(k)`

---
## Exceptions
**1. You must always catch exceptions or have a throws clause in method signature.**

- False. 

- Checked exceptions must be: caught with try/catch, OR declared in throws
(Examples: IOException, ParseException). But unchecked exceptions Do NOT need to be caught or declared.
(Examples:RuntimeException (e.g., NullPointerException, IndexOutOfBoundsException, Error (e.g., OutOfMemoryError))


**2. Exceptions are always caught by the closest try-catch block in source code that has a matching catch clause**

- True. 

- How does this work? If an exception is thrown: The JVM searches outward from the throw point. Finds the nearest (innermost → outermost) try block, whose catch matches the exception type,
and handles it.

**3. Exceptions can be any class**

- False.

- In Java, an exception must be a subclass of `java.lang.Throwable.`
Legal exception types are `Exception`, `RuntimeException`, `Error`, and custom exceptions extending `Exception` or `RuntimeException`

**4. Error and RuntimeException are unchecked exceptions**

- True. They need not be explicitly thrown. 

**5. Functional interfaces need to specify the exceptions that lambdas implementing them may throw.**

- True. 
- Tricky: "A lambda may NOT throw new checked exceptions unless the interface declares them" is false!
- See example
```java
// This is good
@FunctionalInterface
interface MyFunc {
    void run() throws IOException;   // declared
}

MyFunc f = () -> {
    throw new IOException();  // must throw, because functional interfaced had it!
};

// This is incorrect
@FunctionalInterface
interface MyFunc {
    void run();   // no throws clause
}

MyFunc f = () -> {
    throw new IOException();  // compile error, where did this exception even come from? compiler confused
};

// Also, unchecked exceptions always fine 
MyFunc f = () -> {
    throw new RuntimeException("oops");  // always allowed, even functional interface did not specify it
};

```
---
## Packages

**1. The default package is just like any other package** 
- False. 
- Default package is the root package ( for example, everything under the /src). There is no name, we cannot import it. 
It can access any other package in the real packages, but no real packages can access it. 
This asymmetric visibility does not generalize to all packages.

**2. Packages depend only on the package declaration in a Java file**
- False. 
- A real Java package depends on BOTH:
The package ...; declaration at the top of the file, AND
The corresponding folder structure (relative to the classpath)

**3. Packages mirror the directory structure of the source/class file**
- True. See previous. 

**4. The class path is the directory where the java file is installed.**
- False. 
- The class path IS: (a) a search path for .class files (b) set using -cp or CLASSPATH
(c) usually “out/production/yourProject” when using IntelliJ, and 
(d) can include JARs or multiple folders

**5. The class path is a collection of roots where Java package directory trees may be found.**

- True, see previous. 