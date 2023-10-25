# Lab01
## Java Basics

### Packages
A package in Java is used to group related classes. Think of it as **a folder in a file directory**. We use packages to avoid name conflicts, and to write a better maintainable code. Packages are divided into two categories:
   ** Built-in Packages (packages from the Java API)
   ** User-defined Packages (create your own packages)

#### Built-in Packages
The Java API is a library of prewritten classes, that are free to use, included in the Java Development Environment.
The library contains components for **managing input**, **database programming**, and much much more. The complete list can be found at Oracles website: https://docs.oracle.com/javase/8/docs/api/.
The library is divided into packages and classes. Meaning you can either import a single class (along with its methods and attributes), or a whole package that contain all the classes that belong to the specified package.
To use a class or a package from the library, you need to use the import keyword:
```Java
import package.name.Class;   // Import a single class
import package.name.*;   // Import the whole package
```

#### User-defined Packages
To create your own package, you need to understand that Java uses a file system directory to store them. Just like folders on your computer:
```
└── root
  └── mypack
    └── MyPackageClass.java
```
To create a package, use the package keyword:
```Java
package mypack;
class MyPackageClass {
  public static void main(String[] args) {
    System.out.println("This is my package!");
  }
}
```

### Defining a Class in Java
Java provides a reserved keyword class to define a class. The keyword must be followed by the class name. Inside the class, we declare methods and variables.
In general, class declaration includes the following in the order as it appears:
    I. **Modifiers**: A class can be public or has default access.
    II. **class keyword**: The class keyword is used to create a class.
    III. **Class name**: The name must begin with an initial letter (capitalized by convention).
    IV. **Superclass** (if any): The name of the class's parent (superclass), if any, preceded by the keyword extends. A class can only extend (subclass) one parent.
    V. **Interfaces** (if any): A comma-separated list of interfaces implemented by the class, if any, preceded by the keyword implements. A class can implement more than one interface.
    VI. **Body**: The class body surrounded by braces, { }.
Syntax Example:

```Java
<access specifier> class class_name   
    {  
    // member variables   
    // class methods   
    }
```

### Java Primitives
Inspite of the factual assumption that everything in Java is an Object, the Java Programming Language actually features eight primitive data types.
These include **int**, **byte**, **short**, **long**, **float**, **double**, **boolean** and **char**. These aren’t considered objects and represent raw values.
They’re stored directly on the stack.

| Type 	   | Size(bits)  | Minimum 	            | Maximum 	                                    | Example                        |
| :------: | :---------: | :------------------: | :-------------------------------------------: | :----------------------------  |
| byte 	   | 8 	         | -2<sup>7</sup> 	    | 2<sup>7</sup> – 1 	                          | byte b = 100;                  |
| short    | 16 	       | -2<sup>15</sup> 	    | 2<sup>15</sup> – 1 	                          | short s = 30_000;              |
| int 	   | 32 	       | -2<sup>31</sup> 	    | 2<sup>31</sup> – 1 	                          | int i = 100_000_000;           |
| long 	   | 64 	       | -2<sup>63</sup> 	    | 2<sup>63</sup> – 1 	                          | long l = 100_000_000_000_000;  |
| float 	 | 32 	       | -2<sup>-149</sup>   	| (2-2<sup>-23</sup>)*2<sup>127</sup>           | float f = 1.456f;              |
| double 	 | 64 	       | -2<sup>-1074</sup> 	| (2-2<sup>-52</sup>2-52)*2<sup>1023</sup>      | double f = 1.456789012345678;  |
| char 	   | 16 	       | 0	                  | 2<sup>16</sup> – 1                            | char c = ‘c’;                  |
| boolean  | 1 	         | – 	                  |   – 	                                        | boolean b = true;              |

N.B. **Wrapper classes** provide a way to use primitive data types (int, boolean, etc..) as objects.
The table below shows the primitive type and the equivalent wrapper class:
| Primitive Data Type  | Wrapper Class    |
| :------------------: | :--------------: |
| byte 	               | Byte             |
| short 	             | Short            |
| int 	               | Integer          |
| long 	               | Long             |
| float 	             | Float            |
| double 	             | Double           |
| boolean 	           | Boolean          |
| char 	               | Character        |

> Sometimes you must use wrapper classes, for example when working with Collection objects, such as ArrayList, where primitive types cannot be used (the list can only store objects):
>
```Java
ArrayList<int> myNumbers = new ArrayList<int>(); // Invalid
ArrayList<Integer> myNumbers = new ArrayList<Integer>(); // Valid
```
### Java Strings 
A Java string is a sequence of characters that exists as an object of the class **java.lang**. Java strings are created and manipulated through the string class. Once created, a string is **immutable** -- its value cannot be changed.
A string is sequence of characters. A class is a user-defined template for creating an object. A string class is a user-defined template for creating and manipulating string objects, which are sequences of characters.

Examples:
```Java
String greeting = "Hello world!"; // The preferred way of instantiating a string
String s1 = new String("Hello world!");
char[] ch = {'H', 'e', 'l', 'l', 'o', 'w', 'o', 'r', 'l', 'd', '!'}
```

##### Types of strings in Java
Java distinguishes between primitive strings and object strings:
1. **Primitive strings**: These are string literals or string calls from a nonconstructor context. A constructor is a special method used to initialize objects. Primitives are not objects and have no methods or properties. They are represented at the lowest level of language implementation.
2. **Object strings**. These are strings created using the new operator. Object strings create two objects, whereas primitives create just one. Object strings create the string literal and the variable to refer to it.
The two string types are stored in memory differently.

When a string literal is created, the Java virtual machine (JVM) checks the string pool to see if it already exists. The string constant pool is a memory area where strings are stored. If the value exists, the string primitive will occupy the existing value. If the value does not exist, the JVM creates a new string and adds it to the pool.

The string constant pool lives inside the memory heap. When an object string is created, the part between the double quotes goes into the string constant pool. The variable assigned to the string is stored in the stack and matched to the string inside the pool.

The memory heap provides global access to all data stored in the heap for the entire life of the Java application. All object values are stored in the heap, including string literals, which are stored in the string constant pool inside the heap. Primitive variables and references to strings are stored in the stack and are matched to values in the heap. 

![Meory Heap and Stack in Java](https://cdn.ttgtmedia.com/rms/onlineimages/stack_and_heap_memory-f.png)

### Access Modifiers
In Java, Access modifiers help to restrict the scope of a class, constructor, variable, method, or data member. It provides security, accessibility, etc to the user depending upon the access modifier used with the element

1. **Default Access Modifier**
When no access modifier is specified for a class, method, or data member – It is said to be having the default access modifier by default. The data members, classes, or methods that are not declared using any access modifiers i.e. having default access modifiers are accessible **only within the same package**.

2. **Private Access Modifier**
The private access modifier is specified using the keyword private. The methods or data members declared as private are accessible only within the class in which they are declared.
Any other class of the same package will not be able to access these members.Top-level classes or interfaces can not be declared as private because private means “only visible within the enclosing class”.
protected means “only visible within the enclosing class and any subclasses”
Hence these modifiers in terms of application to classes, apply only to nested classes and not on top-level classes

3. **Protected Access Modifier**
The protected access modifier is specified using the keyword protected.
The methods or data members declared as protected are accessible within the same package or subclasses in different packages.

4. **Public Access modifier**
The public access modifier is specified using the keyword public. 
    ** The public access modifier has the widest scope among all other access modifiers.
    ** Classes, methods, or data members that are declared as public are accessible from everywhere in the program. There is no restriction on the scope of public data members.

### Encapsulation
Encapsulation is a fundamental concept in object-oriented programming (OOP) that refers to the bundling of data and methods that operate on that data within a single unit, which is called a class in Java. Encapsulation is a way of hiding the implementation details of a class from outside access and only exposing a public interface that can be used to interact with the class.

In Java, encapsulation is achieved by declaring the instance variables of a class as private, which means they can only be accessed within the class. To allow outside access to the instance variables, public methods called getters and setters are defined, which are used to retrieve and modify the values of the instance variables, respectively. By using getters and setters, the class can enforce its own data validation rules and ensure that its internal state remains consistent.

Encapsulation is defined as the wrapping up of data under a single unit. It is the mechanism that binds together code and the data it manipulates. Another way to think about encapsulation is, that it is a protective shield that prevents the data from being accessed by the code outside this shield. 
    ** Technically in encapsulation, the variables or data of a class is hidden from any other class and can be accessed only through any member function of its own class in which it is declared.
    ** As in encapsulation, the data in a class is hidden from other classes using the data hiding concept which is achieved by making the members or methods of a class **private**, and the class is exposed to the end-user or the world without   providing any details behind implementation using the abstraction concept, so it is also known as a combination of **data-hiding** and **abstraction**.
    ** Encapsulation can be achieved by Declaring all the variables in the class as private and writing public methods in the class to set and get the values of variables.
    It is more defined with the setter and getter method.

### Java Arrays
Arrays are used to store multiple values in a single variable, instead of declaring separate variables for each value.
To declare an array, define the variable type with square brackets:

```Java

String[] cars;
String[] cars = {"Volvo", "BMW", "Ford", "Mazda"};
String string = new String[10]; // To declare strings with a certain dimension
int[] myNum = {10, 20, 30, 40};

```
### Java main() Method 

```Java

// Java Program to demonstrate the
// use of any other access modifier
// other than public
 
class Main {
    private static void main(String[] args)
    {
        System.out.println("I am a Geek");
    }
}

```
#### Static Keyword
It is a keyword that is when associated with a method, making it a class-related method. The main() method is static so that JVM can invoke it without instantiating the class. This also saves the unnecessary wastage of memory which would have been used by the object declared only for calling the main() method by the JVM.

### JavaDoc

JavaDoc tool is a document generator tool in Java programming language for generating standard documentation in HTML format. It generates API documentation. It parses the declarations ad documentation in a set of source file describing classes, methods, constructors, and fields.

Before using JavaDoc tool, you must include JavaDoc comments /**………………..*/ providing information about classes, methods, and constructors, etc. For creating a good and understandable document API for any java file you must write better comments for every class, method, constructor.

The JavaDoc comments is different from the normal comments because of the extra asterisk at the beginning of the comment. It may contain the HTML tags as well. 
```Java
// Single-Line Comment

/* 
* Multiple-Line comment
*/

/** 
* JavaDoc comment
*/
```

**JavaDoc Format**: – 
It has two parts: – a description which is followed by block tags.
Some Integrated Development Environments (IDE) automatically generate the JavaDoc file like NetBeans, IntelliJ IDEA, Eclipse, etc.

**Generation of JavaDoc**: – 
To create a JavaDoc you do not need to compile the java file. To create the Java documentation API, you need to write Javadoc followed by file name. 
```Java
javadoc file_name or javadoc package_name
```
After successful execution of the above command, a number of HTML files will be created, open the file named index to see all the information about classes.
##### JavaDoc Tags 
 | Tag 	      | Parameter 	 | Description                                                        |
 | :--------- | :----------- | :----------------------------------------------------------------- |
 | @author 	  | author_name  | describes an author                                                |
 | @param 	  | description  | provide information about method parameter or the input it takes   |
 | @see 	    | reference 	 | generate a link to other element of the document                   |
 | @version 	| version-name | provide version of the class, interface or enum.                   |
 | @return 	  | description  | provide the return value                                           |
 | @link      | reference    | inserts an inline link with a visible text labe                    |
 | @code      | reference    | used to refer certain part of the code without formatting it       |

JavaDoc Example:

```Java
/**
* Returns an image that represents a solved sudoku. 
* This method always returns immediately, whether or not the 
* image exists. It is a similar implementation to {@link solveTetris}
* located in the same suite of games. 
*
* @param  path an absolute path to the location of the starting image
* @param  name the name of the image that represents the solved sudoku
*/
public Image solveSudoku(String path, String name) {
    try {
        return solve();
    } catch (Exception e) {
        return null;
    }
}
```
### Coding Styles in Java
Coding style rules in Java are a set of guidelines and conventions that dictate how Java code should be written to ensure readability, maintainability, and consistency across projects and teams. 
These rules help make Java code more understandable and easier to work with. Some key aspects of coding style rules in Java include:

1. **Naming Conventions**:
   - Class names should be in CamelCase, starting with an uppercase letter (e.g., MyClass).
   - Variable and method names should be in camelCase, starting with a lowercase letter (e.g., myVariable, myMethod).
   - Constants should be in all uppercase with underscores (e.g., MAX_VALUE).

2. **Indentation and Formatting**:
   - Use consistent indentation with spaces or tabs (typically 4 spaces per level).
   - Curly braces should be on their own lines for classes, methods, and control structures.
   - Line lengths should be limited (usually 80-120 characters) to improve code readability.

3. **Comments and Documentation**:
   - Use meaningful comments to explain complex code sections or algorithms.
   - Include Javadoc comments to document classes, methods, and their parameters.
   - Avoid excessive or redundant comments that clutter the code.

4. **Code Organization**:
   - Organize code into packages and follow a logical directory structure.
   - Import only the necessary classes/packages and avoid using wildcard imports.
   - Group related methods and variables together within a class.

5. **Code Readability**:
   - Choose meaningful and descriptive variable and method names.
   - Keep methods and classes focused on a single responsibility (Single Responsibility Principle).
   - Avoid using overly complex or nested code structures.

6. **Error Handling**:
   - Properly handle exceptions using try-catch blocks and provide meaningful error messages.
   - Avoid catching generic exceptions unless necessary.

7. **Use of White Spaces**:
   - Add white spaces around operators and between elements to improve readability.
   - Use empty lines to separate logically distinct parts of the code.

8. **Coding Standards and Conventions**:
   - Adhere to the coding standards and conventions established by your organization or project.
   - Follow industry-standard best practices, such as those outlined in the Java Code Conventions.
