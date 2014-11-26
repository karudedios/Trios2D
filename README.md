Trios2D
=======

It is a simple, lightweight game engine for the web working over canvas

##How to Use

```javascript
var game = new Trios2D("selector", {
    init: function () {
        ...
    },
    render: function (canvasContext) {
        ...
    },
    update: function (delta) {
        ...
    }
});

game.start();
```
Create an Engine object with the canvas where the game will be rendered as the first parameter and an object containing these ther methods:

* `init`: The begin of the game logic. Here you can set things when the game begins (`#start`).
* `render`: Here you can render whatever into the context.
* `update`. here you can update the game logic.

Objects can be created to the game and those when added can perform its currents updates and renders independently;

```javascript
    init: function (engine) {
        var independentObject = new Trios2D.GameObject();
        independentObject.position = new Trios2D.Vector(30,15);
        independentObject.update = function (delta) {
            ...
        };
        independentObject.render = function (context) {
            renderthings(context, this.absolutePosition.x, this.absolutePosition.y);
            ...
        };

        engine.addChild(independentObject);
    } 
```

Every object have its own childrens, so an object could be a container. An object which is made from other objects can be easyly done.

```javascript
var car = new Trios2D.GameObject();

car.wheels = [];

car.wheels[0] = new Trios2D.GameObject();
car.wheels[1] = new Trios2D.GameObject();
car.wheels[2] = new Trios2D.GameObject();
car.wheels[3] = new Trios2D.GameObject();

for (var wheel in car.wheels) {
   car.addChild(wheel);
}

game.addClild(car);
```
___

##Built-in Objects

Trios2D has some objects to work with the engine, some of them are:

###Vector

A `Vector` is simply a vector. It encapsulates *x* and *y* values and offer a set of methods to make math with them as other utitlity methods.

To make a new `Vector` just call `new Trios2D.Vector(x, y)`, where `x` and `y` are the coordenates. You can also do it these other ways:

```javascript
var coords = [x, y];
var vec1 = new Trios2D.Vector(coords); // it can take an array as parameter.
                                       // this way coors[0] is x and coors[1]
                                       // is y.
```

And this way:

```javascript
var coords = {x: 0, y: 0};
var vec1 = new Trios2D.Vector(coords); // Here coords.x is x and coords.y is y
```

####Methods

As mentioned before the an `Vector` object has some utility methods. Currents are:

* `#add(otherVector)`: This method return a new vector made by the addition of these two vectors.

* `#sub(otherVector)`: This method return a new vector made by the substraction of these two vectors.

* `#multiply(scalar)`: This method return a new vector made by the product of this vector and an scalar.

* `#divide(scalar)`: This method return a new vector made by the quotient of this vector and an scalar.

* `#invert()`: Return an inverted vector (`x` and `y` values are inverted).

* `#getAbsoluteValue()`: returns the absolute value from the vector (obtained by the pythagorean theorem).

* `#lerp(to, by)`: Linear interpolation. Return an interpolated vector from the current `Vector`object to the `to` vector by the `by` fraction.

* `#isBetween(vector1, vector2)`: Returns `true` if the current vector is in between `vector1` and `vector2` coordenates.


####GameObjects

You read about them above, dey are object made to work togueder in the game and interact. That way you can reduce your game logic to just objects interacting with each other.

A `GameObject` can be made this way: `new Trios2D.GameObject()`.

A game object has a `position` which is a `Vector` and is relative to the parent.

//TODO: Complete GameObject documentation and then the Engine it self

##Modules

Trios2D has modules built in, making easy thing like images managing or animations. It isn't very complete yet, but it is growing. All the modules are Game Objects and you can treat them as it. Modules are in the `./modules` folder.

###Some Modules

####GameImage

It is a module to manage images. It implements the render and update methods so you just have to specify the image and the size and it will make the work for you.

To include it you must import the `./modules/GameImage.js` script.

```html
<script src="js/Trios2D.js"></script>
...
<script src="js/modules/GameImage.js"></script>
```

To make a new image use `new Trios2D.GameImage(image, size)` where image is an `HTMLImage` Object or a source string. If the browser supports data url GameImage too. The `size` is an `Vector` object, an object containing `{x: 0, y: 0}` or even an array `[x, y]`.

If you are working with sprites you can make the `GameImage` this way: `new Trios2D.GameImage(image, clipStart, size)`. Here `clipStart` is where to start trimming the image, and the size is how much to trim. The same as `size`, `clipStart`can be a `Vector` and object or an array.

//TODO: Complete GameImage Documentation and other models as Components
