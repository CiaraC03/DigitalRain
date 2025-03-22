---
---

By Ciara Crowe

## First Steps
The first thing I worked on was creating the constructors for my project. The main variables I wanted to focus on for the raain was the width of the screen and the height. This is the first constructor I made for my project:

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">

	class DigitalRain {
      public:
	DigitalRain();
	DigitalRain(int width, int height);
	DigitalRain(const DigitalRain&);
	~DigitalRain();

	void StartRain(); //this just prints amessage
	void ShowRain(); //this will  be the function to dispay the rain?
	char GetRandomCharacter();

</div>


## Characters

The next step for me was choosing what charcters I wanted to be displayed for my rain. I could have a very specific database with specific numbers and letters or i could choose a wide range of them. For me I decided to use a bunch of different charcters to dispaly my rain to make it more like the matricx rain display.
After a bit of research I saw that the main library in choosing what characters I wanted to set my rain to was: 

<div class="code-box">
    std::uniform_int_distribution &lt;int&gt; u(x, y);
</div>






X and Y were dependent on what type of charcter I wanted to display whether it be ascii, numbers or uppercase characters. This meant i could display my rain with any symbol which was more preferable over a specific symbol. 
I wanted to create a specific function which would generate the random symbols. I created a small function which would return a random set of ascii numbers: 




<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    
     char DigitalRain::GetRandomCharacter()
      {
	std::uniform_int_distribution<int> dist(33, 126);
        return static_cast<char>(dist(engine_));
     }
    
</div>




I chose to return a random numbers from 33 to 126 meaning that any ascii character from 33 which is the '!' chacrter to 126, '~' would be printed. The static_cast converts the number generated into ascii code, casting a char. 



## First Attempt at DigitalRain

For my first attempt I wanted to create a basic rain display, using the height and width variables I already created. First I created a function to display my rain. 

My fist plan was to find out how to update the sequence of numbers every time my rain ran. This is the resaerch I came back with:

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    
std::rand() -> Old c ++ way of programming
std::random_device -> This is used mainly for hardware, but can be slow
std::mt19937 -> This produces fast and high quality random numbers
    
</div>


I decided to generate a different range of numbers I was gonna use the **'std::mt19937'** library as this was more relevent to what I was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. 



Now that I had decided on my numbers, I focused on the function to create the rain. I created a scructure called Raindrop which would display the charcter, speed, x postion and the y position. Using the distribtion generator I created the column distance, to decide on the distance for the columns, chance, which decided on what chance the rain was going to fall, and charset, to pick random charcters: 

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    <pre>
        
	std::uniform_int_distribution<int> column_dist;
        std::uniform_int_distribution<int> chance_;
        std::uniform_int_distribution<int> charset_;
        std::vector<std::string> screen_;

        struct Raindrop {
            int x_pos;
            int y_pos;
            char character;
            int speed;
        };
        std::vector<Raindrop> raindrops;
    </pre>
</div>









<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image6.png" width="400" height="300">

I used for loops to update and display the rain drops, whilst the charcter moved vertically down the screen. 




## Updating the DigitalRain
From the above example it is clear that the rain is very basic and there is a lot more i can add to make it look better and to clean up my code. The first thing i want to change is the number of charcters falling in the vector. 
