# HW0

### Exercise 1a: Drawing a Triangle

```java
public class DrawATriangle {
    public static void main(String [] args){
        int row = 0;
        int SIZE = 5;
        while (row < SIZE){
            int col = 0;
            while (col <= row) {
                System.out.print("*"); //does not include an auto newline
                col += 1;
            }
            System.out.println(" "); //go to next line
            row += 1;
        }
    }
} //tested
```

### Exercise 1b: DrawTriangle

```java
public class TriangleDrawer {
   public static void drawTriangle(int N) {
      int row = 0;
      int SIZE = N;
      while (row < SIZE){
         int col = 0;
         while (col < row){ //no =
            System.out.print("*");
            col += 1;
         }
         System.out.println("*"); //has *
         row += 1;
      }
   }
   
   public static void main(String[] args) {
      drawTriangle(20);
   }
} //tested
```

### Exercise 2

```java
public class ClassNameHere {
    public static int max(int[] m) { 
    //function returns the max value of an int array, m is the array name
        int maxValue = m[0];
        for (int i = 1; i < m.length; i++){ //i = 1 is better than i = 0
            if (m[i] > maxValue){ // compare 2 and 9
                maxValue = m[i];
            }
        }
        return maxValue;
    }
    public static void main(String[] args) {
        int[] numbers = new int[]{9, 2, 15, 2, 22, 10, 6};
        System.out.print(max(numbers));
    }
} //tested
```

### 



