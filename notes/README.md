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
A Java string is a sequence of characters that exists as an object of the class **java.lang**. Java strings are created and manipulated through the string class. Once created, a string is **immutable -- its value cannot be changed.
A string is sequence of characters. A class is a user-defined template for creating an object. A string class is a user-defined template for creating and manipulating string objects, which are sequences of characters.



