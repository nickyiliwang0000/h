<!-- Student takeaway -->
<!-- By the end of this lesson, the student should know:
- That AJAX is used to get data without having to refresh the page
- How to write an AJAX request using jQuery's $.ajax() method
- How to troubleshoot common API errors (e.g. JSONP, disabling CORS, using a proxy, checking the Network tab)
- That a proxy is an intermediary between a browser and a server
- That JSON data can be accessed and manipulated like a regular JavaScript object
-->

# Accessing API data with AJAX

## AJAX

So far we've figured out how to get data from an API by visiting URLs in our browser, but what if we want to work with the data inside our own website or app?

This is where we'll use _AJAX_ (Asynchronous JavaScript and XML) because it allows us to send and receive data _asynchronously_ (i.e. without having to refresh the page). 

> AJAX got its name a long time ago, when XML was the expected response format. Today JSON is more common as a response format but the name remains.

We can use AJAX to request data from an API, then we can use JavaScript to use the returned data to update the current page **without a browser refresh**.

AJAX is used all over the web to help provide continuous user experiences. Twitter uses AJAX to implement the infinite scroll (i.e. it loads more tweets when you get to the bottom of the page). Google uses AJAX to auto-complete search suggestions, and Facebook uses AJAX to instantly show new comments on a post.

## `$.ajax` with jQuery
There are many ways to perform AJAX requests but they do have some cross-browser quirks, so we'll work with jQuery's `$.ajax()` method to handle our requests. 

[Looking at the documentation](https://api.jquery.com/jQuery.ajax/), the `$.ajax()` method lets us specify the URL we're using and a settings object in two different ways:
```js
$.ajax('https://www.urlWeAreRequestingFrom.com', {
    this:'is',
    the:'settings',
    object:'🎉'
})
// is the same as
$.ajax({
    urlWeAreRequestingFrom:'https://www.urlWeAreRequestingFrom.com', 
    more:'settings',
    other:'settings',
    someOther:'settings 🎉'
})
```
We're going to do it the second way so that all the information is in one place, but you'll see both in the wild.

If the `$.ajax()` method is successful, it returns the information we're requesting. Once we have it in the browser ([check the 'Network' tab](https://github.com/HackerYou/bootcamp-notes/blob/10ee6cbd78aaad16a0b1718eda9fa27ad6dd90cb/06-applied-javacript/6.4-accessing-api-data-with-ajax.md#debugging-ajax-requests)), we need to tell the browser what to do with that information. We can chain a `.then()` method onto our `$.ajax()` method like this: `$.ajax().then()`. 

> `.then()` is a special JavaScript method; we'll learn more about it the deeper we get into AJAXland.

Let's try this with the TTC API:

```js
$.ajax({
  url:'https://myttc.ca/finch_station.json',
  method: 'GET',
  dataType: 'json'
}).then(function() {
  console.log('It worked!');
});
```

Open up [the starter files for your first AJAX request](https://hychalknotes.s3.amazonaws.com/my-first-ajax-request.zip) to see this AJAX request in action.

### Oh no! An error!
The result in the console should be an error:

```bash
Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at https://myttc.ca/finch_station.json. (Reason: CORS header ‘Access-Control-Allow-Origin’ missing).[Learn More]
```

Click the `Learn More` link and you'll be redirected to [the MDN docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/Errors/CORSMissingAllowOrigin) telling you that a _CORS_ (cross-origin resource sharing) header is missing. 

> When we make an _HTTP_ (hypertext transfer protocol) request to a different domain than the one that hosts the file with the request in it, we are creating a _cross-site_ HTTP request. HTTP requests come with information for the browsers called _headers_. Think of headers like the front of a letter: they say who the message is from, who it's to, and where the addressee expected to be located. Most servers will not allow HTTP requests from external sources for security reasons - kind of like how you don't open emails from unknown senders because it could be a virus.

AJAX is restricted by the _same-origin policy_ which [basically states](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) that people can only send emails to themselves (i.e. AJAX requests to a domain/subdomain can only come from that same domain/subdomain). 

#### How do we send emails to other people!?
##### JSONP
One way of getting around the same-origin policy without messing directly with the headers is to ask for a data format called _JSON with padding_ (JSONP) in your AJAX request. The "padding" is a JavaScript wrapper that the server has set up. 

When we request JSONP in our `$.ajax()` method, jQuery injects a script tag into our website temporarily. The script's `src` attribute points to a bit of JavaScript on the server from which we requested data. The server then wraps the JSON data in a JavaScript function (the aforementioned padding). This function becomes available to us, gets executed, and we get our data. Then, the script tag is removed from our website.

This technique doesn't break the same-origin policy because you are requesting **JavaScript** from another server, not JSON data. Requesting JavaScript from another domain is an integral part of the modern web and we do it all the time (e.g. loading jQuery from Google's CDN).

#### If you API doesn't have a JSONP wrapper set up

You can try one of the follow techniques: 

##### Disabling CORS
Some APIs have opted out of the same-origin policy by disabling CORS in their headers. This is a newish protocol and we cannot force any API to use it: it has to be done server-side. Unfortunately the TTC API doesn't use CORS.

##### What if that still doesn't work?
Sometimes you can't get data from an API even when you request JSONP:
```bash
browser
{\__/}
( • . •)
/ > ✉️  server, can i have the data?

server
{\__/}
( 0 _ 0)
💾 <\  i do not know you
```

In that case, you can try using a _proxy server_:

```bash
browser
{\__/}
( • . •)
/ > ✉️  proxy server, can i have the data?

proxy
{\__/}
( • - •)
/ >  lemme see your request?

proxy
{\__/}
( • . •)
/> 💾️ <\ thank u, browser. brb

proxy
{\__/}
( 0 - 0)
/ >  ✉️  hey server, can i have the data?

server
{\__/}
( 0 _ 0)
/ > 💾 here u go pal

```
A proxy server is a go-between that can speak both to the browser that's requesting data and the server from which the browser is requesting data.

```bash
proxy
{\__/}
( • - •)
/ > 💾 here u go browser pal

browser
{\__/}
( u . u)
/> 💾 <\ thank u, proxy
```

Browser-to-server communication is sometimes blocked via CORS but server-to-server communication is more open. We have a proxy server with great documentation right [here](https://github.com/hackeryou/json-proxy) for situations like that!

### Let's fix our error
Let's change the `dataType` in the AJAX request in `my-first-ajax-request.html` from `json` to `jsonp`.

```js
$.ajax({
  url:'http://myttc.ca/finch_station.json',
  method: 'GET',
  dataType: 'jsonp'
}).then(function() {
  console.log('It worked!');
});
```

You should see `It worked!` in the console. But where's the data? We can see it in the 'Network' tab, but we can't use it in our JavaScript yet. 
![Successful AJAX request in the Network tab of Firefox](https://hychalknotes.s3.amazonaws.com/successful-ajax-request-in-network-tab.png)

Remember the `.then()` method?

The `.ajax()` method retrieves the information and upon the completion of the request, [the docs](https://api.jquery.com/deferred.then/) tell us to pass it into the `.then()` method that handles our next steps.

The `.then()` method has three parameters: 
1. what to do when the request is successful  (required)
1. what to do when there is an error (optional)
1. what to do while the request is in progress (optional)

We will only be using the required parameter right now.

[The docs](https://api.jquery.com/deferred.then/) say that this first parameter is expected to be a function; that's what we've got in there, we're using an anonymous function to call our console.log:
```js
$.ajax({
  url:'http://myttc.ca/finch_station.json',
  method: 'GET',
  dataType: 'jsonp'
}).then(function() {
  console.log('It worked!');
});
```

We could also do the same using a named function, which we define elsewhere:
```js
$.ajax({
  url:'http://myttc.ca/finch_station.json',
  method: 'GET',
  dataType: 'jsonp'
}).then(resultsFunction);

function resultsFunction(){
  console.log('It worked!');
}
```

This is the function that will run when the request is successful. We can expect to have some JSON data from the API if the request is successful, so we'll pass that data as an argument called `result`:

```js
$.ajax({
  url:'http://myttc.ca/finch_station.json',
  method: 'GET',
  dataType: 'jsonp'
}).then(function(result) {
  console.log('It worked!');
});
```

When a function calls another function like this, we say that second one is the _callback function_. We've previously seen callback functions in event handlers:

```js
$('h1').on('click', function(){
  // here is the content of the callback function
})
```

Let's make our callback function do something! Let's log the data we got back from the API:
```js
$.ajax({
  url:'http://myttc.ca/finch_station.json',
  method: 'GET',
  dataType: 'jsonp'
}).then(function(result) {
  console.log('It worked! : ', result);
});
```

You should see our `It worked!` success message as well as an object containing _payload_ (another way of saying "the result of an API call") in the console.

### Working with JSON data

Once we can see our payload in the console, clicking on the little arrow next to it will open up the object for inspection. jQuery has _parsed_ (read and converted) the JSON into a JavaScript object so we can work with the returned data in a familiar way. 

We can use the parameter name we created (`result`) to refer to the object and access entries on it using dot notation:

* `result.time` gives the time the TTC server was pinged for information. 
* `result.stops` gives an array of all the vehicle stops in and around the station.

We can do all the usual JavaScript and jQuery things with the data, like store the values in variables:

```js
let busRoute = result.stops[1].routes[0].name;
let nextBusLeavingTime = result.stops[1].routes[0].stop_times[0].departure_time;
```

Or update the DOM:

```js
$("p.nextDeparture").html("The next " + busRoute + " bus leaves at " + nextBusLeavingTime);
```

#### Exercise: Working with `$.ajax()`

Get some practice debugging and working with `$.ajax()` these [these practice exercises](https://hychalknotes.s3.amazonaws.com/ajax-practice-bootcamp.zip). Don't look at the solution until you've given it your best shot!

### Debugging other AJAX request errors
Sometimes it's not a JSONP or CORS issue. Sometimes there's an error message you don't understand. Follow these steps:

1. Open up your dev tools

2. Click on the 'Network' tab

3. Click the 'Filter' icon to choose which requests show up in this panel. You'll notice stylesheets, scripts, and images all show up. Choose 'XHR' to limit the view to AJAX requests.
  * Firefox:

    ![network filter on Firefox](https://hychalknotes.s3.amazonaws.com/network-filter-firefox.png)
  * Chrome:

    ![network filter on chrome](https://hychalknotes.s3.amazonaws.com/network-filter-chrome.png)

4. Refresh the page to see the requests in real time.

5. Clicking on a request will take you to a panel where you can see the response header, response body, and a bunch more information.
  * Firefox:

    ![selected XHR request information panel in Firefox](https://hychalknotes.s3.amazonaws.com/network-tab-headers-firefox.png)
  * Chrome:
  
    ![selected XHR request information panel in Chrome](https://hychalknotes.s3.amazonaws.com/network-tab-headers-chrome.png)

Using the information here will help tremendously in debugging AJAX requests. If you don't see your request at all, check for things like syntax errors. If the request was made but the result wasn't as expected, have a look at the headers and body of the response.

HTTP status code | means...
:--:|--
1xx | The server needs a second to look for some stuff.
2xx | The server has given you what you asked for.
3xx | The server wants you to go somewhere else.
4xx | You asked for something wrong.
5xx | Something's wrong with the server.
