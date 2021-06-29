# Week 1

## Introduction

### What is 61?

* Writing codes that runs efficiently. \(Algorithms and Data Structures\)
* Writing code efficiently.

## First Java Program

### 1. HelloWorld & LargerDemo

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
3. Var must be declared a specific type before use it \(called static type\), and type can't change, eg: \(int x , int y\);
4. Type verified before code run, if has type issue, code won't run.
5. public static declare functions, functions must have return type \(int\) or void, `main` or `larger` is method \(function in class called method\) 



