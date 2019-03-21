# Reading API documentation

Learning how an API works will take some time. Well documented APIs have enough information and examples to get you started. The examples should show how to make the request and what the response data looks like. Spending time reading this information helps a lot. So it can't be stressed enough, **read the documentation carefully**.

Tips for reading API documentation: 

1. Make sure you understand REST & HTTP requests. The vocabulary(`GET,POST,PUT,DELETE`) will make the documentation much easier to understand.
2. Look for information that you really need (covered below).
3. Explore and play around (nothing beats hands-on experience).

## Find the API documentation
To locate API docs, check to see if they're linked off the service's main page or try searching for the name of the service + "API".

Let's try this with the Rijksmuseum API. You should be able to find 
<http://rijksmuseum.github.io/>

## Response format
Next we need to know how the responses of this API are delivered to us. Common formats you'll come across are XML and JSON. If we check the **Parameters** section of the docs, we see we can get a response in the following formats: *xml, json, jsonp* Try to stick to APIs that return JSON. It's the easiest to work with in JavaScript.

## CORS or JSONP?
Remember the "same origin policy" that prevents one domain from requesting data from another?  We need to find out if the API uses JSONP or CORS to get around that restriction. Since JSONP is a valid response format, we can use that.

## Limitations & Authentication
To prevent spammy requests, most APIs have restrictions on who can make requests and how many requests can be made in a given time frame. You'll often need to sign up for an API key that authorizes you to make requests.  

How do we get an API key? Under **Access to the API** it says:

> To access the data and images, you will first need to obtain an API key. You can do this via the advanced settings of your Rijksstudio account. You will be given a key instantly upon request. Every request to the API must be accompanied by this key.

Head over to <https://www.rijksmuseum.nl/en/mijn/gegevens> and create an account. Change the language to English, then create a new account. Once logged in, visit your account settings and scroll down to the Advanced section. Fill out the required information. The request for an API key should be granted immediately. Save the API key somewhere safe.

![](https://hychalknotes.s3.amazonaws.com/Rijksmuseum-api-profile.png)

## Base URI
This is a RESTful API so all requests should be structured something like this:

`<base_url>/<endpoint>?params=value`

The first section of the documentation and the sample request, 

`https://www.rijksmuseum.nl/api/nl/collection/sk-c-5?key=fakekey&format=json` 

provides us with clues as to how to use this API.

`https://www.rijksmuseum.nl/api/` is the **base uri**. All requests will start with this.<br>
`/nl/collections/` is the **endpoint**. As noted, we'll want to use `/en/` in our requests to ensure we get results in English. <br>
`/sk-c-5` is the **ID of a single item** in the collection<br>
`?key=fakekey&format=json` are **query string parameters** that get passed along with our request to specify additional information. The docs here state that every API request should specify a key and a format.

## Endpoints

The Rijksmusuem offers four different endpoint for us to work with. Endpoints determine which data set we are accessing. Here, we see we can access public data on the collection, web page content, user created sets of art, and an events calendar.

## Exploring an Endpoint
Let's take a look at the **Collections** endpoints.  Scrolling though, there are three different resources we can access.  

`/api/[culture]/collection` for accessing the full collection<br>
`/api/[culture]/collection/[object-number]` for accessing a particular item<br>
`/api/[culture]/collection/[object-number]/tiles` for accessing image data as a set of tiles of a particular item<br>

## Playing around with an API

Lets try making a request using the [Postman](https://www.getpostman.com/) app. Postman will provide us with a friendly GUI (graphical user interface) where we can build HTTP requests and get back detailed responses.

![](https://hychalknotes.s3.amazonaws.com/postman-min.png)

Let's look at this together.

### Getting Collection info

Add the /collection/ endpoint as the destination for our request and then click "Launch Request". hurl.it will format the response nicely.

Destination: https://www.rijksmuseum.nl/api/en/collection/

In postman make sure you click params beside the URL and add `key` as a URL param with your API key, then it send.

The "collection" resource (JSON object) is composed of four properties.

1. ellapsedMilliseconds => number
2. count => number
3. artObjects => array of objects


### Refining results with Parameters

The count tells us there are thousands of results, but we're only getting back a few detailed listings. If we want to get the more, we can add another parameter to our request (eg. `&p=2` after your API key and format parameters). Try adding that to postman and notice how the results change. 

This API also allows us to specify how many posts per page we want to retrieve. Try adding a the post per page parameter `ps` with a small value like `3` and see how what you get back. Limiting the amount of data we initially retrieve is often referred to as pagination. This practice improves response times and helps make the response data easier to handle.

The artObjects now shows the 3 pieces we asked for and some brief info on each of them. Here's some of the data for a single one:

```js
"artObjects": [
    {
      "links": {
        "self": "https://www.rijksmuseum.nl/api/en/collection/BK-NM-3888",
        "web": "https://www.rijksmuseum.nl/en/collection/BK-NM-3888"
      },
      "id": "en-BK-NM-3888",
      "objectNumber": "BK-NM-3888",
      "title": "Virgin and Child",
      "hasImage": true,
      "principalOrFirstMaker": "Adriaen van Wesel",
      "longTitle": "Virgin and Child, Adriaen van Wesel, c. 1470 - c. 1480",
      "showImage": true,
      "permitDownload": true
      ...
    }
```

If we wanted to get more information about this particular art item then the `objectNumber` from the original results will be handy. We can make another request, this time to `/collection/[objectNumber]`, to get more detailed info.

Similarly, we can retrieve the tiled image data by making a new request to `collection/[objectNumber]/tiles`.

#### More parameters

Note that there are lots more options for refining results. You can search by artist, media, colours etc. Be sure to explore all the API docs to find out what it's capable of!

![](https://i.cloudup.com/NQP7-dZyf7.png)

## Wrap up

- We know how to make requests to the Rijksmuseum API
- We know how the response data is structured
- We know that we can make multiple requests to obtain different data.