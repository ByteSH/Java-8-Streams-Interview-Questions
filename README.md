# Java 8 Streams Interview Questions

---

#### Click :star: if you like it!!

Every contribution counts, no matter how small. Join me on this exciting journey of open-source collaboration and learning. Together, let's build something amazing! 🚀

---

## 📦 Shared DTO Classes

> **Note:** `Employee` is used from **Question 12** onward (Q12, Q13, Q14, Q15), and `Person` is used in **Question 16**.

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

**1. Write a Java program to demonstrate different ways to create a Stream in Java.**
The program should include the following examples:

1. Create an `IntStream` from an `int[]` array using `Arrays.stream()`.
2. Create a Stream from an `Integer[]` array using `Arrays.stream()`.
3. Create a Stream from a `List` using the `stream()` method.
4. Create a Stream using `Stream.of()`.
5. Create a Stream using `Stream.generate()` and print only 3 elements.

```java
import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {
        // 1. Stream from an int[] array
        int[] arr = {1, 2, 3, 4, 5, 6};
        Arrays.stream(arr).forEach(System.out::println);

        // 2. Stream from an Integer[] array
        Integer[] integer = {1, 2, 3, 4, 5};
        Arrays.stream(integer).forEach(System.out::println);

        // 3. Stream from a Collection
        List<Integer> list = Arrays.asList(10, 20, 30);
        list.stream().forEach(System.out::println);

        // 4. Stream using Stream.of()
        Stream.of("A", "B", "C").forEach(System.out::println);

        // 5. Stream using Stream.generate()
        Stream.generate(Math::random)
              .limit(3)
              .forEach(System.out::println);
    }
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

**11. Partition numbers into two separate lists: even and odd**

```java
import java.util.*;

void main(){

    List<Integer> numbers = Arrays.asList(10, 15, 20, 25, 30, 35);

    Map<Boolean, List<Integer>> partitioned =
            numbers.stream()
                    .collect(Collectors.partitioningBy(n -> n % 2 == 0));

    System.out.println("Even numbers: " + partitioned.get(true));
    System.out.println("Odd numbers: " + partitioned.get(false));
}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**12. Sort a list of Employee objects by their salary**

```java
import java.util.*;

void main(){

    List<Employee> employees = Arrays.asList(
        new Employee(1, "Hamza", "IT", 50000),
        new Employee(2, "Ali", "HR", 40000),
        new Employee(3, "Sara", "Finance", 60000)
    );

    employees.stream().sorted(Comparator.comparing(Employee::getSalary)).forEach(System.out::println);   // Ascending.
    employees.stream().sorted(Comparator.comparing(Employee::getSalary).reversed()).forEach(System.out::println);  // Descending.

}
```

**[:top: Scroll to Top](#java-8-streams-interview-questions)**

---

**13. Group employees by department and calculate the average salary for each department**

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

**14. Find the highest-paid employee in each department**

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

**15. Departments with More Than 1 Employee**

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

**16. Calculate the average age of a list of Person objects**

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
