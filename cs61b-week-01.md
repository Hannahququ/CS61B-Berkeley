# CS61B Week 1

## Lecture 1 Intro, Hello World Java

### 1. Introduction

#### What is 61?

* Writing codes that runs efficiently. \(Algorithms and Data Structures\)
* Writing code efficiently.

### 2. HelloWorld & LargerDemo

```java
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("hello world");
	}
}
```

```java
public class LargerDemo {
	/** Returns the larger of x and y. */
	public static int larger(int x, int y) {
		if (x > y) {
			return x;
		}
		return y;
	}

	public static void main(String[] args) {
		System.out.println(larger(-5.5, 10));
	}
} 
```

1. All codes must be in class.
2. Curly braces and semi-colons.
3. Var must be declared a specific type before use it, and type can't change, so called static type,  eg: \(int x , int y\); int x = 1;
4. Type verified before code run, if has type issue, code won't run.
5. public static declare functions, functions must have return type \(int\) or void, `main` or `larger` is method \(function in class called method\) 

### 3. Conditional \(if, while\)

#### \(1\) if 

* if-else if-else clauses can be **nested** and **daisy-chained**. Nesting can build **decision trees**. Daisy-chaining can present more than two alternatives. Eg: find the max of three numbers.
* Even there is only one statement inside if, still use curly braces, to avoid bugs

```java
  if (x > y) {
      if (x > z) {
        maximum = x;
      } else {
        maximum = z;
      }
    } else if (y > z) {
      maximum = y;
    } else {
      maximum = z;
    }
```

## Lecture 2 Defining and Using Classes





