# Finished Code

## List

### 1. IntList -- linked list

```java
public class IntList {
    public int first;
    public IntList rest;     
    
    public IntList (int f, InList r) { // constructor 
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

### 3. DLList -- linked list

### 4. AList -- array-based list

