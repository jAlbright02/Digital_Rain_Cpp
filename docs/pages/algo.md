# Algorithms
This is my main algorithm, it calls on the Rain class and the Utils/Display files.

First we set the text colour in the terminal, then hide the cursor so the printing looks smoother without a white line blipping around.

In the main loop that runs for as long as the program is alive, we check the number of 'rain' in our rainfall. Here we want to make sure that there isn't too many on the screen as it can clutter up and look messy.
If there's space, we add another to the vector.

Then the displaying of the 'rain' is done.

````
setConsoleColor(10);
hideConsoleCursor();

std::vector<Rain> rainFall;

while (true) {

	if (rainFall.size() < 35) {
		Rain newRain;
		rainFall.push_back(newRain);
	}

	for (Rain& rainIterator : rainFall) {
		clearOldRain(rainIterator);
		rainIterator.updateRain();
		displayRain(rainIterator);
		if (rainIterator.isOffScreen()) {
			rainIterator.resetRain();
		}
	}

	waitForX(100);
}
````

## For every rain within our rainfall, we...

### Clear the rain

For each raindrop, it gets its previous y position (old_y) by subtracting 1 + i from the current position, moving the character upwards on the console. We then check if this new position is a valid Y position (meaning it isn't off-screen). If the position is valid, it moves the cursor to that spot using goToXY and clears the previous raindrop by printing a space character at that location, removing it from the display. 

````
for (int i = 0; i < rain.getRainLength(); ++i) {
    int old_y = rain.getYPos() - 1 - i;
    if (old_y >= 0 && old_y < cols) {
        goToXY(rain.getXPos(), old_y);
        std::cout << ' ' << std::flush;
    }
}
````

### Update the rain

This is all that's needed, we just want to advance the raindrop down towards the bottom of the console

``
y_pos += 1;
``

### Display the rain

It loops through each raindrop and calculates its new vertical position (y) by subtracting 'i' from the current Y position to move it down. We then check if this new 'y' position is valid. If it is valid, it moves the cursor to the corresponding 'x' and 'y' coordinates and prints a character, updating the screen to show the raindrop at its new position. The function `getChars()` is a vector so we access it's index using `[i]` 

````
for (int i = 0; i < rain.getRainLength(); ++i) {
    int y = rain.getYPos() - i;
    if (y >= 0 && y < cols) { 
        goToXY(rain.getXPos(), y);
        std::cout << rain.getChars()[i] << std::flush;
    }
}
````

### Reset the rain

First we look at if the vector of raindrop goes off screen by comparing the y position to the console height and the length of the rain

``
return y_pos >= cols + rainLength;
``

To reset we 're-initialise' the rain with random length, x position and character. This is done with functions from the `Utils` file. 

````
x_pos = randX();
y_pos = 0;
rainLength = randLength();
chars.clear();
for (int i = 0; i < rainLength; ++i) {
	chars.push_back(randChar());
}
````

## How are the random values are random?

I make use of the `<random>` library that's incldued with the C++ Standard Library.

Firstly, `std::random_device` provides a seed, which is the starting point for generating a random number, using either hardware/software-based randomness. Then, `std::mt19937`, which is a high-quality random number generator, is initialised with this seed and produces a sequence of random numbers. Finally, `std::uniform_int_distribution<>` takes these numbers and maps them to a specific range, ensuring that the numbers are evenly distributed.

I globally declare these as they are used in three separate functions and there is no need for individual declaration within each one.

``
static std::random_device rd;
static std::mt19937 gen(rd());
``

I then personalise the distribution for each. For example, in my random X value function, I want a range of 0 -> max size of the console width - 1.
So I can now print rain within the bounds of the terminal, making use of the space I have.
