# CS61B Week 2

## Lecture 3 Testing

When you are writing programs, it's normal to have errors, and instead of using the autograder, we could write tests for ourselves.

We will write a test method `void testSort()` first to test a `sort()` method before we really implement the method.

### 1. Ad Hoc Testing

We could easily create a test, such as the code below, which will return nothing or the first mismatch of the provided arrays.

We should not use `!=` while comparing two array objects, using `!input[i].equals(expected[i])`because`!=` will simply compare the memory address pointed by the two variables.

```java
//Actual sort method
public class Sort {
	/** Sorts strings destructively. */
	public static void sort(String[] x) {
    
	}
}
```

```java
//Just to test the Sort.sort method works, this is test method
public class TestSort {
    /** Tests the sort method of the Sort class. */
    public static void testSort() {
        String[] input = {"i", "have", "an", "egg"};
        String[] expected = {"an", "egg", "have", "i"};
        Sort.sort(input); // after run, the input string need to change to meet the expected string
        
        for (int i = 0; i < input.length; i += 1) {
            if (!input[i].equals(expected[i])) {
                System.out.println("Mismatch in position " + i + ", expected: " + expected + ", but got: " + input[i] + ".");
                break;
            }// op: Mismatch in position 0, expected: an, but got: i.
        }
    }

    public static void main(String[] args) {
        testSort();
    }
}
```

### 2. JUnit

With the JUnit library, our test method could be simplified to the following codes, output is pretty much same with Ad Hoc \(change for loop to just one line\)

```java
public static void testSort() {
    String[] input = {"i", "have", "an", "egg"};
    String[] expected = {"an", "egg", "have", "i"};
    Sort.sort(input);
    
    org.junit.Assert.assertArrayEquals(expected, input);
}
```

### 3. Selection Sort

Basic steps of selection sort a list of N items:

* Find the smallest item.
* Move it to the front.
* Selection sort the remaining N-1 items \(without touching the front item\).

#### **\(1\) Find the smallest item -- findSmallest\(\)**

Since `<` can't compare strings, we could use the `compareTo` method.

```java
//Actual findSmallest method
public class Sort {
    /** Sorts strings destructively. */
    public static void sort(String[] x) { 
           // (1) find the smallest item
           // (2) move it to the front
           // (3) selection sort the rest of the array (using recursion?)
           
           //(3.1)make some calls or glue two helper methods together (findSmallest and swap)
           int smallestIndex = findSmallest(x);
           swap(x, 0, smallestIndex);
           //(3)sort the rest of the array, start at position 1
    }
    
    

    /** Returns the index of the smallest string in x. */
    public static int findSmallest(String[] x) {
        int smallestIndex = 0;
        for (int i = 0; i < x.length; i += 1) {
            int cmp = x[i].compareTo(x[smallestIndex]);
         // if x[i] < x[smallestIndex], cmp will be -1
         // a < b, return -1, a = b, return 0, a >b, return 1
            if (cmp < 0) {
                smallestIndex = i;
            }
        }
        return smallestIndex;
    }
}
```

```java
//Just to test the findSmallest method works, this is test method
// Test the Sort.findSmallest method
public class TestSort {
    public static void testFindSmallest() {
        String[] input = {"i", "have", "an", "egg"};
        int expected = 2;

        int actual = Sort.findSmallest(input);
        org.junit.Assert.assertEquals(expected, actual);        

        String[] input2 = {"there", "are", "many", "pigs"};
        int expected2 = 1;

        int actual2 = Sort.findSmallest(input2);
        org.junit.Assert.assertEquals(expected2, actual2);
    }
    public static void main(String[] args) {
        testFindSmallest();    
    }
}
```

**\(2\) Move to the frong -- Swap**

```java
//Actual findSmallest method
public class Sort {
    /** Sorts strings destructively. */
    public static void sort(String[] x) { 
           // (1) find the smallest item
           // (2) move it to the front
           // (3) selection sort the rest (using recursion?)
    }
    
    /** (2) Swap item a with b*/
    public static void swap(String[] x, int a, int b) {
    String temp = x[a]; //creat temporary storage location --temp
    x[a] = x[b];
    x[b] = temp;
    }
    
    
    /** (1) Returns the smallest string in x. */
    public static String findSmallest(String[] x) {
        int smallestIndex = 0;
        for (int i = 0; i < x.length; i += 1) {
            int cmp = x[i].compareTo(x[smallestIndex]);
         // if x[i] < x[smallestIndex], cmp will be -1
         // a < b, return -1, a = b, return 0, a >b, return 1
            if (cmp < 0) {
                smallestIndex = i;
            }
        }
        return x[smallestIndex];
    }
}
```

```java
/** Test the Sort.swap method*/
public static void testSwap() {
    String[] input = {"i", "have", "an", "egg"};
    int a = 0;
    int b = 2;
    String[] expected = {"an", "have", "i", "egg"};

    Sort.swap(input, a, b);
    org.junit.Assert.assertArrayEquals(expected, input);
}
public static void main(String[] args) {
        testSwap();    
    }
```

#### \(3\) Recursive Array Helper Method

Since Java doesn't support array slicing \(`x[1:2]`\), we should add a helper method to recursively sort the whole array.

```java
public static void sort(String[] x) {
    sort(x, 0);
}

public static void sort(String[] x, int start) {
    smallestIndex = findSmallest(x);
    swap(x, start, smallestIndex);
    sort(x, start + 1);
}
```

However, the `findSmallest` method doesn't work well since it will start from 0 instead of the start point. We could easily fix it.

```java
public static int findSmallest(String[] x, int start) {
    int smallestIndex = start;
    for (int i = start; i < x.length; i += 1) {
        int cmp = x[i].compareTo(x[smallestIndex]);
        if (cmp < 0) {
            smallestIndex = i;
        }
    }
    return smallestIndex;
}
```

#### \(4\) Enhanced JUnit Test

To allow IntelliJ to automatically run the tests, we could modify our test structure as the following rules:

* Import the library `org.junit.Test`.
* Precede each method with `@Test` \(no semi-colon\).
* Change each test method to be non-static.
* Remove our main method from the `TestSort` class.

