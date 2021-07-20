# CS61B Week 3

## Lecture 6 DLList & Arrays

### 1. DLLists

### 2.Generic List

### 3. Arrays 

Recursive class build expandable list class: Intlist, SLList, DLList

Array build array-based list and AList -- How to build a list class using arrays

#### \(1\) Definition 

Array is a special kind of object which consists of a numbered sequence of memory boxes. Unlike class instances, which have named memory boxes.

An array consists of:

* A fixed integer `length`, N, cannot change!
* A sequence of N memory boxes where `N=length`, and all boxes hold the same type of value, which are numbered from 0 to `length-1`.

Arrays do not have methods

#### \(2\) Creation

Instantiate an array:

* get one reference at the time it's created
* if you reassign all variables containing that reference, you can never get the array back

Like classes, arrays are instantiated with `new`: \(three ways to create arrays\)

```java
int [] x;
int [] y;
(1) x = new int[3]; // fill each of the 3 boxes with the default int value 0.
(2) y = new int[]{1, 2, 3, 4, 5};
(3) int[] w = {9, 10, 11, 12, 13}; // no new, declare the var at the same time, can't ust it with an already declared var
```

**\(3\) Access and Modification**

```java
int[] z = null; // an reference to an int array
int[] x, y; // create two 64 bits boxes, an address goes in each of them

x = new int[]{1, 2, 3, 4, 5}; // new: find someplace in memory for five integers to live, 32 bits for each one
  // x records the location in memory of the whole five boxes
y = x; // copy the bits
x = new int[]{-1, 2, 5, 4, 99}; // won't change y
y = new int[3]; // throw away the old bits, the array is gone will never get back 
  // = an object is anonymous = lost the reference
z = new int[0];
int xL = x.length;

String[] s = new String[6]; // each 6 box is 64 bits, holds string reference, String default value is null 
s[4] = "ketchup";
s[x[3] - x[1]] = "muffins"; // based on x array to do the math = s[2]

int[] b = {9, 10, 11};
System.arraycopy(b, 0, x, 3, 2);
// copy from array b to array x, starts at position 0 of b, copy to position 3 of x
// copy two of those numbers from b
```

![](.gitbook/assets/1.png)

#### **\(4\) Copy Array**

Two ways to copy arrays:

1. Item by item using a loop.
2. Using `arraycopy`: Source array, start position in source, target array, start position in target, number to copy.

```java
int[] x = {9, 10, 11, 12, 13};
int[] y = new int[2];
int i = 0;
while (i < x.length) {
    y[i] = x[i];
    i += 1;
}
```

**\(5\) 2D Array**

We could create a 2-dimensional array with the following codes.

```java
// method 1
int[][] matrix;
matrix = new int[4][]; // creates one array, 4 rows
matrix = new int[3][4]; // creates five arrays, 3 rows, 4 columns
matrix[0] = new int[]{1}; // first row is {1}
// method 2
int[][] pascalAgain = new int[][]{{1}, {1, 1},{1, 2, 1}, {1, 3, 3, 1}};
```

#### **\(6\) Arrays vs. Classes**

data structure: list, set, map...

Both arrays and classes can be used to organize a bunch of memory boxes. **In both cases, the number of memory boxes is fixed**, i.e. the length of an array cannot be changed, just as class fields cannot be added or removed.

The key **differences** between memory boxes in arrays and classes:

* Array boxes are numbered and accessed using \[ \] notation, and class boxes are named and accessed using dot notation.
* Array boxes must all be the same type. Class boxes can be different types.
* Array index can be computed at runtime. Class member var names cannot be computed and used at runtime.

## Lecture 7 ALists, Resizing, vs. SLists

#### Limitation of DLists

Suppose we added `get(int i)`, which returns the ith item of the list. While we have a quite long DList, this operation will be significantly slow.

By instead, we could use Array to build a list without links.

#### Random Access in Arrays

Retrieval from any position of an array is very fast, which is independent of the size of it.

#### Naive AList Code

```text
public class AList {
    private int[] items;
    private int size;

    public AList() {
        items = new int[100];
        size = 0;
    }

    public void addLast(int x) {
        items[size] = x;
        size += 1;
    }

    public int getLast() {
        return items[size - 1];
    }

    public int get(int i) {
        return items[i];
    }

    public int size() {
        return size;
    }
}
```

Here are some invariants of this piece of code:

* The position of the next item to be inserted is always `size`.
* `size` is always the number of items in the AList.
* The last item in the list is always in position `size - 1`.

#### Delete Operation

```text
public int removeLast() {
    int returnItem = items[size - 1];
    items[size - 1] = 0;
    size -= 1;
    return returnItem;
}
```

#### Naive Resizing Arrays

The limitation of the above data structure is that the size of array is fixed.

To solve that problem, we could simply build a new array that is big enough to accomodate the new data. For example, we can imagine adding the new item as follows:

```text
public void addLast(int x) {
  if (size == items.length) {
    int[] a = new int[size + 1];
    System.arraycopy(items, 0, a, 0, size);
    items = a;  	
  }
  items[size] = x;
  size += 1;
}
```

The problem is that this method has terrible performance when you call `addLast` a lot of times. The time required is exponential instead of linear for SLList.

Geometric resizing is much faster: Just how much better will have to wait. \(This is how the Python list is implemented.\)

```text
public void addLast(int x) {
  if (size == items.length) {
	resize(size * 2);
  }
  items[size] = x;
  size += 1;
}
```

#### Memory Performance

Our AList is almost done, but we have one major issue. Suppose we insert 1,000,000,000 items, then later remove 990,000,000 items. In this case, we'll be using only 10,000,000 of our memory boxes, leaving 99% completely unused.

To fix this issue, we can also downsize our array when it starts looking empty. Specifically, we define a "usage ratio" R which is equal to the size of the list divided by the length of the `items` array. For example, in the figure below, the usage ratio is 0.04.

#### Generic Array

When creating an array of references to Item:

* `(Item []) new Object[cap];`
* Causes a compiler warning, which you should ignore.

The another change to our code is that we will delete an item by setting it to `null` instead of `0`, which could be collected by Java Garbage Collector.

## Lecture 8 Inheritance, Implements

