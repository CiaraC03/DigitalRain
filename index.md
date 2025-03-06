---
layout: post
title: A Project in Modern C++, Digital Rain
tags: cpp coding project
categories: demo
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


The next step for me was working with the characters itself and choosing what i could do. I did a little research to decided what would be the best library to use to choose my rain. 
After a bit of research I saw that the main library in choosing what chacrters i wanted to set my rain to was, 
**'std::uniform_int_distribution <int> u(33, 254);'**
This generates random datasets from an ascii range. This meant i could display my rain with any symbol. 
I did a little more research to see if there was anything else out there I could use as I had an idea where instead of having rain where the output is just an ascii range, maybe I could prompt the user to see what they wanted. 
They could choose between ascii numbers, uppercase letters, numbers or a combination of all. 



I needed to find a way to generate random letters, so I did a bit of research to see what the best way to do this. What I found:


**'std::rand() -> Old c ++ way of programming
std::random_device -> This is used mainly for hardware, but can be slow
std::mt19937 -> This produces fast and high quality random numbers
'**

I decided to generate a different range of numbers I was gonna use the **'std::mt19937'** library as this was more releavmt to what i was doing and seemed to be more advanced than the old c++ library **'rand()'**. To add this to my project i just needed to add the header file **'#include <random>'**. 


















Font can be *Italic* or **Bold**.

Code can be highlighted with 'backticks'.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list:

- vectors
- algorithms
- iterators

You can add an impage that has been uploaded to the repository in a /docs/assets/images folder.

<img src="https://raw.githubusercontent.com/CiaraC03/DigitalRain/main/docs/assets/images/image.png" width="400" height="300">
