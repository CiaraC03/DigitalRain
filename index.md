---
---

By Ciara Crowe

## First Steps
The first thing I worked on was creating the constructors for my project. The main variables I wanted to focus on for the raain was the width of the screen and the height. This is the first constructor I made for my project:

```

  class DigitalRain {
public:
  DigitalRain();
  DigitalRain(int width, int height);
  DigitalRain(const DigitalRain&);
  ~DigitalRain();

void StartRain(); //this just prints amessage
void ShowRain(); //this will  be the function to dispay the rain
char GetRandomCharacter(); //i will use this function to get my characters

```


## Characters

The next step for me was choosing what charcters I wanted to be displayed for my rain. I could have a very specific database with specific numbers and letters or i could choose a wide range of them. For me I decided to use a bunch of different charcters to display my rain to make it more like the matricx rain display.
After a bit of research I saw that the main library in choosing what characters I wanted to set my rain to was: 


**std::uniform_int_distribution &lt;int&gt; u(x, y);**







X and Y were dependent on what type of charcter I wanted to display whether it be ascii, numbers or uppercase characters. This meant i could display my rain with any symbol which was more preferable over a specific symbol. 
I wanted to create a specific function which would generate the random symbols. I created a small function which would return a random set of ascii numbers: 


**char DigitalRain::GetRandomCharacter()**





I chose to return a random numbers from 33 to 126 meaning that any ascii character from 33 which is the '!' chacrter to 126, '~' would be printed. Here I was able to choose what characters I wanted, https://www.geeksforgeeks.org/ascii-table/ . The static_cast converts the number generated into ascii code, casting a char. 



## First Attempt at DigitalRain

For my first attempt I wanted to create a basic rain display, using the height and width variables I already created. First I created a function to display my rain. 

My fist plan was to find out how to update the sequence of numbers every time my rain ran. I used chat gpt to see what was best libraries I could use to update my code. This is the resaerch I came back with:

 '''
    
	std::rand() -> Old c ++ way of programming
	std::random_device -> This is used mainly for hardware, but can be slow
	std::mt19937 -> This produces fast and high quality random numbers

 '''
    



I decided to generate a different range of numbers I was gonna use the **'std::mt19937'** library as this was more relevent to what I was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. 



Now that I had decided on my numbers, I focused on the function to create the rain. I created a scructure called Raindrop which would display the character, speed, x postion and the y position. Using the distribtion generator I created the column distance, to decide on the distance for the columns, chance, which decided on what chance the rain was going to fall, and charset, to pick random charcters. In my constrcutor I have set the chance to be chance_(0, 10), meaning that an int is produced between 0 and 10. Chance is set to 3 when creating a new drop so that the probablility of producing a new rain drop is about 3/11, just under 30%: 

'''
        
	std::uniform_int_distribution<int> column_dist;
	std::uniform_int_distribution<int> chance_;
	std::uniform_int_distribution<int> charset_;
	std::uniform_int_distribution<int> choose_colour;
	std::vector<std::string> screen_;

	struct Raindrop {
		int x_pos;
		int y_pos;
		int characters;
		int speed;
	};
	std::vector<Raindrop> raindrops;

'''
	


<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image6.png" width="400" height="300">

I used for loops to update and display the rain drops, whilst the charcter moved vertically down the screen. 




## Updating the DigitalRain to handle colour
From the above example it is clear that the rain is very basic and there is a lot more i can add to make it look better and to clean up my code. The first thing I want to change is the colour of the charcters falling. I decided it would be a cool idea if the colour could change everytime the rain is updated. In order to add colour into my rain I decided to use the **#include <windows.h>**. I decided to use the distribution object again to generate random colours, **std::uniform_int_distribution<int> choose_colour;**. I used the following function, 
**HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);**. This function is used to control the handle of the consoles output. By getting the handle I can set the handle to the colour I need. I created a getter and a setter for my random colours to do this. This is the outcome, 

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image2.png" width="400" height="300">


## Making a column in my Digital rain
As of right now, I have my rain displayed so that one character is being displayed. i wanted to update this code so that 3 characters would be generated. The first thing i did was changed my characters in my raindrop structure from an int to a char of vectors so i could display multiple characters, **std::vector<char> characters;**. I then had to update my function to display the rain with the charcters generated so I added a for loop into my rain with, 

'''

       for (int i = 0; i < 3; ++i) {
           new_drop.characters.push_back(GetRandomCharacter());
       }


'''

I decided to use the **push_back** to my vector to add an element to the end of it, https://www.w3schools.com/cpp/ref_vector_push_back.asp. The next thing I did was displaying my rain vertically after the characters were generated. 

# More characters printed in the screen
