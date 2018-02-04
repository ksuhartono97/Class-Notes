# Extra Notes
Event Handler is an interface!! not a class, so when you do `new EventHandler` you are actually creating a new object that implements EventHandler!

`static` and `public` are interchangeable, they can be switched around anytime.

```java
interface Haha {
  void laugh (int n);
}

//To override a lambda expression, you need to check the parameter list
//Use that as the LHS of the lambda expression
//Then on the RHS of the arrow, you put all the statements.
public class TestLambda1 {
  static public void main(String[] args) {
    Haha h = n-> System.out.println ("Haha " + n);
    //This is a lambda expression, it gives you an object
    //You must keep it in a reference variable

    //To call laugh,
    h.laugh(5);
  }
}
```

```java
interface Hehe {
  int interesting(double c);
}

public class TestLambda2 {
  public static void main (String[] args) {
    Hehe h = c-> (int)(c + 123.456);
    //No need to put a return value as lambda expression automatically returns the
    //result of the operations.

    //To call:
    int retVal = h.interesting(0.123456);
    System.out.println("Return value: "+ retVal);
    //Return Value: 123
  }
}
```

When you see interfaces with only a single abstract method (SAM), you can use lambda expressions to simplify the usage.

If there are multiple parameters, you can do this `(param1, param2, param3, ...)`. You don't have to put the parameter types in, but you'll have to put in the brackets. And again if you don't have any parameters you can put `()` for the lambda expression.

`@FunctionalInterface` annotation checks whether the interface has more than 1 abstract method(is it SAM or not). If it isn't SAM then it will give an error.

`this.variable` in an anonymous class refers to the instance variable of the class outside of it instead of a variable of the anonymous class itself.

```Java
class Person {
  private String name;
  private int age;
  private int double salary;
  public Person (String name, int age, double salary) {
    this.name  = name;
    this.age = age;
    this.salary = salary;
  }
  //Assume there are getters and setters for all the data members

  public class LambdaFinal {
    public static void main (String[] args) {
      ArrayList<Person> personList = new ArrayList<>();
      personList.add(new Person("Desmond", 18, 10000));
      personList.add(new Person("Alex", 19, 15000));

      /*
          interface Predicate<T> {
            boolean test(T t);
          }
      */
      //The above is a generic interface

      Predicate<Person> predicate1 = t -> t.getAge() <= 18;
      for(Person p : personList) {
        boolean result = predicate1.test(p);
        System.out.println("Result: " + result);
      }  

      /*
          interface Function<T> {
            R apply(T t);
          }
      */
      Function<Person, Double> f = t -> t.getSalary() + 1000;
      for(Person p : personList) {
        Double result = f.apply(p);
        System.out.println("Result: " + result);
      }
    }
  }
}

//Note imports are not included here, but there are some imports needed
//for above code to run
```
