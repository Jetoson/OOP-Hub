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
`
String str1 = "Hello";
String str2 = "Hello";
String str3 = "Class";
`
The following illustration explains the memory allocation for the above declaration: 
![String-Pool Image](https://media.geeksforgeeks.org/wp-content/uploads/20230620182846/Java-String-Pool-3-768.png)

One way to skip this memory allocation is to use the new keyword while creating a new string object. The ‘new’ keyword forces a new instance to always be created regardless of whether the same value was used previously or not. Using ‘new’ forces the instance to be created in the heap outside the string constant pool which is clear, since caching and re-using of instances isn’t allowed here. 

Let’s understand this with an example:
`
String str1 = new String("John");
String str2 = new String("Doe");
`
The following illustration explains the memory allocation for the above declaration:
![Using the new keyword](https://media.geeksforgeeks.org/wp-content/uploads/20230714112418/String-Pool-in-Java-660.png)
