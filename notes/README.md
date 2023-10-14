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

### 






