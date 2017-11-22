# Graphical User Interfaces Programming

## Binding

Binding properties is useful for autoresizing of an object in the GUI when the window is resized.

`DoubleProperty` is necessary to bind a double variable. Meaning that if this type is used, the variable can be bound to some other thing, so that when one changes, the bound variable is also changed.

Other types like the above `DoubleProperty` is `IntegerProperty`

Unidirectional binding, in the case where B is bound to A. Then if object A changes, then object B changes. But the opposite doesn't apply. To do this, call the `bind` method

Whereas for bidirectional, changes to each side will change the other object. To do this, call the `bindBidirectional`.

> Both need a Property object as an argument

Note, when `d1.bind(d2)` is done, `d2` is the source, `d1` is the target.

Common methods:

- `setStyle` to change the style of the button, by giving it a special CSS.
- `setRotate` to rotate the object by an amount specified by the argument
