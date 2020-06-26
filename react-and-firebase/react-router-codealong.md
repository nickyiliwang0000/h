# React-Router code-along

Using Create React App, React-Router, and [The Movie Database API](https://developers.themoviedb.org/3/getting-started/introduction), we're going to build an application that is going to look similar to Netflix.

This app will allow us to see a catalogue of popular movies from a given year. It's also going to allow us to click on each individual movie in our catalogue and go to a separate view that shows more information about that movie.

To get started, we will create a new `create-react-app` project and call it `Hackflix`.

```bash
npx create-react-app hackflix
```

You can find the pre-written styles for this code along [HERE](https://hychalknotes.s3.amazonaws.com/movie-db-codealong.zip). This CSS can replace the default styles that exist within the `index.css` file in our new `Hackflix` project.

Let's clear out some of the boilerplate `jsx` from the default `App.js`, and add some custom header markup to our `App` component:

```jsx
// App.js
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header>
          <h1>Hackflix</h1>
        </header>
      </div>
    );
  }
}

export default App;
```

Perfect. Now that we have our header, let's grab the initial data we need from the movie database API. To start out, we're going to want to grab a list of all the popular movies from 1990 (or any year you prefer) so we can display them on the page. We're going to need to install `axios` as a dependency to our application and import it. Then, we can make our initial request for the data inside of the `componentDidMount` lifecycle method. 

We then store the result of that API call inside of a state value called `movies`. Before we can do that we first need to create the state value in the constructor with a default value of an empty list so that our component can render even when we don't yet have any movies from our API.

```jsx
// App.js
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  constructor(){
    super();
    this.state = {
      movies: [],
    }
  }

  componentDidMount() {
    // After the component has been added to the DOM make our API call...
    axios({
      url: 'https://api.themoviedb.org/3/discover/movie',
      params: {
        api_key: 'f012df5d63927931e82fe659a8aaa3ac',
        language: 'en-US',
        sort_by: 'popularity.desc',
        include_adult: 'false',
        include_video: 'false',
        page: 1,
        primary_release_year: 1999,
      },
    }).then(res => {
      res = res.data.results;
      // Store the API results to the "movies" state value...
      this.setState({
        movies: res,
      })
    })
  }

  render() {
    return (
      <div className="App">
        <header>
          <h1>Hackflix</h1>
        </header>
      </div>
    );
  }
}

export default App;

```

Awesome! We should now be retrieving our movies from the movie DB and storing them inside of our state. Now let's display them on the page! Inside of our App component `render` method, let's add the following code after the `<header>` element:

```jsx
<div className="catalogue">
  {this.state.movies.map (movie => {
    return (
      <div key={movie.id} className="movie">
        <img src={`http://image.tmdb.org/t/p/w500/${movie.poster_path}`}/>
      </div>
    );
  })}
</div>
```

And now we have movies displayed on the page! But what if we wanted to use this Catalogue elsewhere in our app? Let's make this more reusable by breaking it out into a separate component. 

Since this new component will be responsible for getting the data and storing it in state for later use, we will make this a stateful component and move our `axios` call into this component as well.

```jsx
// Catalogue.js
import React, { Component } from 'react';
import axios from 'axios';

class Catalogue extends Component {
    constructor(){
    super();
    this.state = {
      movies: [],
    }
  }

  componentDidMount() {
    axios({
      url: 'https://api.themoviedb.org/3/discover/movie',
      params: {
        api_key: 'f012df5d63927931e82fe659a8aaa3ac',
        language: 'en-US',
        sort_by: 'popularity.desc',
        include_adult: 'false',
        include_video: 'false',
        page: 1,
        primary_release_year: 1999,
      },
    }).then(res => {
      res = res.data.results;
      this.setState({
        movies: res,
      })
    })
  }
  render() {
    return (
      <div className="catalogue">
        {this.state.movies.map((movie) => {
          return (
            <div key={movie.id} className="movie">
              <img src={`http://image.tmdb.org/t/p/w500/${movie.poster_path}`}
              />
            </div>
          );
        })}
      </div>
    );
  }
}

export default Catalogue;
```

And then inside of our App component, we can refactor like so:

```jsx
import React, { Component } from 'react';
import Catalogue from './Catalogue';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header>
          <h1>Hackflix</h1>
        </header>
        <Catalogue />
      </div>
    );
  }
}

export default App;

```

Now have a `Catalogue` component that gets our data and displays all of our movies! 🎬 

This is cool and all, but what if we want to create the ability to click on a movie and be transported to a page that has additional information about that movie? We can do this with routing. Let's start by installing `react-router-dom` as a dependency and importing it into our `App` component. Then we will start refactoring our `render` method a little so that it can start to use routing:

```jsx
// App.js
import React, { Component } from 'react';
import Catalogue from './Catalogue';
import { BrowserRouter as Router, Route } from 'react-router-dom';

class App extends Component {
  render() {
    return (
      <Router>
        <div className="App">
          <header>
            <h1>Hackflix</h1>
          </header>
          <Route exact path="/" component={Catalogue} />  
        </div>
      </Router>
    );
  }
}

export default App;
```

Now let's add our second route, which is going to be `/movie/:movie_id`, where `movie_id` is a parameter: the id of the movie we'd like to request from the movie database.

```jsx
// App.js
import React, { Component } from 'react';
import Catalogue from './Catalogue';
import { BrowserRouter as Router, Route } from 'react-router-dom';
import MovieDetails from './MovieDetails';

class App extends Component {
  render() {
    return (
      <Router>
        <div className="App">
          <header>
            <h1>Hackflix</h1>
          </header>
          <Route exact path="/" component={Catalogue} />  
          <Route exact path="/movie/:movieID" component={MovieDetails} />
        </div>
      </Router>
    );
  }
}

export default App;

```

Now let's create a `MovieDetails` component that will grab our a movie by the ID parameter that gets passed when we navigate to that route:

```jsx 
// MovieDetails.js
import React, { Component } from 'react';

class MovieDetails extends Component {
  render() {
    return <h1>{this.props.match.params.movieID}</h1>;
  }
}

export default MovieDetails;
```

You'll see that whatever number we pass after `/movie` in the URL, that number gets printed out on to the page! We can use this number to make another `axios` request to the API for more data on that particular movie like this:

```jsx
// MovieDetails.js
import React, { Component } from 'react';
import axios from 'axios';

class MovieDetails extends Component {
  constructor() {
    super();
    this.state = {
      movie: {},
    };
  }

  componentDidMount() {
    axios({
      url: `https://api.themoviedb.org/3/movie/${this.props.match.params.movieID}`,
      params: {
        api_key: 'f012df5d63927931e82fe659a8aaa3ac',
        language: 'en-US',
        sort_by: 'popularity.desc',
        include_adult: 'false',
        include_video: 'false',
        page: '1',
        primary_release_year: '2018',
      },
    }).then(res => {
      this.setState({
        movie: res.data,
      })
    })
  }

  render() {
    return <h1>{this.props.match.params.movieID}</h1>;
  }
}

export default MovieDetails;

```

Here we are hitting the `/3/movie` endpoint of the MovieDB API and passing in `this.props.params.movieID` as the unique movie ID we'd like to grab. We store the results in our state in a property called `movie`.

Now that we have access to our `movie` property, we can start displaying its data on to the page! Inside the render method in `MovieDetails` let's add:

```jsx
// MovieDetails.js
render() {
  return (
    <div>
      <div className="poster">
        <div className="description">
          <h1>{this.state.movie.original_title}</h1>
          <h2>{this.state.movie.tagline}</h2>
          <p>{this.state.movie.overview}</p>
        </div>
        <div className="image">
          <img src={`http://image.tmdb.org/t/p/w500/${this.state.movie.poster_path}`} alt=""/>
        </div>
      </div>
    </div>
  );
}
```

We're almost wrapped up, there's just one more key step: we need to make it so that you when you click a movie in Catalogue, it brings you to the `MovieDetails` view. In order to do this, we'll need access to the ID of the movie inside of our `Catalogue` component. We already have access to this because we're making an API call inside our `Catalogue` component and our response contains a unique `id` property.

Inside our `Catalogue` component, let's use React-Router's `Link` component to create a link to our movie details URL.

```jsx
// Catalogue.js
import React, { Component } from 'react';
import axios from 'axios';

// import a Link component
import { Link } from 'react-router-dom';

class Catalogue extends Component {
    constructor(){
    super();
    this.state = {
      movies: [],
    }
  }

  componentDidMount() {
    axios({
      url: 'https://api.themoviedb.org/3/discover/movie',
      params: {
        api_key: 'f012df5d63927931e82fe659a8aaa3ac',
        language: 'en-US',
        sort_by: 'popularity.desc',
        include_adult: 'false',
        include_video: 'false',
        page: 1,
        primary_release_year: 1999,
      },
    }).then(res => {
      res = res.data.results;
      this.setState({
        movies: res,
      })
    })
  }
  render() {
    return (
      <div className="catalogue">
        {this.state.movies.map((movie) => {
          return (
            <div key={movie.id} className="movie">

              {
              // wrap the Link component around each Catalogue image and 
              // set the "to" attribute to our route's URL path with movie ID stored in our API data 
              }
              <Link to={`/movie/${movie.id}`}>
                <img src={`http://image.tmdb.org/t/p/w500/${movie.poster_path}`} alt={`Movie poster for ${movie.original_title}`}>
              </Link>
            </div>
          );
        })}
      </div>
    );
  }
}

export default Catalogue;
```

And that's all there is to it! 
