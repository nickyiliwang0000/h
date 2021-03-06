## Weather App Code Along

### Building a Weather App: Code Along

The data that we get back has a lot of information. The data object consists of two JavaScript objects; the object of interest to us is the one named "current_observation". This object has a lot of interesting data.

The Wunderground documentation lists all of the available data. For "conditions": http://www.wunderground.com/weather/api/d/docs?d=data/conditions

For this widget we need the following data:

* `temp_c`: Temperature in celsius
* `display_location.city`
* `forecast_url`
* `observation_time_rfc822`: date and time
* `weather`: e.g. "Sunny" or "Partly Cloudy"
* `icon_url`: image representing the weather


We will combine this information to create a weather widget together. Download **[weather-app.zip](https://hychalknotes.s3.amazonaws.com/weather-app.zip)** to get started.

The HTML & CSS for the widget has been provided for you in `weather-app.html`. jQuery has been included for you as well. We will write JavaScript inside of the `weather-app.js` file.
 
For this app/widget we'll create an object called `weatherWidget` to namespace our code and organize it. The object will have several properties:

1. `init`: a function to initialize/start the widget. We'll invoke/call this function when the document loads.

2. `getWeather`: a function used to make our AJAX request.

3. `parseData`: a callback function that gets called on successful AJAX request. We'll go through the response data and put the relevant data in `weatherData`. From here we'll call `updateDOM`.

4. `updateDOM`: a function that will use jQuery to update the DOM with data from `weatherData`.

#### Reminder
We will prefix all property calls with `weatherWidget`. So `weatherWidget.parseData` instead of just `weatherWidget`.

You can view a complete working version of the app [here](https://hychalknotes.s3.amazonaws.com/weather-app-answer.zip).

#### Extension exercises:

* Create a button to update data on click
* Change the background colour based on the weather condition
* Provide an input field for state and city. Refresh the widget with the right data when the form is submitted.