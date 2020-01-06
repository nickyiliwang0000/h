<!-- Student Takeaway -->
<!-- By the end of this lesson students should be comfortable with the basics of what web accessibility and inclusive design are, what the WCAG guidelines are and how to navigate them, the POUR concepts, and what the AODA and ADA/section 508 are -->
# Introduction to Web Accessibility

## What is Web Accessibility?

Web accessibility is exactly what it sounds like. It is the practice of making the web accessible to all users! This means that folks with any range of disabilities should be able to *perceive, understand, navigate and interact* with all of our websites and applications. 

### Disability

Disability is often viewed as an affliction that an individual is hindered by. But it's much more productive and inclusive to consider disability as the intersection of a person's abilities with their environment. In this light we can focus on fixing the environment. For example, folks with less than 20/20 vision have a visual disability until they have glasses. People holding babies have a situational physical disability until they have a baby carrier freeing up their arms. 

There is a tendency to focus on blind users with respect to accessibility. It is important that we consider a broader scope of disabilities when developing our digital products. 

Disabilities can be:

* auditory
* cognitive
* neurological
* speech related
* physical
* visual

Disabilities can be permanent (eg. blindness), temporary (eg. recovering from eye surgery), or situational (eg. bright sunlight makes it hard to see your phone screen). In considering this, the range of users we are optimizing for is much bigger. 

Accessibility is *for* people with disabilities. It's important to remember this so we keep these folks centred in our processes and discussions. But it also benefits everyone! 

### Curb Cut Effect

There is a concept referred to as the **curb cut effect** that we see in prioritizing accessibility in both physical and digital spaces. 

Our sidewalks did not used to have "curb cuts" in them, those little ramps at the corners. Eventually these ramps were instituted to make sidewalks accessible to wheelchair users. But they ended up benefitting society as a whole! Folks with bikes, strollers, grocery carts, skateboards, small children, etc all had much easier access to sidewalks once the curb cuts were in place.

Web accessibility has been shown to have curb cut effects too. When you make interfaces accessible to disabled users, all users stand to benefit. For example, many disabled users require keyboard navigation to use a website. This also stands to benefit "power users" who don't like to use a mouse. 

## Inclusive Design

Web accessibility does not begin with development. It needs to be a part of the entire product life cycle in order to be successful. This means that UX and visual designers have to prioritize it in their process as well as developers. And the journey does not end with development either, it continues with QA and ideally end-user testing as well.

**Inclusive design** is the practice of designing for a diverse range of users with different abilities and trying to identify our own biases so that we might overcome them in the design process. 

Microsoft released some very good content and a toolkit about inclusive design that we highly recommend checking out!
[inclusive design from Microsoft](https://www.microsoft.com/design/inclusive/)

## W.C.A.G.

Different regions have their own regulating bodies for web accessibility (more on that below). But they all point back to the internationally recognized standards of the **Web Content Accessibility Guidelines** made by the **World Wide Web Consortium**, or **WC3**.

The WCAG guidelines are a reference guide for achieving accessible interfaces. The most recent stable release is version 2.1 which is available online: [WCAG 2.1](https://www.w3.org/TR/WCAG21/).

It can take some time to navigate and familiarize yourself with this document and all of the success criteria and suggestions within it. Over time as you become more comfortable testing your code for compliance issues you will become more comfortable with WCAG.

### A, AA, AAA

Accessibility compliance has three levels. `A`, `AA`, and `AAA`. Most regions legally require `WCAG 2.1 AA` level compliance. Single A would not be considered sufficient and triple A is ideal though often not legally required (there are likely many industry specific exceptions to this). 

As you navigate the WCAG guidelines be sure you are watching for these levels and achieving at least AA support.

### P.O.U.R.

The WCAG guidelines are broken into 4 categories: **perceivable, operable, understandable** and **robust**.

**Perceivable:** Users have to be able to perceive and intake all of the content. For example, if the user is blind, all of the content needs to be available via screen reader. 
More information: [Web AIM - perceivable](https://webaim.org/articles/pour/perceivable).

**Operable:** Users need to be able to navigate and operate and interact with the interface. Not all users have ability to use a mouse, and many assistive technologies use the keyboard or emulate keyboard functionality. 
More information: [Web AIM - operable](https://webaim.org/articles/pour/operable).

**Understandable:** Users need to be able to understand the content itself as well as how the functionality works. This is important for all users, but particularly imperative for folks with cognitive disabilities. 
More information: [Web AIM - understandable](https://webaim.org/articles/pour/understandable).

**Robust:** Users need to be able to access web content with a range of devices and browsers. Making interfaces or even features only usable with certain devices, operating systems and browsers can exclude many people. 
More information: [Web AIM - understandable](https://webaim.org/articles/pour/robust).

## Regulating bodies

Different regions and even industries can have their own regulating bodies with respect to accessibility compliance. Here in Ontario we have the **Accessibility for Ontarians with Disabilities Act** or the **AODA** for short. 

### A.O.D.A.

[AODA - guide to the ACT](https://www.aoda.ca/guide-to-the-act/)

There is an Ontario-wide legislative act from the AODA which covers both physical and digital accessibility. It is governed by a minister and the Accessibility Standards Advisory Council. This act applies to:
* provides goods, services or facilities;
* employs persons in Ontario;
* offers accommodation;
* owns or occupies a building, structure or premises; or
* is engaged in a prescribed business, activity or undertaking or meets such other requirements as may be prescribed.

Tl;dr any business you work for that operates in Ontario will be required to comply.

The government of Ontario also has a helpful resource about how to make your websites accessible [here](https://www.ontario.ca/page/how-make-websites-accessible).

**Beginning January 1, 2021**: all public websites and web content posted after January 1, 2012 must meet WCAG 2.0 Level AA other than criteria 1.2.4 (live captions) and 1.2.5 (pre-recorded audio descriptions).

After this date if your company is found to be failing compliance you will likely be given a window of time to address the issues before being fined. Here is some information about the [fines in Ontario](https://www.aoda.ca/aoda-administrative-monetary-penalties-scheme-%E2%80%93-three-strikes-you%E2%80%99re-out/). They can be up to $100,000 per day for repeat offenders!

### ADA and Section 508 of the Rehabilitation Act

Many of you will work for companies that are American or operate in the US. In the United States they have the broader [Americans with Disabilities Act](https://www.ada.gov/) (ADA), as well as [Section 508 of the Rehabilitation Act](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines), which is specific to *Information Communication Technology*. 

## Career Opportunities

Web accessibility is becoming more in-demand as a skillset, especially as enforcement deadlines approach here in Ontario. Many folks who have been in tech for years are lacking in up-to-date knowledge about accessibility and the requisite skills to implement accessible code. 

Juno grads have an opportunity to help solve a critical business problem for companies looking to achieve accessibility compliance and to differentiate themselves in the market by offering this skillset.

There are specific accessibility development roles out there, but it is also seen as a very valuable asset to bring to any frontend development team.
