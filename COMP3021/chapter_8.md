# Event Driven Programming and Animations

The basis of event driven programming is exactly that, events. Upon events happening, execute associated code. Usually for webs and apps.

Will need event handlers to capture the event.

To make a handler, you'll need an object that implements `EventHandler<ActionEvent>`.

For outer class, you are not allowed to make the class protected. For an inner class you can define it as protected.

```java
class Handler implements EventHandler<ActionEvent> {
  @Override
  public void handle(ActionEvent e) {
    System.out.println("hello");
  }
}

public class ButtonDemo extends Application {
  @Override //Override the start method in the application class
  public void start(Stage primaryStage) {
    Button button = new Button("Hello");
    Pane pane = new Pane();
    pane.getChildren().add(button);
    button.setOnAction(new Handler());
    //sets the handler to handle actions to the Button

    Scene scene = new Scene(pane);
    primaryStage.setTitle("ActionEvent Demo"); //Set stage title
    primaryStage.setScene(scene); //Place the scene in the stage
    primaryStage.show(); //Display the stage
  }
}
```

## Inner Class Listeners

The idea is to define a new listener class inside another class.

"Inner Class" means that the class is inside another class. The point of inner class is that so you can hide it from other class (sometimes, it's more of a design issue).

Even if the inner class is visible, if you want to create the inner class, you have to create an object the outer class object (the class that owns the inner class).

```java
public class OuterClass {
  private int a;
  public class InnerClass {
    public void func() {
      a = 10;
      System.out.println(a);
    }
  }
  public static void main (String[] args) {
    OuterClass outer = new OuterClass();
    OuterClass.InnerClass inner = outer.new InnerClass();
    inner.func();
  }
}
```

Methods in the inner class can reference it's outer class methods and variables, as the outer class has to be instantiated first before the inner class can exist (meaning that for sure it already exists).

When compiled, each class will get its own class files, even inner classes.

Inner classes **can be** declared as `static`.

```java
public class Haha {
  static public class Hehe{
    ...
  }
}
```

For static inner classes, you can instantiate the inner class without having to instantiate an outer class first.

So you can do the following:

```java
public class Demo {
  public static void main (String[] args) {
    Haha.Hehe hoho = new Haha.Hehe();
    // possible only if Hehe is a static inner class.
  }
}
```

> `static` keyword can only be used for inner class! Cannot use for outer class.

A class can be defined without giving a name to the class, this class is called an anonymous class.

```java
public class Handler implements EventHandler<ActionEvent> {
  public void func() {
    ...
  }
}
```

```
//is equivalent to
new EventHandler<ActionEvent>() {
  public void func() {
    ...
  }
}
```

This also works for inheritance.

The use of using this anonymous inner class is that you get to make classes without having to give a name to the class, for example a special class for a certain behaviour. But if you are only using it for standard use then there is no need.

You can further simplify this by using **lambda expressions**.

## Lambda Expressions

Given that there is only one parameter without an explicit data type, you can omit the parentheses for the function.

## Single Abstract Method (SAM) Interface

Lambda expressions can only be used for single methods, more than that and there will be compilation error.

A functional interface is an interface that only has one abstract method (SAM).

```java
public class Haha implements EventHandler<ActionEvent> {
  public void handle(ActionEvent e) {
    ...
  }
}

//Code Segment
Button button = new Button("Hi");
button.setOnAction(new Haha());

// Can be simplified to
Button button = new Button("Hi");
button.setOnAction(new EventHandler<ActionEvent>() {
  public void handle(ActionEvent e) {
    ...
  }
})

// Can use lambda expression to do this
Button button = new Button("hi");
button.setOnAction(e -> {
  ...
})

//Note this is also legal syntax
button.setOnAction(() -> {
  ...
})
// If there is no arguments then you can just do this
// Remember parentheses are only required on multiple arguments or no arguments
```
