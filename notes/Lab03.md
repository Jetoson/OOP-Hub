# Lab03

## Aggregation and Inheritance

### Aggregation and Composition

#### Aggregation

It is a special form of Association where:
   - It represents **Has-A**’s relationship.
   - It is a unidirectional association i.e. a one-way relationship. For example, a department can have students but vice versa is not possible and thus unidirectional in nature.
   - In Aggregation, both the entries can survive individually which means ending one entity will not affect the other entity.

Examples of Aggregation in Java 
```Java

public class Foo { 
    private Bar bar;
 
    // The object of type Bar continues to exist even if the object Foo doesn't exist.
    Foo(Bar bar) {
       this.bar = bar; 
    }
}
```

```Java
final class Car {

  private Engine engine;

  void setEngine(Engine engine) {
    this.engine = engine;
  }

  void move() {
    if (engine != null)
      engine.work();
  }
}
```
In the example above, the **Car** performs its functions through an Engine, but the Engine is **not always** an internal part of the Car. Engines may be swapped, or even completely removed (i.e using setEngine method). Not only that, but the outside world can still have a reference to the Engine, and tinker with it regardless of whether it's in the Car. 


#### Composition
Composition is a restricted(strong) form of Aggregation in which two entities are highly dependent on each other.  
    - It represents **part-of** relationship.
    - In composition, both entities are dependent on each other.
    - When there is a composition between two entities, the composed object cannot exist without the other entity.

Examples of composition in Java
```Java
public class Foo {
    // The object of type Bar can't exist without the object Foo.
    private Bar bar = new Bar();
}
```

```Java
final class Car {

  private final Engine engine;

  Car(EngineSpecs specs) {
    engine = new Engine(specs);
  }

  void move() {
    engine.work();
  }
}
```
In the example above,the Engine is completely encapsulated by the Car. There is no way for the outside world to get a reference to the Engine. The Engine lives and dies with the car.

Insightful explanation from StacOverflow:
> Take a university that has 1 to 20 different departments and each department has 1 to 5 professors. There is a composition link between a University and its' departments. There is an aggregation
>  link between a department and its' professors.
>
> Composition is just a STRONG aggregation, if the university is destroyed then the departments should also be destroyed. But we shouldn't kill the professors even if their respective departments
>  disappear.
> 
The full code can be found below:

**Professor Class**
```Java
import java.util.ArrayList;
import java.util.List;

public class Professor {

    private final String name;
    private final List<Department> attachedDepartments = new ArrayList<>();

    public Professor(String name) {
        this.name = name;
    }

    public void destroy() {

    }

    public void join(Department d) {
        attachedDepartments.add(d);
    }

    public void quit(Department d) {
        attachedDepartments.remove(d);
    }

    public String getName() {
        return name;
    }

    @Override
    public String toString() {
        return "Professor " + name + " working for " + attachedDepartments.size() + " department(s)\n";
    }
}
```

**Department Class**
```Java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

public class Department {

    private final String name;
    private List<Professor> professors = new ArrayList<>();
    private final University university;

    public Department(University univ, String name) {
        this.university = univ;
        this.name = name;
        //check here univ not null throw whatever depending on your needs
    }

    public void assign(Professor p) {
        //maybe use a Set here
        System.out.println("Department hiring " + p.getName());
        professors.add(p);
        p.join(this);
    }

    public void fire(Professor p) {
        //maybe use a Set here
        System.out.println("Department firing " + p.getName());
        professors.remove(p);
        p.quit(this);
    }

    public void destroy() {
        //It's aggregation here, we just tell the professor they are fired but they can still keep living
        System.out.println("Destroying department");
        professors.forEach(professor -> professor.quit(this));
        professors = null;
    }

    @Override
    public String toString() {
        return professors == null
                ? "Department " + name + " doesn't exists anymore"
                : "Department " + name + "{\n" +
                "professors=" + professors.stream().map(Professor::toString).collect(Collectors.joining("\n")) +
                "\n}";
    }
}
```

**University Class**
```Java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

public class University {

    private List<Department> departments = new ArrayList<>();

    public Department createDepartment() {
        final Department dep = new Department(this, "Math");
        departments.add(dep);
        return dep;
    }

    public void destroy() {
        System.out.println("Destroying university");
        //it's composition, when I destroy a university I also destroy the departments. they cant live outside my university instance
        if (departments != null)
            departments.forEach(Department::destroy);
        departments = null;
    }

    @Override
    public String toString() {
        return "University{\n" +
                "departments=\n" + departments.stream().map(Department::toString).collect(Collectors.joining("\n")) +
                "\n}";
    }
}
```
**Driver test Class**
```Java
public class Test
{
    public static void main(String[] args)
    {
        University university = new University();
        //the department only exists in the university
        Department dep = university.createDepartment();
        // the professor exists outside the university
        Professor prof = new Professor("Raoul");
        System.out.println(university.toString());
        System.out.println(prof.toString());

        dep.assign(prof);
        System.out.println(university.toString());
        System.out.println(prof.toString());
        dep.destroy();

        System.out.println(university.toString());
        System.out.println(prof.toString());

    }
}
```
### Aggregation and Inheritance

#### Inheritance
In scenarios where classes have substantial similarities and disparities at the same time, inheritance offers a solution in the context of Object-Oriented Programming.
It implies an **is a** relationship. A good example would be a **Cat** class inheriting an **Animal** class.

#### Aggregation

In scenarios where one class uses another class as the data type of its attributes, aggregation (a.k.a composition) as a construct is involved.
It implies a **has a** relationship i.e. represents a **whole-part** relationship between objects. A good example would be a **Car** class having an **Engine** class inside of it.

##### When to use which? an excellent explanation from StackOverflow:

It's not a matter of which is the best, but of when to use what.
In the 'normal' cases a simple question is enough to find out if we need inheritance or aggregation.
    - If The new class is more or less as the original class. Use **inheritance**. The new class is now a subclass of the original class.
    - If the new class must have the original class. Use **aggregation**. The new class has now the original class as a member.

However, there is a big gray area. So we need several other tricks.
    - If we have used inheritance (or we plan to use it) but we only use part of the interface, or we are forced to override a lot of functionality to keep the correlation logical. Then we have a big nasty smell that indicates that we had to use aggregation.
    - If we have used aggregation (or we plan to use it) but we find out we need to copy almost all of the functionality. Then we have a smell that points in the direction of inheritance.

To cut it short. We should use aggregation **if part of the interface is not used or has to be changed to avoid an illogical situation**. We only need to use inheritance, **if we need almost all of the functionality without major changes**. And when in doubt, use Aggregation.

An other possibility for, the case that we have a class that needs part of the functionality of the original class, is to **split the original class in a root class and a sub class**. And let the new class inherit from the root class. But you should take care with this, not to create an illogical separation.

Lets add an example. We have a class **Dog** with methods: **Eat**, **Walk**, **Bark**, **Play**.
```Java
class Dog
  Eat;
  Walk;
  Bark;
  Play;
end;
```
We now need a class **Cat**, that needs **Eat**, **Walk**, **Purr**, and **Play**. So first try to extend it from a Dog.
```Java
class Cat is Dog
  Purr; 
end;
```
Looks, alright, but wait. This cat can **Bark** (Cat lovers will kill me for that). And a barking cat violates the principles of the universe. So we need to override the Bark method so that it does nothing.
```Java
class Cat is Dog
  Purr; 
  Bark = null;
end;
```

Ok, this works, but it smells bad. So lets try an aggregation:
```Java
class Cat
  has Dog;
  Eat = Dog.Eat;
  Walk = Dog.Walk;
  Play = Dog.Play;
  Purr;
end;
```
Ok, this is nice. This cat does not bark anymore, not even silent. But still it has an internal dog that wants out. So lets try solution number three:
```Java
class Pet
  Eat;
  Walk;
  Play;
end;
```
```Java
class Dog is Pet
  Bark;
end;
```
```Java
class Cat is Pet
  Purr;
end;
```
This is much cleaner. No internal dogs. And cats and dogs are at the same level. We can even introduce other pets to extend the model. Unless it is a fish, or something that does not walk. In that case we again need to refactor. But that is something for an other time.

![aggregation vs inheritance](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-9b3faa1d251e39a86f6bc3fa58e88b65_l3.svg)

### Upcasting and Downcasting
**Upcasting**: Upcasting is the typecasting of a child object to a parent object. Upcasting can be done **implicitly**. Upcasting gives us the flexibility to access the parent class members but it is not possible to access all the child class members using this feature. Instead of all the members, we can access some specified members of the child class. For instance, we can access the overridden methods.
**Analogy**: A child inherits his father.

**Downcasting**: Similarly, downcasting means the typecasting of a parent object to a child object. Downcasting cannot be implicit.
**Analogy**: A father may or may not inherit his/her child.

![upcasting vs downcasting](https://media.geeksforgeeks.org/wp-content/uploads/20200505231745/Upcasting-Vs-Downcasting.png)

Example:
```Java
// Java program to demonstrate
// Upcasting Vs Downcasting

// Parent class
class Parent {
	String name;

	// A method which prints the
	// signature of the parent class
	void method()
	{
		System.out.println("Method from Parent");
	}
}

// Child class
class Child extends Parent {
	int id;

	// Overriding the parent method
	// to print the signature of the
	// child class
	@Override void method()
	{
		System.out.println("Method from Child");
	}
}

// Demo class to see the difference
// between upcasting and downcasting
public class GFG {

	// Driver code
	public static void main(String[] args)
	{
		// Upcasting
		Parent p = new Child();
		p.name = "GeeksforGeeks";

		//Printing the parentclass name
		System.out.println(p.name);
		//parent class method is overridden method hence this will be executed
		p.method();

		// Trying to Downcasting Implicitly
		// Child c = new Parent(); - > compile time error

		// Downcasting Explicitly
		Child c = (Child)p;

		c.id = 1;
		System.out.println(c.name);
		System.out.println(c.id);
		c.method();
	}
}

```
![Explanation](https://media.geeksforgeeks.org/wp-content/uploads/20200506150009/Upcasting-Vs-Downcasting1.png)

#### `Instanceof`
Using `instanceof` in Java is not always "bad," but it can indicate potential design issues or anti-patterns. Here are reasons why `instanceof` might be seen as a bad practice:

1. **Violates the Open/Closed Principle**: If you're using `instanceof` to check types and then act on them, every time you add a new type, you might have to modify existing code. This can violate the Open/Closed Principle of object-oriented design which states that software entities should be open for extension but closed for modification.

2. **Breaks Polymorphism**: Using `instanceof` can be a sign that you're not making full use of polymorphism. Instead of asking an object what type it is and then acting on it, a better approach can often be to use polymorphism so that the object itself knows how to act.

3. **Decreases Code Maintainability**: Code that relies on `instanceof` checks can become hard to maintain. As your system grows and more types are added, you may find yourself adding more and more `instanceof` checks.

4. **Performance Concerns**: While modern JVMs are highly optimized, frequent use of `instanceof` might have performance implications, especially if it's being used in critical paths of an application.

5. **Type Casting**: Often after an `instanceof` check, you'll cast that object to the type you've just checked it against. This is redundant and can lead to potential runtime errors if not done carefully.

6. **Can Indicate Code Smells**: Frequent use of `instanceof` can be a sign of the "Switch Statements" code smell. In object-oriented design, it's often recommended to use polymorphism and inheritance over extensive branching logic based on type checks.

That said, there are legitimate cases where `instanceof` is useful, especially when dealing with external APIs or libraries where we don't have control over the design, or in certain patterns like the Visitor Pattern. The key is to understand its drawbacks and use it judiciously.

Here's a scenario where using instanceof becomes nearly **unavoidable**: When dealing with external libraries or frameworks where you receive objects of a base type and must determine their specific subtype. Let's consider the Java's Object method **equals(Object other)**. When you're overriding this method for a custom class, you often need to check if other is an instance of the current class.
Here's an example:
```Java
public class Circle {
    private int radius;

    public Circle(int radius) {
        this.radius = radius;
    }

    @Override
    public boolean equals(Object obj) {
        // Check if obj is an instance of Circle
        if (!(obj instanceof Circle)) {
            return false;
        }

        // Cast obj to Circle for comparison
        Circle otherCircle = (Circle) obj;
        return this.radius == otherCircle.radius;
    }

    // Other methods...
}

```
In this example, we're overriding the `equals` method for the `Circle` class. Since the signature of the `equals` method accepts an Object, we need to first check if the provided object is an instance of `Circle` before proceeding with our comparison. If we don't, and blindly cast it, we risk a `ClassCastException`.
This is a common scenario where using `instanceof` is not only acceptable but also recommended to ensure type safety.

### Java ArrayList

The `ArrayList` class is a resizable array, which can be found in the `java.util package`.
The difference between a `built-in array` and an `ArrayList` in Java, is that the size of an array cannot be modified (if you want to add or remove elements to/from an array, you have to create a new one). While elements can be added and removed from an ArrayList whenever you want. The syntax is also slightly different:

```Java
import java.util.ArrayList; // import the ArrayList class
ArrayList<String> cars = new ArrayList<String>(); // Create an ArrayList object
```
#### `ArrayList Methods`

| Methods           |	Descriptions
| :---------------- | :------------------------------------------------
| size()            | Returns the length of the arraylist.
| sort()            | Sort the arraylist elements.
| clone()           | Creates a new arraylist with the same element, size, and capacity.
| contains()        | Searches the arraylist for the specified element and returns a boolean result.
| ensureCapacity()  | Specifies the total element the arraylist can contain.
| isEmpty()         | Checks if the arraylist is empty.
| indexOf()         | Searches a specified element in an arraylist and returns the index of the element.



















