# Java Spring

XML : Extended Markup Library, looks like HTML with some extra tags. JSON : an even more simple version of data representation. Only `name : data`

An http protocol request usually consists sending a request, getting a response header and a response body.

## Service Consumer

Consumer issues requests (GET, PUT, POST).

- GET method, parameters put together with the URL
- POST method, embed parameters in the header, **not** in the URL

## Java Spring Framework

Framework is very similar to a library. A framework can be understood as you are given a skeleton of the code, you need to fulfill some parts of the code to make it work.

Hollywood principle: your class must create the components, and then the framework will call your component and the component must react accordingly.

### Inversion of Control

Basically reduce dependency by applying decoupling, so that other people can change out the component according to their needs.

POJO doesn't inherit from any other superclass (plain-old-java-object).

### Autowired

Use gradle, a sort of makefile for Java.

`.gradlew/ bootRun`
