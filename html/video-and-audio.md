<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- What `controls` & `autoplay` do to the video element 
- How to provide different sources to a `video` or `audio` element
- Where to find information about playing video on mobile
- Where to find information about `video` and `audio`accessibility
-->

# Video and audio 
## The `video` element

One of the tools available to us as of HTML5 is native video. (Before, we had to use a plug-in called Flash.) The video tag is supported [in all major browsers](https://caniuse.com/#feat=video)!

The `video` tag is similar to the `img` tag: we provide it with a `src` attribute that points to our video file's location. 

Adding this tag to a new HTML document:

```html
<video src="https://hychalknotes.s3.amazonaws.com/OurLearningLoop.mp4">
  Your browser does not support the video element.
</video>
```

### Controls

A video by itself doesn't make much sense, as there's no way to stop, pause, or resize it. By adding  `controls` (which is the same as `controls=true`) attribute to the tag, we can tell the browser to show its built-in controls for the video. 

Add the `controls` attribute to your HTML file:
```html
<video src="https://hychalknotes.s3.amazonaws.com/OurLearningLoop.mp4" controls>
  Your browser does not support the video element.
</video>
```

Each browser also has their own policies regarding autoplay for HTML5 videos.

As of March 2019, these are the rules for autoplay of video on desktop:

browser | allow `autoplay` with sound | allow `autoplay` with sound with `controls` | allow `autoplay` with `muted` 
---|:---:|:---:|:---:
Safari| no | yes | yes
Firefox| no | no | yes
Chrome| no | no | yes


[More on the specifics of `video`](https://caniuse.com/#search=video) attributes.

Add the `autoplay` and `muted` attributes to your HTML:
```html
<video src="https://hychalknotes.s3.amazonaws.com/OurLearningLoop.mp4" controls muted autoplay>
  Your browser does not support the video element.
</video>
```

There are a couple of known exceptions to the behavior of `autoplay`:
* Autoplay with sound on Chrome desktop is possible if the user has interacted with the domain or [passed the Media Engagement Index threshold](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes#mei), meaning they've previously played the video with sound. 
* Videos on desktop Safari can autoplay with sound if the user has set their browser preferences to allow it.

#### Autoplay on mobile devices
You may notice that videos you set to `autoplay` do not always do so on mobile devices. Many mobile operating systems have disabled this feature. Since videos often use a lot of data to load, these operating systems prevent videos from automatically playing so that users do not end up using too much of their monthly data allowance. Again, each browser has its own specifications for mobile video play.

Here are a couple of known issues:
* On Chrome's mobile browser, a video can autoplay with sound if the user has added the webpage to their home screen. [Click here](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes) for more about Chrome's autoplay policy.
* There are specific scenarios in Safari's mobile browser on iOS that will stop or continue an autoplaying video, outlined [here](https://webkit.org/blog/6784/new-video-policies-for-ios/).

### Providing fallbacks

Today, all major browsers support the `.mp4` format for video. Older browsers sometimes require different formats, like `.ogg` or `.webm`. If we have them, we can include these fallbacks by using a `source` element inside the `video` element. The `source` element has an `src` attribute, where we put the path to each video file. The browser will run through until it finds one it can read. If it can't read any, it'll render the text that comes after.

```html
<video autoplay controls>
  <source src="http://hackeryou.com/wp-content/themes/hackeryou/assets/images/videos/OurLearningLoop.mp4" type="video/mp4">
  <source src="http://hackeryou.com/wp-content/themes/hackeryou/assets/images/videos/OurLearningLoop.ogg" type="video/ogg">
  <source src="http://hackeryou.com/wp-content/themes/hackeryou/assets/images/videos/OurLearningLoop.webm" type="video/webm">
  Your browser does not support the HTML5 video element.
</video>
```

### Some other `video` attributes
attribute | value | description
---|---|---
`src` | URL |Specifies the URL of the video file
`autoplay` | boolean | Specifies that the video will start playing as soon as it is ready
`controls` | boolean |Specifies that the video will start playing as soon as it is ready
`muted` | boolean| Specifies that the audio output of the video will not be heard
`loop` | boolean | Specifies that the video will start over again, every time it is finished
`poster` | URL | Specifies an image to be shown while the video is downloading, or until the user hits the play button
`preload` |`none` `metadata` `preload` `auto`| Specifies if and how the author thinks the video should be loaded when the page loads
`height` | pixels | Sets the height of the video player.
`width` | pixels | Sets the width of the video player.

## The `audio` element

The `audio` element looks very similar to the `video` element. It uses similar attributes and you can provide multiple sources to it different file formats.

Add this to your HTML file:
```html
    <audio controls>
      <source src="https://hychalknotes.s3.amazonaws.com/service-bell_daniel_simion.mp3" type="audio/mp3">
      <source src="https://hychalknotes.s3.amazonaws.com/service-bell_daniel_simion.ogg" type="audio/ogg">
      Your browser doesn't support the HTML5 audio element.
    </audio>
```

## Video and audio accessibility
In order to make video and audio accessible, you will need to provide a legible transcripton for your users. You can either type it up yourself, find a volunteer, or turn to a third party service that will create the transcript for a fee. The transcript should be provided on the page (like on [Radiolab's website](https://www.wnycstudios.org/story/no-part-3)) or implemented as captions or with the `track` tag.

```html
<!-- example taken from https://developer.mozilla.org/en-US/docs/Web/Apps/Fundamentals/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video -->
<video id="video" controls preload="metadata">
   <source src="video/sintel-short.mp4" type="video/mp4">
   <source src="video/sintel-short.webm" type="video/webm">
   <track label="English" kind="captions" srclang="en" src="captions/vtt/sintel-en.vtt" default>
   <track label="Deutsch" kind="subtitles" srclang="de" src="captions/vtt/sintel-de.vtt">
   <track label="Español" kind="subtitles" srclang="es" src="captions/vtt/sintel-es.vtt">
</video>
```

More about how to implement subtitles and captions [here, from MDN](https://developer.mozilla.org/en-US/docs/Web/Apps/Fundamentals/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video).

**Audio descriptions** should also be provided when necessary. Audio description will explain what is in the visuals so that the video is accessible to people who cannot see it. Most videos, however, will not require audio description. For example, you do not need to provide audio description of people talking or text on a slideshow if it has already been read out by a presenter in the video. 

**Sign language** is not required but should be included when possible. For more information on how to make audio and videos accessible, [check out the W3C Multimedia Accessibility FAQ page](https://www.w3.org/2008/06/video-notes)
