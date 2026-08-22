# Java 8 Streams Interview Questions

---

#### Click :star: if you like it!!

Every contribution counts, no matter how small. Join me on this exciting journey of open-source collaboration and learning. Together, let's build something amazing! 🚀

---

## 📦 Shared DTO Classes

> **Note:** `Employee` is used from **Question 11** onward (Q11, Q12, Q13, Q14), and `Person` is used in **Question 15**.

**Employee.java**

```java
public class Employee {
    private int id;
    private String name;
    private String department;
    private double salary;

    public Employee(int id, String name, String department, double salary) {
        this.id = id;
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    public int getId() { return id; }
    public String getName() { return name; }
    public double getSalary() { return salary; }
    public String getDepartment() { return department; }

    @Override
    public String toString() {
        return id + " - " + name + " - " + department + " - " + salary;
    }
}
```

**Person.java**

```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public int getAge() {
        return age;
    }
}
```

---

## 💻 Questions

**1. Ways to create a stream in Java (From Array, Collections, Arrays, Stream.of, Stream.generate)**

```java
import java.util.*;
import java.util.stream.*;

void main(){

    int[] arr = {1, 2, 3, 4, 5, 6};
    List<Integer> list = Arrays.stream(arr)
                                .boxed()
                                .toList();
    System.out.println(list);

    List<Integer> list = Arrays.asList(1, 2, 3);
    list.stream().forEach(System.out::println);

    String[] arr = {"A", "B", "C"};
    Arrays.stream(arr).forEach(System.out::println);

    Stream<Integer> stream = Stream.of(1, 2, 3);
    stream.forEach(System.out::println);

    Stream<Double> stream2 = Stream.generate(Math::random).limit(3);
    stream2.forEach(System.out::println);
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**2. Find the first number greater than 5 from a list**

```java
import java.util.*;
import java.util.stream.*;

void main(){

    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);

    IO.print(
        list.stream().filter((x) -> x > 10).findFirst().orElse(-1)
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**3. Count how many numbers are greater than 5 in a list**

```java
import java.util.*;
import java.util.stream.*;

void main(){

    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);

    IO.print(
        list.stream().filter((x) -> x > 5).count()
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**4. Find the sum or product of all numbers in a list using reduction**

```java
import java.util.*;
import java.util.stream.*;

void main(){

    List<Integer> list = Arrays.asList(1, 2, 3);

    IO.print(
        list.stream()
            .reduce(1, (a, b) -> a * b)
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**5. Find the maximum, minimum, and average**

```java
import java.util.*;
import java.util.stream.*;

void main(){

    List<Integer> list = Arrays.asList(2, 3, 4, 3, 4, 4, 2, 2);

    IO.print(
        list.stream()
            .mapToInt(x -> x)
            .average()
            .orElse(1)
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**6. Find distinct elements**

```java
import java.util.*;
import java.util.stream.*;

void main(){

    List<Integer> list = Arrays.asList(2, 3, 4, 3, 4, 4, 2, 2);

    IO.print(
        list.stream()
            .distinct()
            .toList()
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**7. Find the second highest number in a list**

```java
import java.util.*;

void main(){
    List<Integer> list = Arrays.asList(10, 20, 30, 40, 50);

    IO.println(
        list.stream()
            .distinct()
            .sorted(Comparator.reverseOrder())
            .skip(1)
            .findFirst()
            .get()
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**8. Join list elements which start with "A" in a comma-separated String**

```java
import java.util.*;

void main(){

    List<String> list = Arrays.asList("Apple", "Mango", "Awakado");

    IO.print(
        list.stream()
            .filter(s -> s.toLowerCase().startsWith("a"))
            .collect(Collectors.joining(", "))
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**9. Check if all numbers are positive & any number divisible by 3**

```java
import java.util.*;

void main(){

    List<Integer> list = Arrays.asList(2, 4, 6, 8, 9);

    boolean allPositive = list.stream()
                                .allMatch(x -> x > 0);

    boolean anyDivisibleBy3 = list.stream()
                                .anyMatch(x -> x % 3 == 0);

    System.out.println("All elements are positive: " + allPositive);
    System.out.println("Any element divisible by 3: " + anyDivisibleBy3);
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**10. Find the first non-empty string in a list**

```java
import java.util.*;

void main(){

    List<String> list = Arrays.asList("", "Banana", "");
    IO.println(
        list.stream()
            .filter((s) -> !s.trim().isEmpty())
            .findFirst()
            .get()
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**11. Sort a list of Employee objects by their salary**

```java
import java.util.*;

void main(){

    List<Employee> employees = Arrays.asList(
        new Employee(1, "Hamza", "IT", 50000),
        new Employee(2, "Ali", "HR", 40000),
        new Employee(3, "Sara", "Finance", 60000)
    );

    employees.stream()
                .sorted(Comparator.comparing(Employee::getSalary))
                .forEach(System.out::println);
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**12. Group employees by department and calculate the average salary for each department**

```java
import java.util.*;

void main(){

    List<Employee> employees = Arrays.asList(
        new Employee(1, "Hamza", "IT", 50000),
        new Employee(2, "Ali", "HR", 40000),
        new Employee(3, "Sara", "IT", 60000),
        new Employee(4, "John", "HR", 45000),
        new Employee(5, "Emma", "Finance", 70000)
    );

    Map<String, Double> avgSalaryByDept =
            employees.stream()
                        .collect(Collectors.groupingBy(
                            Employee::getDepartment,
                            Collectors.averagingDouble(Employee::getSalary)
                        ));

    System.out.println(avgSalaryByDept);
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**13. Find the highest-paid employee in each department**

```java
import java.util.*;

void main(){

    List<Employee> employees = Arrays.asList(
        new Employee(1, "Hamza", "IT", 50000),
        new Employee(2, "Ali", "HR", 40000),
        new Employee(3, "Sara", "IT", 60000),
        new Employee(4, "John", "HR", 45000),
        new Employee(5, "Emma", "Finance", 70000)
    );

    Map<String, Optional<Employee>> highestPaid =
        employees.stream()
                    .collect(Collectors.groupingBy(
                        Employee::getDepartment,
                        Collectors.maxBy(Comparator.comparing(Employee::getSalary))
                    ));

    highestPaid.forEach((dept, emp) ->
        System.out.println(dept + " -> " + emp.get())
    );
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**14. Departments with More Than 1 Employee**

```java
import java.util.*;

void main(){

    List<Employee> employees = Arrays.asList(
        new Employee(1, "Hamza", "IT", 50000),
        new Employee(2, "Ali", "HR", 40000),
        new Employee(3, "Sara", "IT", 60000),
        new Employee(4, "John", "HR", 45000),
        new Employee(5, "Emma", "Finance", 70000)
    );

    List<String> departments =
        employees.stream()
                    .collect(Collectors.groupingBy(Employee::getDepartment))
                    .entrySet()
                    .stream()
                    .filter(entry -> entry.getValue().size() > 1)
                    .map(Map.Entry::getKey)
                    .toList();

    System.out.println(departments);
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**15. Calculate the average age of a list of Person objects**

```java
import java.util.*;

void main(){

    List<Person> people = Arrays.asList(
        new Person("Hamza", 25),
        new Person("Ali", 30),
        new Person("Sara", 35)
    );

    double averageAge = people.stream()
                                .mapToInt(Person::getAge)
                                .average()
                                .orElse(0);

    System.out.println("Average Age: " + averageAge);
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**
