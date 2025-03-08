---
title: A Project in Modern C++, Digital Rain
---

By Ciara Crowe

## First Steps
The first thing I worked on was creating the constructors for my project. The main variables I wanted to focus on for the raain was the width of the screen and the height. I decided to use charset, a vector of strings so the charcters could be defined in the project. This is the first constructor I made for my project:

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    <p>
 class DigitalRain
{
  public:
	  DigitalRain();
	  DigitalRain(int width, int height);
	  DigitalRain(const std::vector<std::string>& charset);
	  DigitalRain(int width, int height, const std::vector<std::string>& charset);
    </p>
</div>


## Characters

I decided I wanted my project to be user oriented so that when I started my project the user could choose different options on how the rain looked. The user could choose what word to be displayed, what colour the rain would be etc..

So I did a little research to see what would be the best library to use to display my rain. 
After a bit of research I saw that the main library in choosing what chacrters i wanted to set my rain to was: 

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    
std::uniform_int_distribution <int> u(x, y);
    
</div>






X and Y were dependent on what type of charcter I wanted to display whether it be ascii, numbers or uppercase characters. This meant i could display my rain with any symbol which was more preferable over a specific symbol. 
I wanted to create a specific function which would generate the random symbols. I created a small function which would return a random set of ascii numbers: 




<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    
char DigitalRain::GetRandomCharacter()
{
    return static_cast<char>(std::uniform_int_distribution<int>(33, 126)(engine_));
}
    
</div>



I chose to return a random numbers from 33 to 126 meaning that any ascii character from 33 which is the '!' chacrter to 126, '~' would be printed. The static_cast converts the number generated into ascii code, casting a char. 




I decided to generate a different range of numbers I was gonna use the **'std::mt19937'** library as this was more releavmt to what i was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. 


## First Attempt at DigitalRain

For my first attempt I wanted to create a basic rain display, using the height, width and speed variables I already created. First I created a function to display my rain. 

My fist plan was to find out how to update the sequence of numbers every time my rain ran. This is the resaerch I came back with:

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    
std::rand() -> Old c ++ way of programming
std::random_device -> This is used mainly for hardware, but can be slow
std::mt19937 -> This produces fast and high quality random numbers
    
</div>


I decided to generate a different range of numbers I was gonna use the **'std::mt19937'** library as this was more releavmt to what i was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. To proevent the same sequence of numbers produced with a fixed seed, I decided to use the **#include <chrono>** library to add a fixed time seed. This meant that I could have different varied sequence every time I ran my rain: 

<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    
engine_(std::chrono::system_clock::now().time_since_epoch().count())
    </pre>


Now that I had decided on my numbers, I focused on the function to create the rain. I started by creating a vector with the width variable. This would represent the way the rain ran vertically. I decided to create two for loops. The first for loop was repsonsible for making sure that the screen was cleared so that new characters could be added. I also wanted to add in a check to see if a specific column was showing a character at a row. This was the result for my first rain,




<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image6.png" width="400" height="300">
