# Discussion 2

## 1. Array -- Selection Sort

### \(1\) mystery method

Method mystery takes an array of intergers and an interger as arguments, and returns an integer.

```java
public static int mystery(int[] inputArray, int k){
    int x = inputArray[k]; // x = the item of k index in array
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
        int targetIndex = mystery(inputArray, index);
        int temp = inputArray[targetIndex];
    }

```

