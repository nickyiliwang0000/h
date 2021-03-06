# Extra HTML/CSS exercise

## Flexbox and responsive design
Time to practice flexbox and media queries! Mastering flexbox will allow us to achieve more complex layouts. While knowing how to craft media queries is important when we want to build websites that will flex to users' devices.

A few things to remember when working with flexbox and responsive design:

### Flexbox
1. Properties that go on the **parent/flex-container**
  1. `display`
  2. `flex-direction`
  3. `justify-content`
  4. `align-items`
  5. `flex-wrap`
2. Properties that go on the **flex children**
  1. `order`
  2. `align-self`
  3. `flex-grow, flex-shrink, flex-basis`
  4. `flex` (shorthand for the `flex-grow`, `flex-shrink` and `flex-basis`)
  5. `margin: auto`

### Responsive design
1. Don't forget your viewport meta tag when you make a responsive site.  This should live between your `<head></head>` tags. This is already added for you in the exercise, but remember to add it to your project if you want to make any site. The tag looks like this: `<meta name="viewport" content="width=device-width, initial-scale=1.0">`

## Woofer final product
We'll be creating ~~Twitter~~ Woofer - a social media platform for our doggie friends. Here is the final desktop view:
![Screenshot of Twitter with a dog's face in the profile picture place](https://hychalknotes.s3.amazonaws.com/woofer-final.png)

### Exercise 1: Woofer header and banner (layouts, positioning, pseudo-elements, flex-grow, etc)
Download the starter files to begin: [html-css-bootcamp-fishbowl-header.zip](https://hychalknotes.s3.amazonaws.com/html-css-bootcamp-fishbowl-header.zip). We're going to break this down and work on the header and profile banner first. Here's what you are aiming for:  

![Screenshot of the top banner of Twitter with a dog's face in the profile picture place](https://hychalknotes.s3.amazonaws.com/woofer-header.jpg)

#### Hint image:
![Screenshot of what is probably a pseudo-element](https://hychalknotes.s3.amazonaws.com/woofer-hint-image.png)  

Second hint!
`flex-basis` is a good property to set on the pseudo-element! Pseudo-elements by default are inline: you may need to convert them so that they will accept a dimension.

### Exercise 2: Making Woofer responsive (media queries, flexbox, shared classes, etc)
Download the starter files to begin: [html-css-bootcamp-fishbowl-responsive.zip](https://hychalknotes.s3.amazonaws.com/html-css-bootcamp-fishbowl-responsive.zip). We're going to make Woofer responsive! Here are the designs you are aiming for:  

Large screens:  
![Screenshot of Woofer design for large screens](https://hychalknotes.s3.amazonaws.com/woofer-final.png)  

Medium screens:  
![Screenshot of Woofer design for medium screens](https://hychalknotes.s3.amazonaws.com/woofer-med.png)  

Medium to small screens:  
![Screenshot of Woofer design for medium to small screens](https://hychalknotes.s3.amazonaws.com/woofer-med-sm.png)  

Small screens:  
![Screenshot of Woofer design for small screens](https://hychalknotes.s3.amazonaws.com/woofer-sm.png)  

Done? Check out [this link](https://giphy.com/embed/l4JySAWfMaY7w88sU)!