# HW0

### Creative Exercise 1a: Drawing a Triangle

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

### Creative Exercise 1b: DrawTriangle

```java
public class TriangleDrawer {
    public static void drawTriangle(int N){
        int row = 0;
        int SIZE = N;
        while (row < SIZE){
            int col = 0;
            while (col < row){
                System.out.print("*");
                col += 1;
            }
            row += 1;
            System.out.println("*");
        }
    }
       
    public static void main(String[] args){
                drawTriangle(20);       
    }
}
```



