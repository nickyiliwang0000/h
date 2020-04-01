# Accessibility Testing

Web accessibility should be considered from the design stage of the project as well as throughout the development of the project. In addition to making sure that our [HTML is semantic](https://github.com/HackerYou/bootcamp-notes/blob/master/accessibility/accessibility-and-semantic-html.md) and our [CSS follows best practices](https://github.com/HackerYou/bootcamp-notes/blob/master/accessibility/accessibility-and-css.md), we should also get into the habit of testing our projects to make sure they are WCAG 2.1 compliant.

## Web accessibility checklist

[WCAG 2.1](https://www.w3.org/TR/WCAG21/) is the standard reference of guidelines for accessibility. While this document is detailed and extensive, it is not always easy to navigate and read through. 

[WebAIM](https://webaim.org/) is a non-profit organization that provides services and training for web accessibility. They've developed a couple of tools we can use to help us with the process. Including this handy checklist! - [WCAG 2 Checklist](https://webaim.org/standards/wcag/WCAG2Checklist.pdf)

If you can satisfy all the criteria on this checklist, congratulations, your project is gold standard accessible!

## Testing tools

Once you feel like you've satisfied all the criterias on the checklist, there are a couple of tools you can use to help us audit our project. 

- **[WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org/)**
The tool will provide feedback on a site url you've entered. It will highlight errors you should address and provide suggestions on how to address them. It exists as [Firefox and Chrome extension](https://wave.webaim.org/extension/) as well.  
- **[Accessibility Insights for Web](https://chrome.google.com/webstore/detail/accessibility-insights-fo/pbjjkligggfmakdaogkfomddhfmpjeni?hl=en)**
Extension similar to WAVE developed by Mircosoft, which means it's available on Mircrosoft Edge!
- **Lighthouse**
Lighthouse is an open-source tool owned by Google. You can use it as a [Firefox](https://addons.mozilla.org/en-US/firefox/addon/google-lighthouse/) or [Chrome](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk?hl=en) extension. If you are using the Chrome browser, you can also access it without the extension via your dev tools under the *Audits* tab. Lighthouse is great not only for accessiblity audit, it can also run peformance and best practices reports. 
- **[aXe](https://www.deque.com/axe/)**
Similar to WAVE and Lighthouse, [aXe](https://www.deque.com/axe/) is a browser extension tool. It is developed by [Deque](https://www.deque.com/), a company that provides accessibility solutions and training. The aXe tool is geared more towards developers and works well with web apps. 

W3C also provides an extensive list of tools [here](https://www.w3.org/WAI/ER/tools/).

**For more resources on accessibility, check out [additional resources for accessibility](https://github.com/HackerYou/bootcamp-notes/blob/master/stuff-you-need-to-know/resources-and-cheatsheets/accessibility-resources.md) in the notes.**