<!-- Is your feature request related to a problem? Please describe.
The lesson is pretty short and not super valuable in it's current form.

Describe the solution you'd like

 Identify clear learning objectives for cross-browser testing and document here:
Students should learn:
 ..
 ...
 Review ConEd web-dev version of this lesson for possibly pulling into Bootcamp (and move Web-Dev version lesson to Additional Resources in that course)
 Update lesson -->

 # Cross-browser testing
Testing your code across multiple browsers can be a pain, but it's crucial to do if you want to maintain a good experience for all users.

 ## Cross-browser Compatibility

It's important to understand the issues that can arise when working with different browsers. While all browsers have agreed on some concepts, such as the <!DOCTYPE> at the start of your HTML or that block and inline elements will behave in specific ways, there are actually few other concepts they have chosen to support and interpret in a similar way. This means that while we can expect CSS filters to work on some browsers, they may not work on another the same way.   

There are five main browsers developers need to consider:

1. Chrome
1. Firefox
1. Safari
1. Internet Explorer/Edge
1. Opera

Chrome, Firefox, Edge and Opera are **evergreen browsers**, meaning they update themselves automatically. Internet Explorer and Safari are not.

Chrome has a rapid release schedule and it automatically updates, so you usually only have to support the latest version.

Firefox recently switched to a similar schedule, so supporting the latest version is 100% okay.

Safari is pretty aggressive about updating as well, most support the latest two versions of Safari. 

Opera has recently abandoned their browser engine and adopted Chromium / Blink, which is the engine behind Chrome. So, testing for Chrome is essentially testing for Opera.

Internet Explorer has historically been a pain point for many developers. Microsoft recently discontinued support on older versions, but older versions are still in use. If your client uses an older version of IE, you'll need to support it. 

Right now, most developers support back to IE11, which is considered the last of the buggy browsers to support. 

If you're catering to a modern audience, you may be okay supporting the latest version. When in doubt, look at analytics data on what browsers site visitors are actually using.

![](https://hychalknotes.s3.amazonaws.com/purpose.png)

## The Four Ws

It's easy to fall into the trap of never ending testing. Before you start working on your website, it's important to understand what demographics your website is targeted towards.

Ask yourself the 4 Ws when consider how you will approach testing your website:
* Where: Where do the users live that the website is targeting? Different regions will have higher rates of usage for certain browsers.

    StatCounter has a great map and stats that you can target by date range and region that can be [found by clicking here](http://gs.statcounter.com/browser-market-share/desktop-tablet-console/worldwide#monthly-201901-201906-map).
    
    In 2019, Chrome was the most widely used browser internationally. Each region has their own most used browsers, and the top three should be tested. Also keep in mind that those in more remote areas may have slower internet connections and that should be considered when testing.

* Who: Who is the website primarily targeted towards? The age range of the target demographic of your website should affect how you approach testing.

* What: What type of website are you building? Will it have a lot of graphics included? Will it need a fast internet speed to work properly? If so, does that match the "who" and "where" demographics?

* When: How long will your website be up? Will it be updated often or will it not be checked on for a couple months or years? If the website isn't going to be checked on often, ensure the code is future proofed with code that isn't in the experimental phase or hasn't been rendered obsolete (for example, `<center>` is no longer a valid tag in HTML5 and all centered items should be centered with CSS only).

If you are working on a project for a client or other stake-holders it's important to gather information about which browsers they need you to support. The scope of the work can be greatly affected by this. You'll need to account for cross-browser testing time as well as time to fix any bugs that are discovered in this testing process. It's also important to consider which operating systems are being supported. Browsers may behave differently on a mac vs a windows machine.

## CanIUse
[CanIUse.com](https://caniuse.com/) is a website that allows developers to check which properties are supported, and to what extent, on different browsers and their different versions. It also provides developers with useful insight about known bugs and issues on certain browsers when using specific properties. Web development moves extremely quickly and CanIUse is especially useful when trying out new properties.

For example, when looking up `position: sticky` on [CanIUse](https://caniuse.com/), the following table will come up: 

![Screenshot from the website CanIUse, showing the support for "position: sticky"](https://hychalknotes.s3.amazonaws.com/canIUse--conEd.png)

You can also see the [table live by clicking here](https://caniuse.com/#feat=css-sticky).

This table displays the support per browser and version using colours:
* A red background means there is extremely limited or no support.
* A yellow background means there is partial support.
* A green background means that there is enough support that you can feel comfortable using it.

It also provides information about known issues and bugs. For example, the last three versions of Chrome and Edge as well as Opera have partial support because `position: sticky` will not work when used in a `<thead>`, the table head element, or `<tr>`, the table row element. If our websites do not use tables, this issue isn't a concern at all. CanIUse also shows IE with a red background, meaning there is no support for `position: sticky`, which should be considered if the target audience are large users of IE.

Try looking up "CSS Filters" and "Flexbox" on CanIUse to learn about the support offered by each browser. 

Web development moves really fast. There will be new properties introduced in the CSS specifications in the future. So it's important for us to know which browsers have fully supported these properties and techniques before using them in our projects.

## Browser Testing Tools

### Testing Internet Explorer

#### IE Tester
IE tester for Internet Explorer: [http://www.my-debugbar.com/wiki/IETester/HomePage](http://www.my-debugbar.com/wiki/IETester/HomePage) - lets you open IE in every version. We encourage you to check site analytics, to see if supporting any versions prior to IE11 is even necessary. 

#### Virtual Box + Modern.ie
Regardless of PC/MAC/Linux, you can run a copy of windows right inside of your operating system. Microsoft knows the pain of testing on multiple versions of IE, so they have provided images of windows with different versions of IE loaded onto them. You can download them at [https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/). These are huge downloads, so plan to do so on a stable internet connection.

To run them, you need a free program called Virtual Box — [https://www.virtualbox.org/](https://www.virtualbox.org/).

You can download a copy of windows specially made for testing IE on <http://modern.ie>

### Testing Firefox, Chrome & Opera
For Google Chrome, Firefox and Opera, you don't need to worry about older versions as much - it auto updates. they are what we call <a href="https://www.techopedia.com/definition/31094/evergreen-browser" target="_blank">Evergreen Browsers</a>. They update frequently and automatically. However, you should still continue to test your site on these browsers! It is always wise to check your website on both a PC and Mac version of both. 

### Testing Safari
For Safari you generally don't need to worry as much either, but in some edge cases use this: [http://michelf.ca/projects/multi-safari/](http://michelf.ca/projects/multi-safari/)

### Other Testing
Here are a few tools you can use to help test:

[http://www.smashingmagazine.com/2011/08/07/a-dozen-cross-browser-testing-tools/](http://www.smashingmagazine.com/2011/08/07/a-dozen-cross-browser-testing-tools/)

* [Browser Stack](http://www.browserstack.com/) Provides live testing across multiple browsers and mobile devices.
* [Sauce Labs](https://saucelabs.com/) also provides a similar service
* [Browser Shots](http://browsershots.org/) Gives you screenshots in many different types of browsers
* [Litmus](https://litmus.com/) provides testing for every type of email program you can imagine. Testing email is extremely difficult and this tool is invaluable. If you are coding an email for someone, make sure to bake a few months of Litmus into the price ($80/month). 
	* Paid MailChimp accounts also have litmus integration. It is slower (~10 mins for each test VS 2 mins) but cheaper ($20/month). 

* [MultiFirefox](http://davemartorana.com/multifirefox/) Allows you to run various version of Firefox simultaneously.
* [DebugBar](http://www.my-debugbar.com/)

## Vendor prefixes
Vendor prefixes, also known as browser prefixes, help browsers give extra support to new CSS features. They became extremely popular when CSS3 came out, when a ton a new properties became available and browsers wanted to experiment with how they would implement the properties. Vendor prefixes cannot give support to properties that have no support, but add browser-specific support to certain properties that a browser is experimenting with.

Browser manufacturers each have their own vendor prefix that is pre-pended before the CSS property:
* Chrome, Safari: `-webkit-`
* Firefox: `-moz-`
* Internet Explorer: `-ms-`
* Opera: `-o-`

For example, `border-radius` was introduced with CSS3. While browsers were working on testing out what the property would look like on each of their products, developers would set `border-radius` like so:

```css
div {
    -moz-border-radius: 3px;
    -webkit-border-radius: 3px;
    -o-border-radius: 3px;
    -ms-border-radius: 3px;
    border-radius: 3px; 
}
```

Eventually, when full support was reached on new properties, developers could drop the prefixes and just use `border-radius` the way we do now:

```css
div {
    border-radius: 3px; 
}
```

When working with any new property, check CanIUse to see if a prefix is needed to ensure the property can run properly. CCS3 has been out for a while now, meaning prefixes are less common to see but are still used and important to understand.

## Mobile Testing
Most browser dev tools come with a way to preview what your site will look like on mobile. However, there are occassionally discrepencies between what the dev tools show you, and how the site actually appears on a device. For this reason, testing on actual hardware is always preferable. Try it on your phone to start, but it's also a great idea to find someone with a different phone or tablet model who can test your site for you too!

For testing on iOS (iPhone), Xcode (an application used to develop iOS apps) is useful for testing your websites on various device sizes.


### Mobile Testing with Localhost

Some test cases require you to use the physical device for testing. You can do cross-browser testing via localhost without pushing to a live sandbox site. A good article describing the process on how to utilize localhost testing on devices using your local IP can be found at the following link:

[http://support.apple.com/kb/ts5329](http://support.apple.com/kb/ts5329)


### Remote Debugging

If you do find bugs specific to mobile devices, you can use remote debugging to inspect and debug your page from your computer. 

You can remote debug Chrome for Android using the phone's USB cable and desktop Chrome and (OSX and Windows). <https://developer.chrome.com/devtools/docs/remote-debugging>

Similarly, you can remote debug iOS Safari using the iPhone/iPad USB cable and desktop Safari (OSX only). <http://moduscreate.com/enable-remote-web-inspector-in-ios-6/>

### Where to start testing

We have outlined a lot of different ways we can test various environments. It is important to note that it is not expected of you to start testing and using all of these methods. Start with Evergreen Browsers as your baseline, and if you know the project you are working on will be used on a specific browser, look into the various methods needed to test that!

### Developing with Browser Support in mind

In addition to testing our sites, we should also be building sites with browser support in mind. Web development moves really fast. There will be new properties introduced in the CSS specifications in the future. So it's important for us to know which browsers have fully supported these properties and techniques before using them in our projects. We've already been using <a href="https://caniuse.com/" target="_blank">https://caniuse.com/</a> in this class and we will continue to. If you want to know more about Can I Use (including some neat features we have not yet talked about), check out <a href="https://www.youtube.com/watch?v=WM_cKHH7bZ0" target="_blank">The Secrets of 'Can I Use' by Jen Simmons</a>.
