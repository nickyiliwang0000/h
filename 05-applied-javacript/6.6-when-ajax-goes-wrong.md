## Debugging AJAX Requests

### Seeing AJAX Requests

It's often useful to see what the browser is doing behind the scenes when we're making AJAX requests. Luckily, dev tools can help us here.

1. Open up your dev tools

2. Click on the Network tab

3. Click the filter icon to choose which requests show up in this panel. You'll notice stylesheets, scripts and images also show up here. Choose XHR to limit the view to AJAX requests only.

Chrome

![network filter on chrome](https://hychalknotes.s3.amazonaws.com/network-filter-chrome.png)


Firefox 

![network filter on firefox](https://hychalknotes.s3.amazonaws.com/network-filter-firefox.png)

4. Refresh the page to start capturing requests in the Network panel.

5. Clicking on a request will take you to a panel where you can see the response header, response/body, etc.

Using the information here will help tremendously in debugging AJAX requests. If you don't see your request at all, check for things like syntax errors. If the request was made but the result wasn't as expected then have a look at the headers and body of the response.