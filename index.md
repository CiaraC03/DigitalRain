---
---

By Ciara Crowe

## Setting up my Digital Rain
The first task I worked on was creating the constructors for my project. In order to produce the rain effect, I needed to have variables which took into consinder the screen's width and height. This is the first constructor I added:

```

  class DigitalRain {
public:
  DigitalRain();
  DigitalRain(int width, int height);
  DigitalRain(const DigitalRain&);
  ~DigitalRain();

```

This was my first change to my project, however I changed this later in my blog.

## Characters

My next step involved selecting the characters to be displayed as part of the digital rain effect. I had the option to create a very specific set of characters and letters or I could choose a wide range of them. I decided to use a bunch of different charcters to display my rain to mimic the movie The Matrix rain.
After a bit of research I saw that the main library in choosing what characters I wanted to set my rain to was: 


**std::uniform_int_distribution &lt;int&gt; u(x, y);**



X and Y were dependent on what characters I wanted to display whether it be ascii, numbers or uppercase characters. This flexibility allowed me to display a wide array of symbols instead of being limited to a specific one. 
I wanted to create a function which would generate the random symbols. I created a small function which would return a random set of ascii numbers: 

	char DigitalRain::GetRandomCharacter()
	{
    		return static_cast<char>(charset_(engine_));
	}





I chose to return random numbers from 33 to 126 meaning that characters from '!' to '~' would be printed. Here I was able to choose what characters I wanted, https://www.geeksforgeeks.org/ascii-table/ . The static_cast converts the number generated into ascii code, casting a char. 



## First Attempt at DigitalRain Effect


My fist plan was to find out how to update the sequence of numbers every time my rain ran. I used chat gpt to see what was best libraries I could use to update my code. This is the resaerch I came back with:

 
    
	std::rand() -> Old c ++ way of programming
	std::random_device -> This is used mainly for hardware, but can be slow
	std::mt19937 -> This produces fast and high quality random numbers

 
    



I decided to generate a different range of numbers I was gonna use the **std::mt19937** library as this was more relevent to what I was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. 



Now that I had decided on my numbers, I focused on the function to create the rain. I created a structure called Raindrop which would display the character, speed, x postion and the y position. 
Using the distribution generator I created the column distance, chance, charset and screen. I set the values for these in my constructors. The column distance focused on what distance the columns would be for the rain. Before adding in chance, my rain drops were ran all over the place. I set my change to be between 0, 10. Upon starting up the rain, the chance was set to 5, so that there was a 50% chance of the rain running. If I increased or decreased this number it would effect how much rain appeared om the screen. 
Charset was created so that I could my characters, as descirbed above. 
Finally, screen focused on clearing the display and making sure the characters were stored properly. Without this, the screen wasn't clearning and the rain looked messy. In my constructures, I set screen to set a 2D grid to place characters, **screen_ = std::vector<std::string>(height, std::string(width, ' '));**. By placing the width and height in the vector, the current state of the screen is saved.


        
	std::uniform_int_distribution<int> column_dist;
	std::uniform_int_distribution<int> chance_;
	std::uniform_int_distribution<int> charset_;
	std::vector<std::string> screen_;

	struct Raindrop {
		int x_pos;
		int y_pos;
		int characters;
		int speed;
	};
	std::vector<Raindrop> raindrops;


	


<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image6.png" width="400" height="300">

I used for loops to update and display the rain drops, whilst the charcater moved vertically down the screen. 

## Updating the DigitalRain to handle colour
It is clear that the rain is very basic and there is a lot more I can add to make it look better and to clean up my code. The first thing I want to change is the colour of the charcters falling. I decided it would be a cool idea if the colour could change everytime the rain is updated. In order to add colour into my rain I decided to use the **#include <windows.h>**. I referenced this page, https://www.geeksforgeeks.org/how-to-change-console-color-in-cpp/. I decided to use the distribution object again to generate random colours like how I generated my characters, **std::uniform_int_distribution<int> choose_colour;**. I used the following function, 
**HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);**. This function is used to control the handle of the consoles output. By getting the handle I can set the handle to the colour I need. I created a getter and a setter for my random colours to do this. This is the outcome, 

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/code_recording5.gif" width="400" height="300">

## Adding a delay
When I first rain, it was extremely fast even with changing the speed of the raindrops. 

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image2.png" width="400" height="300">

After research, I decided I needed a delay for the overall frame of the display, https://blog.bearcats.nl/accurate-sleep-function/. I added in, 

     std::this_thread::sleep_for(std::chrono::milliseconds(speed_));


I used two libraires, **#include <chrono>** which was responsible for how long I wanted my delay, milliseconds.  As the **speed** varuable is created inside of the structure and would focus on the speed of each individual raindrop, I decided to create another variable called **speed_** which would focus on the speed of the rain effect. The second library I used was the **#include <thread>** which was responsible for the pause on the thread. 
At the start of the project I created 2 local variables width and height, but instead I decided that I wanted to create member functions as this would allow the code to be reuable and encapsilating. 




## Making a column in my Digital rain
Currently, my rain displays one character at a time. I wanted to update this code so that three characters would be generated instead of one. To do this, I changed my characters in my raindrop structure from an int to a char of vectors so i could display multiple characters, **std::vector<char> characters;**. Since there was three characters now per raindrop, I introduced a for loop to display them, 



       for (int i = 0; i < 3; ++i) {
           new_drop.characters.push_back(GetRandomCharacter());
       }




I decided to use the **push_back** to my vector to add an element to the end of it, https://www.w3schools.com/cpp/ref_vector_push_back.asp. The next thing I did was displaying my rain vertically after the characters were generated. This was the result of my 3 character vector, 

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image7.png" width="400" height="300">


# More characters printed in the screen
