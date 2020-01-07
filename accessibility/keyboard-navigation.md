<!-- Student Takeaway -->
<!-- By the end of this lesson students should be familiar with all of the expected keyboard navigation and able to check a website for correct keyboard behaviour -->

# Keyboard Navigation

Ensuring that your websites and apps have proper keyboard navigation is one of the most important things you can do to enable all users. Many users have difficulty using a mouse and rely on a keyboard. This is true for blind users and folks with physical disabilities and even hand tremors. 

Assistive technologies such as a switch control, pointer and sip and puff all emulate keyboard navigation. So When you ensure that keyboard navigation functions as expected, you are supporting more than just keyboard users! 

## Assistive Technology Examples

### Sip and Puff

![Assistive Technology: Sip and Puff](https://hychalknotes.s3.amazonaws.com/sip_and_puff.jpeg)

### Head Pointer

![Assistive Technology: Head Pointer](https://hychalknotes.s3.amazonaws.com/head_pointer.jpg)

### Switch Device

![Assistive Technology: Switch Device](https://hychalknotes.s3.amazonaws.com/switch_device.jpg)

## Tab behaviour

Pressing the `tab` key should move the user to the next *interactive element*. Interactive elements are things like buttons, inputs, selects and links. When you tab to the next element it should receive a **visible focus indicator**. The user should be able to move backwards to the previous interactive element by pressing the `shift + tab` keys.

## Focus order

It is very important that the "tab order" or "focus order" make sense in the document flow. The focus should not jump from the header to the footer for example. It is not enough to ensure that interactive elements receive focus, we must ensure that the order makes sense.

## Interactive Elements

To ensure that keyboard navigation is up to standard, our main focus will be on the interactive elements and how they behave.

### Buttons

When focus is on a button, the user should be able to activate it with the `enter/return` or `space` key. They should be able to tab away from it using `tab` or `shift + tab`.

**Note:** If the button will be opening a new window, this should be announced by a screen reader.

### Links

When focus is on a link, the user should be able to activate it with the `enter/return` key and tab away from it using `tab` or `shift + tab`.

**Note:** If the link will be opening a new window, this should be announced by a screen reader.

### Inputs

The user should be able to navigate to an input using the `tab` key and back from it using the `shift + tab` keys. It should receive focus.

### Radio Groups

When a group of radio inputs receives focus, the individual inputs should be navigated between using the `arrow` keys. Pressing tab should move to the next interactive element, *not* the next radio input within a group.

**Note:** the user should only be able to select one option from a radio group.

### Checkbox Groups

To navigate within a group of checkboxes the user should press the `tab` key. The user should be able activate or deactivate the checkbox that currently has focus by pressing the `space` key. 

### Selects 

To expand (open the menu) and collapse a select element the user should press the `space` key. To navigate through an open list of options the user should press the `arrow` keys. If the menu is open (or any popup/modal menu is open, not just true for select menus), the user should be able to close it at anytime using the `esc` key.

### Custom Widgets

Sometimes we need to build custom widgets such as modals and popups and we will need to handle some important functionality that was given to us for free for the previous native HTML elements. 

In these scenarios it's critical to ensure that the keyboard navigation makes sense, and that any JavaScript event handlers triggered by a mouse also work with the appropriate keys. 

The [ARIA design patterns](https://www.w3.org/TR/wai-aria-practices/) have some great strategies and best practices for handling custom widgets. 

You may need to use tabindex in these cases, so lets talk about the dos and don'ts of tabindex.

## Tabindex

We can use tabindex to control whether an element is "focusable" or not. We can "turn it on" for typically non-interactive elements such as a div, and "turn it off" for interactive elements like a button.

Interactive (focusable) elements have a default `tabindex="0"`. What this means is that if we want to make something like a div become interactive we can add the tabindex attribute and set it to 0:
```HTML
<div tabindex="0">Some div</div>
```

There are some use cases where we might want to disable the interactivity of an element as well. For example, if you have a modal open with an overlay behind it you want to contain the focus and interactivity within that modal as long as it's open. In this case it may be necessary to disable the focus state of interactive elements behind the modal (on the main page) as long as the modal is open. 

To turn off the focus/interactivity we set `tabindex="-1"` on the interactive element. 

**Note:** this is something we would want to handle in our JavaScript as we want to be sure that tabindex reverts back to normal (0) as soon as the modal has been closed. 

Another case where you might need to leverage this strategy is for slide-in menus that are hidden off-screen with a hamburger icon. You would not want interactive elements in that menu to receive focus when they are off screen. In this case we would again use a JS check to handle the focus/interactivity. If the menu is visible on the screen we want the interactive elements to behave normally, and if they are off screen we want them to have a `tabindex="-1"`.

**Caution!** You can add positive integer values to tabindex like `tabindex="1"` or `tabindex="5"`. This determines tab order. But we **don't ever want to do this**. If the tab order of your page does not make sense, you need to change the structure of your HTML! Visually you can reposition things with CSS but the document flow should be what determines the tabindex. 

## Skip Links

Keyboard users will need to tab through every possible interactive element in the page unless they are using the rotor for navigation. It is very helpful to provide users with a "skip link" at the top of the document which allows them to skip to the main content, potentially bypassing dozens of interactive elements in an intricate nav menu. 

The most straight forward way to create a skip link is to put an anchor tag at the top of the page that says something along the lines of "skip to main content" and connect it to an anchor tag at the beginning of the main section. 

Sometimes you will get pushback for design reasons about having a visible skip link. In this case we can keep the same structure but hide the link visually until it receives focus and then make it visible. Again this visible state is something you would likely handle with JavaScript. 

If you use this approach it's a good idea to consider using CSS animations to fade it out if the user tabs away incase they tab too quickly and the skip link disappears suddenly. Remember, skip links are beneficial to more than just blind users!
