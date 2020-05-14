# Design for Developers 101

You came to Juno to become a developer, so you might be asking why are we learning about design?

Yes we understand that you are here to become developers not designers. We don't need you to come out of the bootcamp as experts in design. In fact when you get a real development job, you will not be expected to know how to design. However development and design go hand in hand. Developers are constantly in communication with designers and other members on the team. Being able to understand the basics and talk about design is a super valuable skill to have alongside development skills and it will make you a better developer.

Making some of these common design mistakes in your projects and portfolio can actually make you look like a incapable developer. 

You will also be in charge of designing your projects in the upcoming weeks of bootcamp. We need all your projects to look as polished as possible because no potential employers wants to look at a ugly project with horrible UI! The goal for this lesson is to help you achieve that. 

> It takes about 50 milliseconds for visitors to form an opinion about your website; whether they like it or not, whether they'll stay or leave. In addition, first impressions are mostly design-related." 
> Shopify, 10 Tips for Building a Beautiful Web Developer Portfolio

After all we don't want your site to become something like this...
[https://www.lingscars.com/](https://www.lingscars.com/])

This is a guide on how you can get started with making design choices and avoid common mistakes!

## 1. Defining the purpose

The first and foremost thing to consider when you are getting started with your project is asking yourself these questions:
1. What is the project?
2. What purpose does it serve? 
3. Who is the target audience? 

Having these questions answered will eventually help define the tone and personality of the project, making it much easier to make design decisions in the future.

Let's use a trivia app as an example.
1. A trivia game that contains questions from different categories
2. Providing entertainment for family/friends gatherings
3. Family members of all ages, friends. 

It is also very important to have the purpose of your project clearly stated upon first landing on it. The user needs to know what the application or site is about when they land before they would like to invest any more of their time on the site further. 

**[Have a look at this site here](http://rottencode.herokuapp.com/)**

Would you want to interact with this site?

## 2. Choosing a colour palette

After you've defined the purpose and tone of your project, making colour choices will be a lot easier! Your site should follow a consistent color scheme throughout the site. Pre-defining a colour palette in your planning will simplify your building process. 

You don't need to understand colour theory to create a colour palette, there are lots of tools to help you out with it!

- **[Coolors](https://coolors.co/)**
- **[Color Hunt](https://colorhunt.co/)**
- **[ColorSpace](https://mycolor.space/)**

### Colour palette formula 🔥
The safest and simplest option to start creating a colour palette is to choose 5 colours: 
- **White or a very light grey (#FAFAFA)**
  A standard white is always needed mainly as the basic background colour of your website. 
- **Black or a very dark grey (#232323)**
  For paragraphs and text.
- **Primary colour**
  The main colour that determines the overall look of the project. This color will define the brand, personality and tone of your project. It can be used as background colours for sections, headings or buttons. 
- **Secondary colour**
  Having one main colour is boring! We will need to pick a second colour to add visual interest. This could be used for alternative background colours, buttons, CTAs, links and highlight tags. 
- **Supporting accent colours**
  Your project might need extra supporting accent colours that could be used for highlights, alert or warning messages. 

[Here's great article about building a successful color palette.](https://refactoringui.com/previews/building-your-color-palette/)

If you are unsure how to choose your primary colour and secondary colour. Look to the purpose of your project for inspiration. 

Once you've chosen a colour palette, stick to it and use those colours throughout the whole project!

_**Very important accessibility Note!**_
In order to meet the [WCAG AA compliance standard](https://github.com/HackerYou/bootcamp-notes/blob/master/accessibility/accessibility-and-css.md), you have to make sure the colour combination you are using between your regular text and the background have a **contrast ratio of 4.5:1**. You can use tools like [Color Safe Color Generator](http://colorsafe.co/) or [Text on Background Image Contrast Checker](https://www.brandwood.com/a11y/) to check contrast ratios.


## 3. Choosing Fonts

Like colours, different fonts can convey different meanings. The most important thing when it comes to choosing fonts is to make sure that they are:
- **Appropriate for the project's purpose**
- **Legible for everyone!**

Think about the content of your site, what your site is about and the mood that it should convey. A font can be classic, artistic, youthful, modern etc. 

(Image of different Fonts)

### Serif vs. sans-Serif

(image of serif vs sans-serif)

It is common to use more than one font for a project. Like colours, designers choose a second font or even a third font to add visual variety. However there should be **no more than three**! If you have more than three fonts, the project can look messy and inconsistent. The typical recommendation would be to **choose two fonts - a heading font and a body text font**. We call this *font pairing*.

### Font pairing tips 🔥

- Keep elaborate and unconventional fonts for headings, as headings are generally short and should be eye-catching visually. 
- Sans-serif fonts are usually recommended for body text as they are easier to read on the screen, but it's not a super hard rule, many serif fonts could work great as body text as well. 
- If your heading font is elaborate, choose a simpler body font. If your heading font is simpler you can choose a more interesting body font, but again keep in mind that body font needs to be legible!
- One of the easiest way to pair fonts while keeping visual interest is to pair a serif font with a sans-serif font.
- **Bulletproof 🔥 Tip**: Just choose a font pairing combination from [fontpair.co](https://fontpair.co/) or [ultimate google font pairings](https://www.reliablepsd.com/ultimate-google-font-pairings/) that speaks to you and your project!


## 4. Styling Text

### Line Height

### Length and spacing

### Alignment

### Text Hierarchy 


## 5. Buttons

Buttons are considered as a major and essential UI element for all sites and applications. They are sometimes referred to as *CTA (call to action)*, which is meant to prompt user interaction. Therefore, they are usually styled to bring visual attention, usually with a secondary color or accent color. 

(image of different button styles)

Buttons comes in all varieties of different styles. There are no right and wrong button styles as long as you **stick to one particular style** throughout the entire project and follow these best user experience (UX) practices:

- Buttons should have a descriptive text telling users what they are expected to happen when they click on the button. 

(image of non descriptive text vs descriptive text)

- Buttons should have some padding space around the descriptive text so that use have enough clickable area. 

(image of space vs no space)

- Buttons are interactive elements which means we need to ensure their pseudo states are styled. These include `:hover`, `:disabled` and `:active`. These will ensure user gets feedback from the interactivity. 
  [Play around with this codepen](https://codepen.io/susan8098/pen/YzXovOY), which button is correctly styled?

- Lastly, if it's not a interactive button (aka. if the element doesn't do anything), don't style it like one! It's confusing to the users!

## 6. Imagery & Icons

Imagery and Icons are elements that are responsible for making up a huge percentage of visual interest for your project, which is why is it very important to keep it cohesive, relevant and on brand. 

### Where to find imagery & icons? 

**Photos**
- [Unsplash](https://unsplash.com/)
- [Pexels](https://www.pexels.com/)
- [SplitShire](https://www.splitshire.com/)
- [Foodies Feed](https://www.splitshire.com/)
- [Life of Pix](https://www.lifeofpix.com/)

**Icons**
- [The Noun Project](https://thenounproject.com/)

**Illustrations**
- [unDraw](https://undraw.co/)
- [DrawKit](https://www.drawkit.io/)
- [humaaans](https://www.humaaans.com/)

Everything listed above are open-sourced and royalty-free! Do keep in mind to **give credits** to those who created them wherever you can! 

### What to watch out for when implementing images

- Make sure your images are high quality that aren't pixelated or stretched!

(images as example)

- At the same time you also want to make sure to optimize your images so that they are not over 2MB in size! Large image size are one of the main contributions to low performance speed. You can use tools like [ImageOptim](https://imageoptim.com/mac) or [Kraken.io](https://kraken.io/). 
- Choose images that are relevant to your content and purpose!

(images as example)

- Make sure to choose images that are cohesive in colour palette.

(images as example)

If you are struggling to find cohesive images, a hack you can use is to implement overlays.

(images as example)

### What to watch out for when implementing icons

Again consistency! All icons in your project needs to maintain consistency in colour, size, line/stroke sizes and treatment.

(images of icons that belongs to different icon set)

The easiest way to achieve this is just use icons that belongs as a set. Most artist create icons as a set and you can easily find sets on The Noun Project. 

The same goes for illustrations as well. Make sure you are using illustrations from the same artist or set for a cohesive look.

## 7. Layout & Grids

## 8. Responsive Optimization

## 9. Creating a style guide for consistency

## 10. UX Considerations
