## Additional Media Queries

#### Media query for orientation

Orientation is which way you are holding a device: portrait or landscape.

![iPhone in portrait and landscape mode](https://hychalknotes.s3.amazonaws.com/iPhone-5-Black-White-MockUp.png)

It's less important to think about the width of the landscape screen (width media queries can direct your styles) and more important to think about **why** the user holding their phone at that particular orientation. If they are holding the device in portrait rather than landscape, there may be a few things to consider:

  * How many hands might they be using to touch the screen? 
    * Are they in a grocery store line with one hand available? 
    * Are they sitting on the couch getting some hardcore screen time in?
  * Where might you want to place certain controls (e.g. buttons on an online game) when the screen is landscape vs. portrait?

A media query like this one will target iPad-sized tablets that are oriented in landscape mode:

```css
@media (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: landscape) {
  /* styles */
}
```

For most cases, **you will be okay using width media queries** instead of orientation. 

But we tell you so you know. 🙏

#### Media query for pixel resolution

Pixels can bend your mind (especially if you are coming from a print background where everything is in 300 DPI and measured in inches). Pixels don't necessarily correspond to the physical size of the screen: a 50-inch 1080p TV is 1080px high while a 9-inch ipad is 1536px high. Some devices on the market today have _High Density Pixels_ (HiDPI). The marketing term for this kind of resolution is "retina". The number of pixels on these devices is doubled and crammed into the same sized screen as their regular density kinfolk, which results in a sharper image.

However, very little has changed for our CSS. A 640px-wide HiDPI phone screen still registers as 320px wide. This is nice because we don't need to write another set of CSS just for HiDPI devices. The values for our text, borders, colors, etc. are all normalized for HiDPI.

Here's a helpful graphic from [Smashing magazine](https://www.smashingmagazine.com/2012/08/towards-retina-web/) on the topic:

![retina display graphic](https://hychalknotes.s3.amazonaws.com/standard-retina-comparison.png)

The one thing that has changed is that our images and graphics are blown up to 2x their natural size which can result in blurry images. The solution to this issue is to use a device resolution media query to swap in images that are 2x the size of the normal ones when the user is on a HiDPI screen.

```css
.buyButton {
  background: url(images/buttonBG.png) center no-repeat;
}

/* give HiDPI screens a bigger background image */
@media  (-webkit-min-device-pixel-ratio: 2), 
    (min-resolution: 192dpi) {
      .buyButton {
        background:url(images/buttonBG@2x.png) center no-repeat;
        background-size: 50%;
        /* Because background images appear at native dimensions, it's recommended to scale the retina-sized images down to 50% 
        so they're the right size, just sharper. */
    }
}
```

Note that above we use both the more widely-functional `min-resolution` query and the vendor-prefixed `-webkit-min-device-pixel-ratio` to account for a few specific special-requirement cases (for details, take a look at [CanIUse](https://caniuse.com/#feat=css-media-resolution)).

#### Other Media Queries
* **monochrome**: targets monochrome screens (like Kindles)
  * **progressive scan**: important pretty much only if you are making TV web apps
  * **color**: if you could somehow get a web browser on an old gameboy color, you could target low or no bits of color.
  ```css
  @media all and (color:0) and (width:160px) and (height:144px) {
    /* Target original gameboy */ 
  }
  ```