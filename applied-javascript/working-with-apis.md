  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - What an API is
  - That we will be using them mostly to get data
  - To get data we will be making a GET request
  - That sometimes GET requests can be modified using a query string
  - That APIs sometimes need keys
  - That JSON is like a JavaScript object
  -->

# Working with APIs

## What is an API?
 _Application programming interface_ is a general term in computer programming; in web development specifically, we use it to refer to a set of instructions and protocols of communication that facilitate communication between a client and a server (the client can be another server but most often for us, it will be the browser).

> Think of an API as the string between two tin cans - it's the thing that makes it possible for a child in one house to hear their neighbor's plan for sneaking out at night. 

We'll mostly be using APIs to access data from sources external to our websites. Many organizations have APIs that allow their data to be used by external developers in their own websites; Twitter has an API that you call to populate a widget on your website that shows your three most recent tweets; Facebook has an API that you interact with when you hit the 'share' or 'like' button on an article from The Globe and Mail.

There are [tons and tons of public APIs](https://www.programmableweb.com/category/all/apis?data_format=21190). They differ in quality, documentation, and organization. We'll mostly be working with RESTful APIs during the bootcamp.

### What's a RESTful API?

To help make our lives as developers easier, many APIs follow a set of organizational principles called _representational state transfer_ (REST). It's **not** imperative that you understand what representational state transfer entails right now.

If you're curious, you can read up on [Wikipedia](https://en.wikipedia.org/wiki/Representational_state_transfer#Applied_to_Web_services).

## Communicating with APIs
When we work with APIs, we use _hypertext transfer protocol_ (HTTP) methods to tell the API what we want to do. HTTP is the predominant protocol of the internet, which means that when browsers and servers communicate, they use HTTP to do so. HTTP has a few standard methods built into it: `GET`, `POST`, `PUT`, and `DELETE`.

 HTTP method | what it does 
 --|--
`GET` | requests data  
`POST` | adds new data
`PUT` | updates data 
`DELETE`| removes data 


You might remember `GET` and `POST` from our work with forms:
```html
<form action="/my-form-page" method="POST">
 <!-- form fields and content -->
</form>
```

To access data from a RESTful API, we make a `GET` request to an _endpoint_. An endpoint is a URL that points to the data we want.

Try viewing these endpoints in your browser:      
* <https://myttc.ca/osgoode_station.json>  
* <https://api.datamuse.com/words?ml=computer>
* <https://api.flickr.com/services/rest/?method=flickr.photos.search&format=json&text=hackeryou&api_key=9ffc680dbb093e647be2784acdb4eb56>

### Anatomy of a GET request

Notice that some of those endpoints have a `?` in them followed by what looks like a key-value pair in the format `key=value`. Endpoints often allow additional options to be passed along with a request after the URL in what's called a _query string_. The `?` and everything after it is the query string. These additional options are called _parameters_, just like in JavaScript. Query string key-value pairs are to `GET` request URLs as parameters are to JavaScript functions.

![anatomy of an API query](https://cl.ly/image/093S2d001811/api-query.png)

Notice that `https://myttc.ca/osgoode_station.json` has no query string. This means that there is a different endpoint for each station, rather than a general endpoint that accepts parameters that define the station.

## API keys and authentication
Notice how some of our sample requests had strings of unintelligible letters and numbers in them? Those strings are unique passphrases, each called an _API key_. API keys identify us to the API owners. Many APIs use this and other forms of authentication (like [OAuth](https://oauth.net/) or a username and password) to prevent spammy requests. 

API keys usually cost only your email!
<!-- Instructors: choose whichever API is most useful to you - if you're doing a code-along soon, use that API! -->

Let's try it with the Harry Potter API:
1. Visit <https://www.potterapi.com/>.
2. Click 'Sign In / Sign Up'.
3. Add an email and password.
4. Click 'Create account'.
5. You should see your API key.

Some are more involved, like the Etsy API:
1. Visit <https://www.etsy.com/developers/documentation>
1. Click 'Register as a developer' on the left sidebar and create an account.
1. Enable two-factor authentication.
1. Choose from the list of options for your API project (you aren't required to add a real URL, but do make it the proper format: `https://www.fakeurl.com`)
   * ![Etsy API options screen](https://hychalknotes.s3.amazonaws.com/etsy-options-screen.png)
1. Copy and save the keystring and shared secret.
1. Go the documentation <https://www.etsy.com/developers/documentation/getting_started/requests> to figure out how to use your key.

## API responses

Let's take a closer look at some of the data we got back from [one of our sample API calls](https://myttc.ca/osgoode_station.json).

```js
{
  "time": 1547575046,
  "stops": [
    {
      "name": "Osgoode Station Concourse",
      "agency": "Toronto Transit Commission",
      "routes": [],
      "uri": "osgoode_station_concourse"
    },
    {
      "name": "Osgoode Station Northeast Entrance",
      "agency": "Toronto Transit Commission",
      "routes": [],
      "uri": "osgoode_station_northeast_entrance"
    },
    {
      "name": "Osgoode Station Northwest Entrance",
      "agency": "Toronto Transit Commission",
      "routes": [],
      "uri": "osgoode_station_northwest_entrance"
    },
    {
      "name": "Osgoode Station Southeast Four Seasons Entrance",
      "agency": "Toronto Transit Commission",
      "routes": [],
      "uri": "osgoode_station_southeast_four_seasons_entrance"
    },
    {
      "name": "Osgoode Station Southwest Queen Entrance",
      "agency": "Toronto Transit Commission",
      "routes": [],
      "uri": "osgoode_station_southwest_queen_entrance"
    },
    {
      "name": "Osgoode Station Southwest University Entrance",
      "agency": "Toronto Transit Commission",
      "routes": [],
      "uri": "osgoode_station_southwest_university_entrance"
    },
    {
      "name": "Osgoode Station Subway Platform",
      "agency": "Toronto Transit Commission",
      "routes": [
        {
          "name": "Yonge-University-Spadina Subway",
          "stop_times": [
            {
              "service_id": 1,
              "shape": "Yonge-University-Spadina Subway To Finch Station",
              "departure_timestamp": 1547575229,
              "departure_time": "1:00p"
            },
            {
              "service_id": 1,
              "shape": "Yonge-University-Spadina Subway To Downsview Station",
              "departure_timestamp": 1547575281,
              "departure_time": "1:01p"
            },
            {
              "service_id": 1,
              "shape": "Yonge-University-Spadina Subway To Finch Station",
              "departure_timestamp": 1547575473,
              "departure_time": "1:04p"
            },
            {
              "service_id": 1,
              "shape": "Yonge-University-Spadina Subway To Downsview Station",
              "departure_timestamp": 1547575525,
              "departure_time": "1:05p"
            },
            {
              "service_id": 1,
              "shape": "Yonge-University-Spadina Subway To Finch Station",
              "departure_timestamp": 1547575717,
              "departure_time": "1:08p"
            },
            {
              "service_id": 1,
              "shape": "Yonge-University-Spadina Subway To Downsview Station",
              "departure_timestamp": 1547575769,
              "departure_time": "1:09p"
            }
          ],
          "uri": "yonge-university-spadina_subway",
          "route_group_id": "1"
        }
      ],
      "uri": "osgoode_station_subway_platform"
    }
  ],
  "uri": "osgoode_station",
  "name": "Osgoode Station"
}
```
Curly braces, comma separated key-value pairs... Looks a lot like a JavaScript object, right? 

🎉That's because it basically is!🎉  

This is a data format called _JavaScript Object Notation_ (JSON) that is very similar to a JavaScript object. APIs can return data in many formats (you might also see the historically more popular XML). We prefer to work with JSON because we can use our knowledge of JavaScript objects to navigate JSON data. The most salient difference between JSON and a JavaScript object is that JSON can include most JavaScript data types (e.g. strings, numbers, booleans, nested arrays, nested objects) but **NOT** functions.
