# Frontend Mentor - Testimonials grid section solution

This is a solution to the [Testimonials grid section challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/testimonials-grid-section-Nnw6J7Un7). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the site depending on their device's screen size

### Screenshot

![Desktop](/src/assets/images/screenshot_desktop.PNG)
![Mobile](/src/assets/images/screenshot_mobile.PNG)

### Links

- Solution URL: [Frontendmentor](https://www.frontendmentor.io/solutions/testimonials-component-dPgvG1e0Z6)
- Live Site URL: [Github](https://theroborobin.github.io/Frontend-Mentor-Testimonials-Component/)

## My process

Since this component is getting more complex I decided to start using the folder architecture that I learned to structure and organize my code. This went fairly smoothly. I'm still getting used to the @use and @forward instead of @import since that's how I learned initially. But overall, it was easy.

Setting up the repository went well. I preemptively set it to use an action before pushing my code for the first commit. Kept it from hitting an error the first time deploy.yml ran.

The main thing while building out the html was that there was a shared testimonial block with modifiers for color or position. And so that's how I set it up.

    <div class="testimonial testimonial--primary testimonial--tl">

Fairly straight forward. I also made the decision to use an entity instead of the provided svg.

I thought about a video that I recently watched from Kevin Powell on css custom properties. It was about the idea of pseudo private properties. I do have different variants of the same testimonial block with multiple properties to manage. So I am going to try and impliment this later.

Since I built my architecture with \_utilities.scss, I decided lets go ahead and use it. I made flex utilities that I'm sure I'll use in this component.

Next was the page architecture, mainly the grid. My thought is a grid with 4 columns that are set to auto fit and have a minmax of 20% and 1fr. See if that gives me the structure I want with responsiveness. And after placing the content, I realized the obvious. With things set so rigidly, auto-fit wasn't going to work. So I'll just have to make media queries to move the grid around.

After building out the loose structure, now on to fiddle with the idea of pseudo private properties.

So the way Kevin explained it was greating the pseudo private property with --\_. It doesn't seem like something I'd be able to just use sass variables for. So maybe I use a combo of variables and custom properties. After some research and troubleshooting, I found that it can be called using something similar to a template literal in JS.

And so... building this all out was as simple as:

    .testimonial {

      //Property that calls the property used later in the modifier

      --_text-main: var(--text-main);
      --_background: var(--background);
      --_border: var(--border);

      //Main property is then called in the color, background-color, and border

      color: var(--_text-main);
      background-color: var(--_background);

        &__img {
          height: 3.2rem;
          width: 3.2rem;
          border: 2px solid var(--_border);
          border-radius: 50%;
        }

      //Called using this modifier that changes what the custom property references through the whole code.

      &--primary {
        --text-main: #{a.$color-white};
        --background: #{a.$color-primary-dark};
        --border: #{a.$color-primary};
      }
    }

As I add more elements that change in between modifiers like text color. Then less complicated have to be used to change those things. This may have been a bit overkill for such a simple project, but its better to understand it with simpler components.

After building the psuedo private properties, the rest of the design came together very easily. I had a few issues with the ::before element not showing but it ended up just being a spelling mistake.

Media queries came together well. Since things were placed specifically in the grid, It was fairly easy to shift things to adjust to the screen size. Did some minor spacing and sizing adjustments too. Overall I think it works very well.

### Built with

- Semantic HTML5 markup
- Flexbox
- CSS Grid
- SASS
- CSS Custom Properties
- "Pseudo Private Properties"
- Block Element Modifier / 7-1 Architecture
- GitHub Actions

### What I learned

I feel like I learned quite a bit in the ways that I can further integrate and use variables or custom properties into my work. I also feel like I have a better feel of the architecture since I actually did it myself instead of just copying the structure given.

### Continued development

I want to continue to work on my organization as projects get bigger. I also want to start more self directed projects.

### Useful resources

- [Using CSS custom properties like this is a waste - Kevin Powell](https://youtu.be/_2LwjfYc1x8?si=9kYdPWoWPa8h_3wV) - This is the video that taught me about this concept of "pseudo private properties"

## Author

- Website - [Robin](https://github.com/TheRoboRobin)
- Frontend Mentor - [@TheRoboRobin](https://www.frontendmentor.io/profile/TheRoboRobin)
