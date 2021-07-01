# Memorizing Point W1-W4

## Week1

### 1. Variables: must declare a static type=can't change the type                             \(m: var name=objects=class\)

### 2. Methods: must have return type, static/ non-static \(instance\) method

* **Static methods** are invoked by using the **class name**, eg: Dog.makeNoise\(\);
* **Instance methods** are invoked by using an **instance name**, eg: maya.makeNoise\(\);

### 3. Class: must have a `main` method to run, if it doesn't have main method, the methods can be invoked by main method of another class

### 4. Class contains methods \(non-static/instance method: makeNoise\) and variables=objects=instance of class \(weightInPounds and new Dog\(\)\)

Variables and methods of a class are also called members of a class, which access using dot

### 5. Class instantiation is almost always done using the `new` keyword,             eg: Dog d = new Dog\(\);

Dog d = new Dog \(25\) -- Declaration, Instantiation and Assignment

### 6. Constructor define the way of using instance of class \(Dog d = new Dog \(25\);\)

### 7. Arrays also instantiated using the `new` keyword

```java
Dog [] dogs = new Dog[2];
dogs[0] = new Dog(8);
dogs[1] = new Dog(20);
dog[0].makeNoise();
```

### 8. Static varibles should be accessed using the class name

