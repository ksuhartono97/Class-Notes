# Design Patterns

## Architectural Patterns

### MVC : Model-View-Controller
View is the user interface part. The controller deals with linking the view and the model (in HTML this is the requests part). And the Model is the backend part.

The idea is to separate the view from the logic.

### Generic Layered Architecture
Very similar to information hiding in a sense. As each layer will only need to know a bit of information to implement it's functionalities. No need to know all the information.

### Repository Architecture
Used usually when we have a large workload with the data. So we can put all the code and data in the center and all the services access it.
