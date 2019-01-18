# Cross-browser testing
Testing your code across multiple browsers can be a pain, but it's crucial to do if you want to maintain a good experience for all users.

There are five main browsers:

1. Chrome
1. Firefox
1. Safari
1. Internet Explorer/Edge
1. Opera

Chrome has a rapid release schedule and it automatically updates, so you usually only have to support the latest version.

Firefox recently switched to a similar schedule, so supporting the latest version is 100% okay.

Safari is pretty aggressive about updating as well, most support the latest two versions of Safari. 

Opera has recently abandoned their browser engine and adopted Chromium / Blink, which is the engine behind Chrome. So, testing for Chrome is essentially testing for Opera.

Internet Explorer is a pain for most developers. Microsoft recently discontinued support on older versions, but older versions are still in use. If your client uses an older version of IE, you'll need to support it. 

Right now, most developers support back to IE11, which is considered the last of the buggy browsers to support. 

If you're catering to a modern audience, you may be okay supporting the latest version. When in doubt, look at analytics data on what browsers site visitors are actually using.

![](https://hychalknotes.s3.amazonaws.com/purpose.png)

### Testing Internet Explorer

#### IE Tester
IE tester for Internet Explorer: [http://www.my-debugbar.com/wiki/IETester/HomePage](http://www.my-debugbar.com/wiki/IETester/HomePage) - lets you open IE in every version. We encourage you to check site analytics, to see if supporting any versions prior to IE11 is even necessary. 

#### Virtual Box + Modern.ie
Regardless of PC/MAC/Linux, you can run a copy of windows right inside of your operating system. Microsoft knows the pain of testing on multiple versions of IE, so they have provided images of windows with different versions of IE loaded onto them. You can download them at [https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/](https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/). These are huge downloads, so plan to do so on a stable internet connection.

To run them, you need a free program called Virtual Box — [https://www.virtualbox.org/](https://www.virtualbox.org/).

You can download a copy of windows specially made for testing IE on <http://modern.ie>

### Testing Firefox, Chrome & Opera
For Google Chrome, you don't need to worry about older versions as much - it auto updates. It is always wise to check your website on both a PC and Mac version of both. For Firefox and Opera, it is a similar story, they are what we call <a href="https://www.techopedia.com/definition/31094/evergreen-browser" target="_blank">Evergreen Browsers</a>. They update frequently and automatically. However, you should still continue to test your site on these browsers! 

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


### Mobile Testing
All tools aside, testing on actual hardware is always preferable. 

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

In addition to testing our sites, we should also be building sites with browser support in mind. Web development moves really fast. There will be new properties introduced in the CSS specifications in the future. So it's important for us to know which browsers have fully supported these properties and techniques before using them in our projects. We've already been using <a href="https://caniuse.com/" target="_blank">https://caniuse.com/</a> in this class and we will continue to. If you want to know more about Can I use (including some neat features we have not yet talked about), check out <a href="https://www.youtube.com/watch?v=WM_cKHH7bZ0" target="_blank">The Secrets of 'Can I Use' by Jen Simmons</a>.