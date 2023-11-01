# Lab04

## Static and Final: Singleton pattern

### The final keyword
The `final` keyword is a non-access modifier used for `classes`, `attributes` and `methods`, which makes them **non-changeable** (impossible to inherit or override).
It is useful when you want a variable to always store the same value, like PI (3.14159...).

Example:
```Java
public class Main {
  final int x = 10;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 25; // will generate an error: cannot assign a value to a final variable
    System.out.println(myObj.x);
  }
}
```
N.B. If all attributes of an object admits a single initialization only (i.e used the final keyword), the object is called **immutable object.** Good examples of immutable objects include `Integer` and `String` Objects.

```Java
String s1 = "abc";
String s2 = s1.toUpperCase();  // s1 does not change; the method returns a reference to a new object which can be accessed using s2 variable
s1 = s1.toUpperCase();         // s1 is now a reference to a new object
```
### What is a String Pool?
A string constant pool is a separate place in the heap memory where the values of all the strings which are defined in the program are stored. When we declare a string, an object of type String is created in the stack, while an instance with the value of the string is created in the heap. On standard assignment of a value to a string variable, the variable is allocated stack, while the value is stored in the heap in the string constant pool. It is a small cache that resides within the heap. Java stores all the values inside the string constant pool on direct allocation. This way, if a similar value needs to be accessed again, a new string object created in the stack can reference it directly with the help of a pointer. In other words, the string constant pool exists mainly to reduce memory usage and improve the reuse of existing instances in memory. When a string object is assigned a different value, the new value will be registered in the string constant pool as a separate instance. 

Let’s understand this with the following example:


> String str1 = "Hello"; 
>
> String str2 = "Hello";
>
> String str3 = "Class"; 

The following illustration explains the memory allocation for the above declaration: 
![String-Pool Image](https://media.geeksforgeeks.org/wp-content/uploads/20230620182846/Java-String-Pool-3-768.png)

One way to skip this memory allocation is to use the new keyword while creating a new string object. The ‘new’ keyword forces a new instance to always be created regardless of whether the same value was used previously or not. Using ‘new’ forces the instance to be created in the heap outside the string constant pool which is clear, since caching and re-using of instances isn’t allowed here. 

Let’s understand this with an example:

>
> String str1 = new String("John");
>
> String str2 = new String("Doe");
>
The following illustration explains the memory allocation for the above declaration:
![Using the new keyword](https://media.geeksforgeeks.org/wp-content/uploads/20230714112418/String-Pool-in-Java-660.png)


### == vs equals in java

Both `equals()` method and the `==` operator are used to compare two objects in Java. == is an operator and equals() is method. But == operator compares reference or memory location of objects in a heap, whether they point to the same location or not. Whenever we create an object using the operator new, it will create a new memory location for that object. So we use the == operator to check memory location or address of two objects are the same or not.

In general, both equals() and “==” operators in Java are used to compare objects to check equality, but here are some of the differences between the two: 
   1. The main difference between the .equals() method and == operator is that one is a `method`, and the other is the `operator`.
   2. We can use == operators for `reference comparison` (address comparison) and .equals() method for `content comparison`. In simple words, == checks if both objects point to the same memory
      location  whereas .equals() evaluates to the comparison of values in the objects.
   3. If a class does not override the equals method, then by default, it uses the `equals(Object o)` method of the closest parent class that has overridden this method.

Example:
```Java
// Java program to understand 
// the concept of == operator

public class Test {
	public static void main(String[] args)
	{
		String s1 = "HELLO";
		String s2 = "HELLO";
		String s3 = new String("HELLO");

		System.out.println(s1 == s2); // true
		System.out.println(s1 == s3); // false
		System.out.println(s1.equals(s2)); // true
		System.out.println(s1.equals(s3)); // true
	}
}

```

#### StringBuilder
StringBuilder in Java represents a mutable sequence of characters. Since the String Class in Java creates an immutable sequence of characters, the StringBuilder class provides an alternative to String Class, as it creates a mutable sequence of characters. 

Example:
```Java
// Java Code to illustrate StringBuilder

import java.util.*;
import java.util.concurrent.LinkedBlockingQueue;

public class GFG1 {
	public static void main(String[] argv) throws Exception
	{
		// Create a StringBuilder object
		// using StringBuilder() constructor
		StringBuilder str = new StringBuilder();

		str.append("GFG");

		// print string
		System.out.println("String = " + str.toString());

		// create a StringBuilder object
		// using StringBuilder(CharSequence) constructor
		StringBuilder str1
			= new StringBuilder("AAAABBBCCCC");

		// print string
		System.out.println("String1 = " + str1.toString());

		// create a StringBuilder object
		// using StringBuilder(capacity) constructor
		StringBuilder str2 = new StringBuilder(10);

		// print string
		System.out.println("String2 capacity = "
						+ str2.capacity());

		// create a StringBuilder object
		// using StringBuilder(String) constructor
		StringBuilder str3
			= new StringBuilder(str1.toString());

		// print string
		System.out.println("String3 = " + str3.toString());
	}
}

```

Output

>
> String = GFG
>
> String1 = AAAABBBCCCC
>
> String2 capacity = 10
>
> String3 = AAAABBBCCCC
>


### The Static Keyword
The `static keyword` is a non-access modifier used for methods and attributes. Static methods/attributes can be accessed **without** creating an object of a class.

Example:

```Java

public class Main {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static methods can be called without creating objects");
  }

  // Public method
  public void myPublicMethod() {
    System.out.println("Public methods must be called by creating objects");
  }

  // Main method
  public static void main(String[ ] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); This would output an error

    Main myObj = new Main(); // Create an object of Main
    myObj.myPublicMethod(); // Call the public method
  }
}

```


