<!-- Student takeaway: -->
<!-- At the end of this lesson, the student will be able to:
- Know that the fetch() method exists
-->
# Fetching data with something other than $.ajax

So far we have been using jQuery's `$.ajax()` method to make our AJAX requests but now that we are entering the Land of React, we won't be relying on jQuery for any kind of DOM manipulation. 

That's okay, because `$.ajax()` is not the only way to make an AJAX request! There are other options that we can explore. Before we do, we want to let you know that **all of these methods of making our requests are promise-based**!

Don't remember what a promise is? Review lesson on promises [here](https://github.com/HackerYou/no-repeat-bootcamp-notes-2018/blob/master/6.9-working-with-asynchronous-events.md#promises).

## `fetch()` 
Modern browsers' Fetch API allows us to make AJAX requests using `fetch()`. This API works in all modern browsers except for IE 11 and Opera Mini. If you need to support older browsers, a polyfill is available. To read more about [what fetch is](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) and `fetch` syntax, [check out this article](https://developers.google.com/web/updates/2015/03/introduction-to-fetch).

## Axios
Axios is a library that does a really great job of simplifying AJAX requests for us. The syntax of Axios is very similar to `$.ajax()`'s. We'll look at the `get` method; the result from the `get` method is a promise.

### Making a GET request with Axios
In the future, we will be using Axios to make AJAX requests in our React apps. 

Here's an example of a GET request using Axios. 

We are going to call the `.get()` method on the `axios` object and pass in the URI of our API as an argument:
```javascript
axios.get('http://api.site.com/api')
```
We can also write a GET request as follows:
```javascript
axios({
  method:'GET',
//a bunch of other stuff
})
```
Same same!

The above examples show that we are sending a GET request to a specified URI.


```js
axios.get('http://api.site.com/api')
  .then((res) => {
    console.log(res);
  }); 
``` 

We can chain a `.then` method, which executes a callback function, logging the result of the Axios call to the console. Axios assumes that the response will be a JSON object, so we don't need to specify any additional options.

If you want to specify query parameters, we can pass them to a configuration object as a second argument where we specify our query params inside of the `params` property like this:

```javascript
axios.get('http://api.site.com/api', {
    params: {
      queryParam: 'value'
    }
  })
  .then(function (res) {
    console.log(res);
  });
```

The above code is the same as doing this:
```javascript
axios( {
  method:'GET',
  url: 'http://api.site.com/api',
  dataResponse: 'json',
    params: {
      queryParam: 'value'
    }
  })
  .then(function (res) {
    console.log(res);
  });
```

### Axios with a proxy server
Under the following conditions, you will need to use a proxy server to access your data: 

* the API requires JSONP
* the data coming back from your API needs to be converted from XML format to JSON
* you need to cache the data
* you need to request insecure data (from an `http` endpoint) from a secure site (`https`) 

If any of these are the case, we recommend using the HackerYou proxy server. Your code will look something like this:

```javascript
axios({
  method:'GET',
  url: 'http://proxy.hackeryou.com',
  //OR url: 'https://proxy.hackeryou.com',
  dataResponse:'json',
  params: {
    reqUrl: 'http://api.site.com/api',
    proxyHeaders: {
      'header_params': 'value'
    },
    xmlToJSON: false
  }).then((res) => {
    console.log(res);
  });
```

#### Specifying query parameters with a proxy server
If you are using a proxy server and want to include query parameters as part of our request (e.g. if you're using the API to search - the word you're searching will be the query parameter), we will have to include a `paramsSerializer` method as a parameter inside of the request object.


```javascript
paramsSerializer: function(params) {
  return Qs.stringify(params, {arrayFormat: 'brackets'})
}
```

This method will be in charge of translating data structures into a readable format to be sent to the server. The `paramsSerializer` method is specific to the HackerYou proxy, because it expects the data to be sent in a very specific way.

In order for us to use this method properly, we will need to install the querystring parsing and stringifying library (called `qs`) as a dependency by running the following command:

```bash
npm install qs --save-dev
```

Next, we will need to import the module inside of our file like this:

```javascript
//React:
import Qs from 'qs';

//if for some reason you're not using React, use the filepath to import the `qs.js` file
  <script src="node_modules/qs/dist/qs.js"></script>
```

Now we should be to use the `paramsSerializer` method inside of our AJAX request like so:

```javascript
axios({
  url: 'http://proxy.hackeryou.com',
  dataResponse:'json',
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },
  params: {
    reqUrl: 'http://api.site.com/api',
    params: {
      queryParam: 'value'
    }, 
    proxyHeaders: {
      'header_params': 'value'
    },
    xmlToJSON: false
  }
  }).then((res) => {
    console.log(res);
  });
```
This method will take the nested `params` key inside of `params` (sorry there are so many params!) and make it look like this `params[queryParam]:'value'`.