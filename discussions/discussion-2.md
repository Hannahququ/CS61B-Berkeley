# Discussion 2

## 1. Array -- Selection Sort

### \(1\) mystery method

Method mystery takes an array of intergers and an interger as arguments, and returns an integer.

```java
public static int mystery(int[] inputArray, int k){
    int x = inputArray[k]; // x = the item of k index in array = 4
    int answer = k; 
    int index = k + 1; 
    while (index < inputArray.length) {  
        if (inputArray[index] < x) { 
            x = inputArray[index];                
            answer = index;                        
        }
        index = index + 1; 
    }
    return answer;
}
```

1.  inputArray = \[3, 0, 4, 6, 3\] and k = 2, answer = 4
2. find the smallest index after point k \(including k\) in inputArray, and return the smallest item's index.

### \(2\) mystery2 method -- using mystery

Method mystery2 takes an array of integers and returns nothing.

```java
public static woid mystery2(int[] inputArray) {
    int index = 0;
    while (index < inputArray.length) {
        int targetIndex = mystery(inputArray, index); //use the mystery method conclusion
        int temp = inputArray[targetIndex];
        inputArray[targetIndex] = intputArray[index]; //change the order of the array
        inputArray[index] = temp; //change the order
        index = index +1;
    }
}
```

1.  inputArray = \[3, 0, 4, 6, 3\], answer = \[0, 3, 3, 4, 6\]
2.  Sort the array: mystery2 method pick the smallest element, swap it with the current item.
3. 最小的值的index；最小的值；最小值的index放在\[0\]；把最小值给\[0\] index; index ++循环下一个值

