# Design Patterns

## Architectural Patterns

### MVC : Model-View-Controller

View is the user interface part. The controller deals with linking the view and the model (in HTML this is the requests part). And the Model is the backend part.

The idea is to separate the view from the logic.

### Generic Layered Architecture

Very similar to information hiding in a sense. As each layer will only need to know a bit of information to implement it's functionalities. No need to know all the information.

### Repository Architecture

Used usually when we have a large workload with the data. So we can put all the code and data in the center and all the services access it.

### Observer Patterns

Subject + Observer = Observer Pattern.

Loose coupling, two or more objects are able to interact with very little knowledge of each other. The point is that changes to either subject or observer will not affect each other.

### Mediator Pattern

Bob's Java enabled system : gets really hard to maintain all the rules, and adding new objects is very challenging on how to connect it in the system. The solution is using a mediator pattern.

Basically add elements and connect everything to the mediator. Uses a central control system design. However, this is bad as it is very tightly coupled. This pattern is good as long as the connected objects are of a small number.

### Object-oriented adapters

To bridge your code with a vendor's code, allowing two interfaces that are incompatible to be used together.

### Decorator pattern
Adds additional responsibilities to an object dynamically.

### Singleton pattern
Ensuring that a class has only one instance, and provides a global point of access to it.

Thread safe definition, define the singleton object in one line so that it is considered an atomic operation
