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
6. // for line comments, /\* and \*/ for block comments

### 3. HW 0: if...else if...else, while, define method\(function\), arrays, for loop, break and continue, 

## Lecture 2 Defining and Using Classes

### 1. Compilation/ Using Terminal \(Windows\)

#### Run java program \(two steps: javac & java\)

```java
$ ls //list the current file
HelloWorld.java
$ javac HelloWorld.java //complie the .java file, turn it into .class
$ ls
HelloWorld.class    HelloWorld.java
$ java HelloWorld //run HelloWorld
HelloWorld!
$ rm HelloWorld.class // remove the compiled .class, then can't run
$ cat HelloWorld.java // show the specific code
```

### 2. Defining Classes

* Every method is associated with some class.
* To run a class, we must define a main method.

```java
public class Dog {
    public static void makeNoise() {
        System.out.println("Bark!");
    }
}
```

This code above can't be run directly because there's no main method.

```java
public class DogLauncher {
    public static void main (String[] args) {
        Dog.makeNoise();
    }
}
```

Calling the makeNoise method from another class \(class.method\) with main method, then can run!

```java
$ javac DogLauncher.java
$ java DogLauncher
Bark!
```

### 3. Object Instantiation

* Classes can contain not just methods, but also data, such as the `size` of each dog.
* Classes can be instantiated as objects. For example, we will create a single Dog class, and then create instances of this Dog.

#### \(1\) Here's a Dog class which provdes a blueprint of Dog objects.

```java
public class Dog {
    public int weightInPounds; // initiate a var
    
    //One integer constructor for dogs
    public Dog(int w) {
        weightInPounds = w;
    }
    
    public void makeNoise() { 
    //no static, because weightInPounds is a non-static var
        if (weightInPounds < 10) {
            System.out.println("yipyipyip!");
        } else if (weightInPounds < 30) {
            System.out.println("bark. bark.");
        } else {
            System.out.println("woof!");
        }
    }
}
```

```java
public class DogLauncher {
    public static void main(String[] args) {
        // Dog.makeNoise(); 
        // non-static method(makeNoise) can't be referred in static context
        Dog d = new Dog(); //reference type to initiate a var d
        d.weightInPounds = 25;
        d.makeNoise();  
    } // run, op: bark
}// create a dog, set weight, then let him make noise 
```

#### \(2\) Constructor

```java
public class DogLauncher {
    public static void main(String[] args) {
        Dog d = new Dog(25); 
        d.makeNoise();  
    } //create a constructor below Dog class
} //give new Dog an integer, the constructor will be called
```

#### \(3\) Terminology

```java
public class Dog {
    // Instance variable(can have as many as you want)
    public int weightInPounds; 

    // Constructor(similar to method, determine how to instantiate the class)
    public Dog(int startingWeight) { 
        weightInPounds = startingWeight;
    }

// Non-static method or Instance method: invoked by an instance of the class
// If the method need to use my instance var, the method must be non-static
    public void makeNoise() {
        if (weightInPounds < 10) {
            System.out.println("yipyipyip!");
        } else if (weightInPounds < 30) {
            System.out.println("bark. bark.");
        } else {
            System.out.println("woof!");
        }
    }
}
```

```java
public class DogLauncher {
    public static void main(String[] args) {
        Dog smallDog; // Declaration of a Dog var(m: var name/object/class)
        new Dog(20); // Instantiationof the Dog class as a Dog object
        smallDog = new Dog(5); // Instantiation and Assignment
        Dog hugeDog = new Dog(150); // Declaration. Instantiation, and Assignment
        smallDog.makeNoise(); // Invocate the method
        hugeDog.makeNoise(); // The dot notation 
    }
}
```

