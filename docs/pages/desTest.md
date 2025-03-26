# Initial Design

[Home](/index.md)

The initial design I went with for this project was a simple struct and function based system. I decided to start this way as I believed it promoted rapid prototyping and it was easier to manage in the beginning.
Which is true, it was easier to get logic working with a loosely based system. I had a neat running project in a few days of iteration.

This what how my project was 'designed' intially.

<img src="https://raw.githubusercontent.com/jAlbright02/Digital_Rain_Cpp/main/docs/assets/images/structExample.png" >

You can see this is absolutely not ideal, it has inspiration for how a basic CRUD (create, read, update, delete) application is designed, instead of using getters, encapsulation (public and private functions/variables) and other benefits of having classes like inheritance.

# Issue

### However

When it came time to refactor, because I knew it was absolutely necessary to use a class with functions and variables, I had to do a lot of work to get it working. Probably ended up having to do more than if i had started out with this design.

Because it was dififcult to just 'do' this refactor, I made a UML (Unified Modeling Language) Class diagram to give myself more structure and so I didn't get lost in all of the redesigning.

Here I've attached my diagram

<img src="https://raw.githubusercontent.com/jAlbright02/Digital_Rain_Cpp/main/docs/assets/images/umlDiag.png" > 

### Attributes:
``x_pos (type: int)`` -> Represents the x position of the rain.

``y_pos (type: int)`` -> Represents the y position of the rain.

``rainLength (type: int)`` -> Represents the length of the rain.

``chars (type: std::vector<char>)`` -> A vector of characters representing the set of characters that can be used to display the rain.

### Methods:
#### Constructors:

``Rain()`` ->  Default constructor (initialises attributes with default values from initRain()).

``Rain(int, int, int, char)`` -> Constructor that takes four parameters: x and y positions, rain length, and a charset for the rain.

``Rain(int, int, int)`` -> Constructor that takes x and y positions and the rain length.

``Rain(int, int)`` -> Constructor that takes x and y positions.

``Rain(int)`` -> Constructor that takes just the rain length.

``Rain(char)`` -> Constructor that takes a single character (likely for charset).

#### Destructor:

``~Rain()`` -> Destructor, which likely cleans up the class when it is no longer needed.

### Helper Methods:

``updateRain()`` -> Updates the state of the rain, moving the rain down.

``resetRain()`` -> Resets the rain, re-initialises the object.

``isOffScreen()`` -> Checks whether the rain has gone off the screen.

``getXPos() getYPos() getRainLength()`` -> Getters that return the x and y positions, as well as the length of the rain.

``getChars()`` -> Returns the vector of characters (likely the charset used for rain).

Private Methods:

``initRain()`` -> Likely a helper method to initialize or set up the rain's properties (though not fully visible in the code provided).

This is what I used to keep myself focused during the next iteration of development.

# Fix and Implementation

### New Design

So after integrating this class, I looked through my other files to see if I could do the same. It ended up not being necessary, with one being entirely full of helper functions for things like the randomness of the Rain object values, and another designed to ``clearOldRain`` - replace the last first value with ``' '`` and ``displayRain`` - get the latest y position of the 'rainfall' and insert a random character there.   

### Multiparadigm Approach

#### What is Mutliparadigm Programming
["Multiparadigm programming languages ​​are those that allow different programming styles to be used in the same language. This means that a programmer can choose the most suitable approach to solve a specific problem, be it structured programming, object oriented or functional, among others."](https://tecnobits.com/en/What-is-a-multiparadigm-programming-language%3F/)

C++ is a multiparadigmed language, meaning I can use OOP (Object Oriented Programming) style, [procedural](https://hackr.io/blog/procedural-programming) or functional if I wanted to. I do use mainly 2 throughout this project. OOP is how my class is based with private variables, getters, public methods, constructors/destructors... The procedural aspect is how the program runs, which is in a while loop where a set of instructions are followed step by step.

I decided to not go down the route of overdesigning and making everything OOP, it was best to leave what works, working. The most important object got converted from a struct to a proper class and in my opinion (once I designed my UML diagram) which lead to cleaner code. Doing it for everything would have been extremely time consuming and convoluted. Simpler, sometimes, is better.
