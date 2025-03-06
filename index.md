---
title: A Project in Modern C++, Digital Rain
---

By Ciara Crowe

## First Steps
The first thing I worked on was creating the constructors for my project. The main variables I wanted to focus on for the raain was the width of the screen and the height. I decided to use charset, a vector of strings so the charcters could be defined in the project. This is the first constructor I made for my project:


**' class DigitalRain
{
  public:
	  DigitalRain();
	  DigitalRain(int width, int height);
	  DigitalRain(const std::vector<std::string>& charset);
	  DigitalRain(int width, int height, const std::vector<std::string>& charset);
   '**

I decided I wanted my project to be user oriented so that when I started my project the user could choose different options on how the rain looked. The user could choose what type of characters to be displayed were, what colour the rain would be etc..

So I did a little research to see what would be the best library to use to display my rain. 
After a bit of research I saw that the main library in choosing what chacrters i wanted to set my rain to was, 
**'std::uniform_int_distribution <int> u(x, y);'**

X and Y were dependent on what type of charcter I wanted to display whether it be ascii, numbers or uppercase characters. This meant i could display my rain with any symbol which was more preferable over a specific symbol. 
I wanted to create a specific function which would generate the random symbols. First I craeted an enum which held the different character types 



I needed to find a way to generate random letters, so I did a bit of research to see what the best way to do this. What I found:


**'std::rand() -> Old c ++ way of programming
std::random_device -> This is used mainly for hardware, but can be slow
std::mt19937 -> This produces fast and high quality random numbers
'**

I decided to generate a different range of numbers I was gonna use the **'std::mt19937'** library as this was more releavmt to what i was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. 




<div style="border: 2px solid #3498db; padding: 10px; border-radius: 5px; background-color: #f0f8ff; margin: 20px 0;">
    <p>Your content goes here. You can add Markdown elements like <strong>bold</strong> text or <em>italic</em> text, 
    lists, and even code blocks.</p>
</div>













Font can be *Italic* or **Bold**.

Code can be highlighted with 'backticks'.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list:

- vectors
- algorithms
- iterators

You can add an impage that has been uploaded to the repository in a /docs/assets/images folder.

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image.png" width="400" height="300">
