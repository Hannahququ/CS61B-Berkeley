# Finished Code

## List

### 1. IntList -- linked list

```java
public class IntList {
    public int first;
    public IntList rest;     
    
    public IntList (int f, IntList r) { // constructor 
        first = f;
        rest = r;
    }   

	  /** Return the size of the list using recursion (prefer) */
	  public int size() {
			  if (rest == null) { //base case: rest is null, then size is 1
			  		return 1;
				}
				return 1 + this.rest.size();
		}

		/** Return the size of the list using no recursion! */
		public int iterativeSize() {
				IntList p = this; // create a pointer variable
				int totalSize = 0;
				while (p != null) { // iterate every element in p list one by one
						totalSize += 1;
						p = p.rest;
				}
				return totalSize;
		}

		/** Returns the ith item of this IntList. */
		public int get(int i) {
				if (i == 0) { // do it recursively, then need base case
						return first;
				}
				return rest.get(i - 1);
	  }

	  public static void main(String[] args) { // build list 5, 10, 15 backward
				IntList L = new IntList(15, null);
				L = new IntList(10, L);
				L = new IntList(5, L);

				System.out.println(L.size());
				System.out.println(L.iterativeSize());
				System.out.println(L.get(1)); // op: 10
	  }
} 
```

### 2. SLList -- linked list

```java
public class SLList {
    
    private static class IntNode { // nested class, generally on top
        public int item; 
        public IntNode next;
        public IntNode(int i, IntNode n) {
            item = i;
            next = n;
        }
    }
    
    /* The first item (if it exists) is at sentinel.next. */
    private IntNode sentinel; 
    private int size; // Fast size() method
    
    /** Creates an empty SLList*/  //constructor
    public SLList() { //set instance var to represent an empty list
        sentinel = new IntNode(63, null); 
        size = 0; //63 just a random number in order to hold something
    }
    
    /** Creates one item SLList*/  //constructor
    public SLList(int x) {
        sentinel = new IntNode(63, null); 
        sentinel.next = new IntNode(x, null); 
        size = 1;
    }
    
    /** Adds x to the front of the list*/
    public void addFirst(int x) {
        sentinel.next = new IntNode(x, sentinel.next);
        size += 1;
    }
    
    /** Return the first item in the list*/
    public int getFirst() {
        return sentinel.next.item;
    }
    
    /**Add an item to the end of the list*/ 
    public void addLast(int x) {
        size = size + 1;
        IntNode p = sentinel;
        
        while (p.next != null) {
            p = p.next;
        }
        p.next = new IntNode(x, null);
    }
    
    public int size() { // Fast size() method
        return size; //compute the size upfront and return it
    }
    
    public static void main(String[] args) {
        SLList L = new SLList(); // creates an empty list
        SLList L = new SLList(15); //create a list of one integer, namely 15
        L.addFirst(10); 
        L.addFirst(5);
        L.addLast(20);
        System.out.println(L.size());
        System.out.println(L.getFirst());
    }
}    
```

### 3. DLList -- linked list

```java

```

### 4. AList -- array-based list

