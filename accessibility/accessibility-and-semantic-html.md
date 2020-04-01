<!-- Student Takeaway -->
<!-- By the end of this lesson students should be able to recognize the importance of semantic HTML for accessibility and how to make better choices than just divs and spans to create their structure. They should understand how users can navigate websites using headings and how to access the rotor. -->

# Semantic HTML and Accessibility

Arguably the biggest accessibility improvement you can make to a website is to have the content created with proper semantic HTML and hierarchy. 

The word semantic means to give something meaning. When you use a `div` or `span` element there is no real structural meaning beyond a generic box for content. Before reaching for one of these elements ask yourself: what is this content? If it's text, reach for a text element. If it's a list, reach for an `ol` or `ul` with `li` elements inside. If it's a button, use a `button` element, if it's a link, use an `a` tag.

Writing semantic HTML greatly improves the experience for screen reader users because the type of content will be announced. But it's also a curb cut (see intro to accessibility notes for definition) because proper semantics increase search engine optimization and better communicate your intention to other developers on your team. 

## Headings

One of the most helpful things we can do for screen reader users is to properly organize the hierarchy of our page with headings using `h1` though `h6` tags. This is because many screen reader users leverage headings to navigate the page. So although using a `p` tag is technically a semantic element, if something is a heading or sub-heading this would be the wrong text element choice.

Some things to keep in mind:

* You should only ever have one `h1` element on the page.
* Your hierarchy should make sense in the document flow. In most cases you should not be skipping from an `h1` to an `h4` and then back to an `h2`.
* Try to separate your thinking about the heading styles from the heading hierarchy. Ask yourself, if you were to strip away all the CSS, does the hierarchy make sense? You can style an `h2` to look like an `h4` easily without making improper hierarchy decisions. 

### Rotors

Screen reader users navigate using headings or other elements with a tool called the rotor. This acts like a menu or table of contents. There are many screen readers out there but we will look at navigation using the Mac VoiceOver utility and NVDA for PC.  

### Mac users 

You can access the rotor within the VoiceOver utility's built-in screen reader. You will need to have the VoiceOver screen reader open, the shortcut for this is: `command + f5`. With this utility running you can then open the rotor with the shortcut `ctrl + opt + u`. You can use the shortcut `ctrl + opt + h` to jump to the next heading.

**Note:** Whenever you see the keys `VO` referenced, this is short for VoiceOver and refers to `ctrl + opt` unless you have customized your settings. So you may notice `ctrl + opt + h` written as `VO + h` in the article below.
 
This article from Deque University has a good overview of the [Mac VoiceOver screen reader shortcuts](https://dequeuniversity.com/screenreaders/voiceover-keyboard-shortcuts).

### PC Users

Using the free NVDA screen reader software PC, users can navigate with a rotor.

To open the screen reader use the shortcut `Control + Alt + N`. To navigate to the next heading use the `h` key and to specify the heading level use the `1` through `6` keys.

This article from Deque University goes over all the [NVDA screen reader shortcuts](https://dequeuniversity.com/screenreaders/nvda-keyboard-shortcuts). 

## Landmarks

It is very important that we break our page up into regions using semantic landmarks. The landmark elements are: `header`, `nav`, `main`, `aside`, `form` and `footer`. This allows a user to jump to the part of the page they are concerned with, and know where they are at any given time. 

Prior to the release of HTML 5, these elements were not available. You can also designate these landmarks on any element with `ARIA role` attributes (more on ARIA in a later lesson).

The mapping of the role attributes to the elements is:

* `<header>` => `role="banner"`
* `<main>` => `role="main"`
* `<nav>` => `role="navigation"`
* `<aside>` => `role="complementary"`
* `<form>` => `role="form"`
* `<footer>` => `role="contentinfo"`

**IMPORTANT NOTE:** You shouldn't need to assign these ARIA roles if you're using the correct landmark elements! Why put a `role="contentinfo"` on a `div` when you could use a `footer` element? It's important to be aware that these exist, as you may encounter them in the wild, but we can do better 😎.

There is some debate about this in the accessibility community because HTML 5 does not yet have 100% screen reader support, particularly for users with older technology. If you are concerned about covering every possible user the best solution would be to use a combination of both the correct landmark element and the addition of the ARIA role attribute like so:

```html
<header role="banner">This is a header</header>
```

As with anything in web development, it's important to get a sense of who your users are and what browsers and operating systems they are using so you can provide the correct support.

## Buttons and Links

It is a common issue in web development to see buttons styled as links and links styled as buttons. You will also see divs and other elements styled to look like one of these two elements.

Just use a button element to achieve a button and an anchor tag to achieve a link! The browser gives us a lot of expected functionality for free when we use the correct semantic elements, such as correct keyboard functionality and screen reader behaviour. 