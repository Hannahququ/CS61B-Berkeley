# CS61B Week 2

## Lecture 3 Testing

When you are writing programs, it's normal to have errors, and instead of using the autograder, we could write tests for ourselves.

We will write a test method `void testSort()` first to test a `sort()` method before we really implement the method.

### 1. Ad Hoc Testing

We could easily create a test, such as the code below, which will return nothing or the first mismatch of the provided arrays.

We should not use `!=` while comparing two array objects, using `!input[i].equals(expected[i])`because`!=` will simply compare the memory address pointed by the two variables.

```java
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

With the JUnit library, our test method could be simplified to the following codes, output is pretty much same with Ad Hoc

```java
public static void testSort() {
    String[] input = {"i", "have", "an", "egg"};
    String[] expected = {"an", "egg", "have", "i"};
    Sort.sort(input);
    
    org.junit.Assert.assertArrayEquals(expected, input);
}
```

### 3. Selection Sort

Basic steps of selection sort:

* Find the smallest item.
* Move it to the front.
* Selection sort the remaining N-1 items \(without touching the front item\).

**findSmallest\(\)**

Since `<` can't compare strings, we could use the `compareTo` method.

```java
public class Sort {
    /** Sorts strings destructively. */
    public static void sort(String[] x) { 
           // find the smallest item
           // move it to the front
           // selection sort the rest (using recursion?)
    }

    /** Returns the smallest string in x. */
    public static String findSmallest(String[] x) {
        String smallest = x[0];
        for (int i = 0; i < x.length; i += 1) {
            int cmp = x[i].compareTo(smallest);
            if (cmp < 0) {
                smallest = x[i];
            }
        }
        return smallest;
    }
}
```

Test the method above:

```java
public static void testFindSmallest() {
    String[] input = {"i", "have", "an", "egg"};
    String expected = "an";

    String actual = Sort.findSmallest(input);
    org.junit.Assert.assertEquals(expected, actual);        

    String[] input2 = {"there", "are", "many", "pigs"};
    String expected2 = "are";

    String actual2 = Sort.findSmallest(input2);
    org.junit.Assert.assertEquals(expected2, actual2);
}
```

**Swap**

```java
public static void swap(String[] x, int a, int b) {
    String temp = x[a];
    x[a] = x[b];
    x[b] = temp;
}
```

```java
public static void testSwap() {
    String[] input = {"i", "have", "an", "egg"};
    int a = 0;
    int b = 2;
    String[] expected = {"an", "have", "i", "egg"};

    Sort.swap(input, a, b);
    org.junit.Assert.assertArrayEquals(expected, input);
}
```

