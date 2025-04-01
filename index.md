---
---

By Ciara Crowe

## Setting up my Digital Rain
The first task I worked on was creating the constructors for my project. In order to produce the rain effect, I needed to have variables which took into consideration the screen's width and height. This is the first constructor I added:

```

  class DigitalRain {
public:
  DigitalRain();
  DigitalRain(int width, int height);
  DigitalRain(const DigitalRain&);
  ~DigitalRain();

```

This was my first change to my project, however I changed these variables later in my blog.

## Characters

My next step was to choose the characters that would be displayed as digital rain. I had the option to create a very specific set of characters and letters or I could choose a wide range of them. I decided to use a bunch of different characters to display my rain to mimic the movie 'The Matrix'.
In order to produce characters which were flexible, I decided to use the following: 


**std::uniform_int_distribution &lt;int&gt; u(x, y);**



I got my research from here, https://medium.com/@ryan_forrester_/c-random-string-generation-practical-guide-e7e789b348d4. 

X and Y were dependent on what characters I wanted to display whether it be ascii, numbers or uppercase characters. Using this distribution, I could use a random number generator engine to display the charcters. I used chat gpt to see what the best libraries were to update my code. This is the research I came back with:

	std::rand() -> Old c ++ way of programming
	std::random_device -> This is used mainly for hardware, but can be slow
	std::mt19937 -> This produces fast and high quality random numbers

 
To generate a different range of numbers I was gonna use the **std::mt19937** library as this was more relevent to what I was doing and seemed to be more advanced than the old C++ library **'rand()'**. To add this to my project i just needed to add the header file **#include random**. 

I wanted to create a function which would use the random engine generator in conjuction with my charset. I created a small function which would return a random set of ascii numbers: 

	char DigitalRain::GetRandomCharacter()
	{
    		return static_cast<int>(charset(engine_));
	}




 The static_cast converts the number generated into ascii code, casting the char. 



## First Attempt at Digital Rain



Now that I had my characters, I focused on the function to create the rain. I created a structure called Raindrop which would display the character, speed and x and y positions for the rain. 

Using the distribution generator, I created the column distance, chance, charset and screen. 

	std::uniform_int_distribution<int> column_dist;
	std::uniform_int_distribution<int> chance;
	std::uniform_int_distribution<int> charset;
	std::vector<std::string> screen;

I set the values for these in my constructors. The column distance focused on what distance the columns would be for the rain. Each raindrop would set 
a new column. It sets a new integer for each raindrop, making sure it stays in the range of width. Like the characters, the engine creates a random int between the numbers so that each raindrop appears in different areas of the screen. 

	new_drop.x_pos = column_dist(engine);

Before adding in chance, my rain drops ran all over the place. I needed to add code which would prevent creating raindrops constantly. I set my chance to be between 0, 10. Upon starting up the rain, the chance was set to 5, so that there was a 50% chance of the rain running. If I increased or decreased this number it would effect how much rain appeared on the screen. I decided to leave it at 5. I used AI to help me with this idea. 


As described above, charset uses the random number engine to genereate a random integer. In my constructors, I chose to return random numbers from 33 to 126 meaning that characters from '!' to '~' would be printed. Here I was able to choose what characters I wanted, https://www.geeksforgeeks.org/ascii-table/ .
Finally, screen focused on clearing the display and making sure the characters were stored properly. Without this, the screen wasn't clearning and the rain looked messy. In my constructures, I set screen to set a 2D grid to place characters, **screen = std::vector<std::string>(height, std::string(width, ' '));**. By placing the width and height in the vector, the current state of the screen is saved.

This is the raindrop structure I created:


	struct Raindrop {
		int x_pos;
		int y_pos;
		int characters;
		int speed;
	};
	std::vector<Raindrop> raindrops;


	
These are my constructors: 

 	DigitalRain::DigitalRain() : width(80), height(25), speed_(200) , 
	column_dist(0, width - 1), chance(0, 10), charset(33, 126)
	{
	#if VERBOSE
	std::cout << "Rain Default constructor" << std::endl;
	#endif
    	screen = std::vector<std::string>(height, std::string(width, ' '));
	rain_count_++;
	}


 This is my first attempt at Digital Rain.

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image2.png" width="400" height="300">

I used for loops to update and display the rain drops, whilst the character moved vertically down the screen. 

## Adding more characters in my Digital Rain
Currently, my rain displays one character at a time. I wanted to update this code so that three characters would be generated instead of one. To do this, I changed my characters in my raindrop structure from an int to a char of vectors so i could display multiple characters, **std::vector<char> characters;**. Since there was three characters now per raindrop, I introduced a for loop to display them, 



       for (int i = 0; i < 3; ++i) {
           new_drop.characters.push_back(GetRandomCharacter());
       }




I decided to use the **push_back** so the implementation could be more dynanmic, https://www.w3schools.com/cpp/ref_vector_push_back.asp. To ensure my characters were displayed vertically I added this for loop to my code, 

	for (size_t i = 0; i < drop.characters.size(); ++i) {
    	int pos_y = drop.y_pos - i;
     	}

I used a size_t type as this was recommended when working with my vector. I used the size function to return the number of charcters which was three, https://www.w3schools.com/cpp/ref_string_size.asp#:~:text=Definition%20and%20Usage,()%20-%20they%20behave%20the%20same. I created an int pos_y so that each charcter could be displayed vertically. In this for loop, character stays at the first position which is **y_pos**. Then they are displayed a row below eachother until i = 2. 
So while **y_pos** focuses on the position of the entire raindrop, **pos_y** focuses on the charcter of each position to create the vertical effect.


I was having a few errors where the drops were not appearing as expected. Some characters were not appearing in there vertical line so I added in a condition to make sure that the characters would be displayed at the correct positions. I added a for loop which ensured that the positions were not negative, and that the positions were less than the height, which was 25. Using the 2D screen grid, for the vertical position **pos_y**, and the column position **x_pos**, the characters are placed at different places over the screen, 

	if (pos_y >= 0 && pos_y < height) {
        screen[pos_y][drop.x_pos] = drop.characters[i];
	}

This was the result of my 3 character vector, 

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image7.png" width="400" height="300">

## Updating the DigitalRain to handle colour
It is clear that the rain is very basic and there is a lot more I can add to make it look better and to clean up my code. The first thing I want to change is the colours of the charcters falling. I decided it would be an interesting idea if the colour could change everytime the characters are updated on the screen. In order to add colour into my rain I decided to use the **#include windows.h**. I referenced this page, https://www.geeksforgeeks.org/how-to-change-console-color-in-cpp/. I decided to use the distribution object again to generate random colours like how I generated my characters, **std::uniform_int_distribution<int> choose_colour;**. I used the following function, 
**HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);**. This function is used to control the handle of the consoles output. By getting the handle I can set the handle to the colour I need. I created a getter and a setter for my random colours to do this. This is the outcome, 

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/code_recording5.gif" width="400" height="300">

## Adding a delay
In the above video, it is clear that the rain is much too fast even with changing the speed.
After research, I decided I needed a delay for the overall frame of the display, https://en.cppreference.com/w/cpp/chrono/duration. I added in, 

     std::this_thread::sleep_for(std::chrono::milliseconds(speed_));


I used two libraires, **#include chrono** which was responsible for how long I wanted my delay, for my case, milliseconds.  As the **speed** variable is created inside of the raindrop structure and would focus on the speed of each individual raindrop, I decided to create another variable called **speed_** which would focus on the speed of the rain effect. The second library I used was the **#include thread** which was responsible for the pause on the thread. 



## Final Product and cleanup

At the start of the project I created 2 local variables width and height, but instead I decided that I wanted to create member functions as this would allow the code to be reusable and encapsilating. 

	private:
	int width;
	int height;
	int speed_;
	std::mt19937 engine;


 This is my final product, 

 
<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image3.png" width="400" height="300">
<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image5.png" width="400" height="300">
<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image6.png" width="400" height="300">


 

 


