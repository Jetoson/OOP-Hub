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

































