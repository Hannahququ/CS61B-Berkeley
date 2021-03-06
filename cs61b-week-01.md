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
		System.out.println("Hello World!");
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
4. Type will be verified before code run, if it has type issue, code won't run.
5. public static declare functions, functions must have return type \(int\) or void, `main` or `larger` are methods \(function in class called method\) 
6. // for line comments, /\* and \*/ for block comments

### 3. HW 0: if...else if...else, while, define method\(function\), arrays, for loop, break and continue, 

## Lecture 2 Defining and Using Classes

### 1. Compilation/ Using Terminal \(Windows\)

#### Run java program \(two steps: javac & java\)

```bash
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
* To run a class, we must define a main method, methods can be invoked by main method of another class
* A class that uses another class is sometimes called a "client" of that class, `DogLauncher` is a client of `Dog`.
* methods and variables are members of class

```java
public class Dog {
    public static void makeNoise() {
        System.out.println("Bark!");
    }
}
```

This code above can't be run directly because there's no `main` method.

```java
public class DogLauncher {
    public static void main (String[] args) {
        Dog.makeNoise();
    }
}
```

Calling the `makeNoise` method \(class.method\) from another class `DogLauncher`with `main` method, then can run!

```java
$ javac DogLauncher.java
$ java DogLauncher
Bark!
```

### 3. Object Instantiation

* Classes can contain not just methods, but also data, such as the `size` of each dog.
* Classes can be instantiated as objects. For example, we created a single Dog class, and then create instances of this Dog, eg: Dog d = new Dog\(\);

#### \(1\) Here's a Dog class which provides a blueprint of Dog objects.

```java
public class Dog {
    public int weightInPounds; // class contains variables=objects
    // Instance variable(can have as many as you want)
    
     //(2)One integer constructor for dogs
    public Dog(int w) {
        weightInPounds = w;
    }  
    
    public void makeNoise() { //class contains methods
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
        // Dog.makeNoise() is wrong 
        // because non-static method(makeNoise) can't be referred in static context
        Dog d = new Dog(25); //reference type to initiate a var d under Dog class
        d.makeNoise();  
    } // run, op: bark
}// create a dog (d), set weight, then let him make noise 
```

#### \(2\) Constructor

Constructor tell java what to do when a program tries to create an instance of a class, similar to method

One interger constructor for Dog class, give d an integer, the constructor will be called

#### \(3\) Terminology

```java
public class DogLauncher {
    public static void main(String[] args) {
        Dog smallDog; // Declaration of a Dog var(m: var name/object/class)
        new Dog(20); // Instantiation of the Dog class as a Dog object
        smallDog = new Dog(5); // Instantiation and Assignment
        Dog hugeDog = new Dog(150); // Declaration. Instantiation, and Assignment
        smallDog.makeNoise(); // Invocate the method
        hugeDog.makeNoise(); // The dot notation 
    }
}
```

### 4. Static vs. Non-static\(Instance\) Methods

#### \(1\) Class mix with static and non-static methods -- compare two dogs: d1 and d2 

* **Static methods** are invoked by using the **class name**, eg: Dog.makeNoise\(\);
* **Instance methods** are invoked by using an **instance name**, eg: d.makeNoise\(\);
* Static methods can't access instance var \(weightInPounds\), but they are more simple to use
* Static methods \(maxDog\) must access instance var \(weightInPounds\) via a specific instance \(d1\), eg: if \(d1.weightInPounds &gt; d2.weightInPounds\)

`this` : Inside a method, use `this` refer to the current instance

```java
public class Dog {
    public int weightInPounds; 
 
    public Dog(int w) {
        weightInPounds = w;
    
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
    // m: ????????????????????????
    //Let the God of the dog to do the judgement, static version
    public static Dog maxDog(Dog d1, Dog d2){ //create a method called maxDog, return Dog
        if (d1.weightInPounds > d2.weightInPounds){
            return d1;
        }// d1, d2 are instance, so can call non-static var
        return d2;
    }// should have static, because in the next code, we invoke the method using the class name (Dog.maxDog(d, d2))

    //Let the specific dog(ifself) to do the judgement, non-static version
    public Dog maxDog(Dog d2){
        if (this.weightInPounds > d2.weightInPounds){
            return this;
        }
        return d2;
    }    
}
```

```java
public class DogLauncher {
    public static void main(String[] args) {
        Dog d = new Dog(15); 
        Dog d2 = new Dog(100);
        //static to call the method, result store in bigger instance of Dog class
        Dog bigger = Dog.maxDog(d, d2); 
        bigger.makeNoise();
        
        //non-static to call the method
        Dog bigger = d.maxDog(d2);  
        bigger.makeNoise();  
```

#### \( 2\) Static Varibles

Classes to have static var are properties inherent to the calss itself, rather than the instance. 

Static var should be accessed using the class name

```java
public class Dog {
    public int weightInPounds; 
    //the properties apply to all dogs
    public static String binomen = "Cans famliiaris";
    
    System.out.println(Dog.binomen);
    //when access static var, only use the class
```

### 5. Array of Objects

#### To create an array of objects:

* First use the new keyword to create the array
* Then use new again for each object that you want to put in the array

```java
Dog [] dogs = new Dog[2];
dogs[0] = new Dog(8);
dogs[1] = new Dog(20);
dog[0].makeNoise();
```

### 6. **Command Line Arguments**

public static void main\(String\[\] args\)**,** `String[] args`: a parameter that is passed to the main method.

```java
public class ArgsDemo {
// print out the 0th command line argument
    public static void main(String[] args) {
        System.out.println(args[0]);
    }
} //op: these
```

Arguments can be provided by the operating system to your program as ???command line arguments,??? and can be accessed using the `args` parameter in `main`. For example if we call our program from the command line like this `java ArgsDemo these are command line arguments`, then the `main` method of `ArgsDemo` will have an array containing the Strings ???these???, ???are???, ???command???, ???line???, and ???arguments???.

## 

### 



