# React-Router code-along

Using Create-React-App, React-Router, and [The Movie Database API](https://developers.themoviedb.org/3/getting-started/introduction), we're going to build an application that is going to look similar to Netflix.

This app will allow us to see a catalogue of popular movies from a given year. It's also going to allow us to click on each individual movie in our catalogue and go to a separate view that shows more information about that movie.

You can find the pre-written styles for this code along [HERE](https://hychalknotes.s3.amazonaws.com/movie-db-codealong.zip). This CSS can replace the default styles that exist within the `index.css` file in `create-react-app`.

Inside of the `App.js` file let's add a header to our `App` component - it should look something like this:

```jsx
// App.js
import React, { Component } from 'react';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header>
          <h1>Hackflix</h1>
          <nav>
            <a href="#">Catalogue</a>
          </nav>
        </header>
      </div>
    );
  }
}

export default App;
```

Perfect. Now that we have our header, let's grab the initial data we need from the movie database API. To start out, we're going to want to grab a list of all the popular movies from 1990 (or any year you prefer) so we can display them on the page. We're going to need to install `axios` as a dependency to our application and import it. Then, we can make our initial request for the data inside of the `componentDidMount` lifecycle method. 

We then store the result of that API call inside of a state item called `movies`. We'll also need to create some **default** state so that our component can render when we don't have any movies from our API yet.

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

Awesome! We should now be retrieving our movies from the movie DB and storing them inside of our state. Now let's display them on the page! Inside of our App component `render` method, let's add the following code after the `<header>`:

```jsx
<div className="catalogue">
  {this.state.movies.map (movie => {
    return (
      <div key={movie.id} className="movie">
        <img
          src={`http://image.tmdb.org/t/p/w500/${movie.poster_path}`}
          alt="test"
        />
      </div>
    );
  })}
</div>
```

And now we have movies displayed on the page! But what if we wanted to use this catalogue elsewhere in our app? Let's make this more reusable by breaking it out into a different component. 

Since this new component will be responsible for getting the data and storing it in state for later use, we will make this a complex component and move our `axios` call into this component as well.

```javascript
//Catalogue.js
class Catalogue extends Component {
	constructor() {
		super();
		this.state = {
			movies: []
		}
	}
	// ...
	componentDidMount() {
        axios({
            url: 'https://api.themoviedb.org/3/discover/movie',
            params: {
                api_key: 'f012df5d63927931e82fe659a8aaa3ac',
                language: 'en-US',
                sort_by: 'popularity.desc',
                include_adult: 'false',
                include_video: 'false',
                page: '1',
                primary_release_year: '2018'
            }
        })
        .then((res) => {
            this.setState({
                movies: res.data.results
            });
        });
    }
}
```

And then inside of our App component, we can refactor like so:
```javascript
class App extends Component {
	// ...
	render() {
		return (
			<div>
				<header className='top-header'>
					<h1>HackFlix</h1>
					<nav>
						<a href="#">Catalogue</a>
					</nav>					
				</header>
				<Catalogue />
			</div>
		)
	}
}
```

And we now have a `Catalogue` component that gets our data and displays all of our movies! 

Now this is cool and all, but what if we want to create the ability to click on a movie and be transported to a page that has additional information about that movie? We can do this with routing. Let's start by importing our `react-router-dom` package, and refactoring our render method a little bit so that it can start to use routing:

```javascript
//App.js
import { 
	BrowserRouter as Router, 
	Route } from 'react-router-dom';
```

```javascript
//App.js
class App extends Component {
	render() {
		return (
			<Router>
				<div>
					<header className='top-header'>
						<h1>HackFlix</h1>
						<Link to="/">Catalogue</Link>
					</header>
					<Catalogue />
					<Route exact path="/" component={Catalogue} />
				</div>
			</Router>
		)
	}
}
```

Now let's add our second route, which is going to be `/movie/:movie_id`, where `movie_id` is a parameter: the id of the movie we'd like to request from the movie database.

```javascript
//App.js
class App extends Component {
	render() {
		return (
			<Router>
				<div>
					<header className='top-header'>
						<h1>HackFlix</h1>
						<Link to="/">Catalogue</Link>
					</header>
					<Catalogue />
					<Route exact path="/" component={Catalogue} />
					<Route exact path="/movie/:movie_id" component={MovieDetails} />
				</div>
			</Router>
		)
	}
}
```

Now let's create a `MovieDetails` component that will grab our a movie by the ID parameter that gets passed when we navigate to that route:

```javascript
//MovieDetails.js
class MovieDetails extends Component {
	render() {
		return (
			<h1>
				{this.props.match.params.movie_id}
			</h1>
		)
	}
}
```

You'll see that whatever number we pass after `/movie` in the URL, that number gets printed out on to the page! We can use this number to make another `axois` request to the API for more data on that particular movie like this:

```javascript
//MovieDetails.js
class MovieDetails extends Component {
	constructor() {
		super();
		this.state = {
			movie: {}
		}
	}
	render() {
		return (
			<div>
				{this.props.params.movie_id}
			</div>
        )
	}

    componentDidMount() {
        axios({
            url: `https://api.themoviedb.org/3/movie/${this.props.match.params.movie_id}`,
            params: {
                api_key: 'f012df5d63927931e82fe659a8aaa3ac',
                language: 'en-US',
                sort_by: 'popularity.desc',
                include_adult: 'false',
                include_video: 'false',
                page: '1',
                primary_release_year: '2018'
            }
        })
        .then((res) => {
            this.setState({
                movie: res.data
            });
        });
    }
```

Here we are hitting the `/3/movie` endpoint of the MovieDB and passing in `this.props.params.movie_id` as the unique movie ID we'd like to grab. We store the results in our state in a property called `movie`.

Now that we have access to our `movie` property, we can start displaying it's data on to the page! Inside the render method in `MovieDetails` let's add:

```javascript
//MovieDetails.js
render() {
	return (<div>
		<div className='movie-single__poster'>
			<div className='movie-single__description'>
				<header>
					<h1>{this.state.movie.original_title}</h1>
					<h2>{this.state.movie.tagline}</h2>
					<p>{this.state.movie.overview}</p>
				</header>
			</div>
			<div className='movie-single__image'>
				<img src={`http://image.tmdb.org/t/p/w500/${this.state.movie.poster_path}`} />
			</div>
		</div>
	</div>)
}
```

We're almost wrapped up, there's just one more key step: we need to make it so that you when you click a movie on our home page, it brings you to the `MovieDetails` view. In order to do this, we'll need access to the ID of the movie inside of our `Catalogue` component. We already have access to this because we're making an API call inside our `Catalogue component.

Inside our `Catalogue` component, let's add:

```javascript
//Catalogue.js
class Catalogue extends Component {
	constructor() {
		super();
		this.state = {
			movies: []
		}
	}
	// ...
    componentDidMount() {
        axios({
            url: 'https://api.themoviedb.org/3/discover/movie',
            params: {
                api_key: 'f012df5d63927931e82fe659a8aaa3ac',
                language: 'en-US',
                sort_by: 'popularity.desc',
                include_adult: 'false',
                include_video: 'false',
                page: '1',
                primary_release_year: '2018'
            }
        })
        .then((res) => {
            this.setState({
                movies: res.data.results
            });
        });
    }
	render() {
		return (
            <div className='movie-catalogue'>
                {this.state.movies.map((movie, i) => {
                    return (
                        <div key={movie.id} className='movie-catalogue__movie'>
                            <Link to={`/movie/${movie.id}`}>
                                <img src={`http://image.tmdb.org/t/p/w500/${movie.poster_path}`} />
                            </Link>
                        </div>
                    )
                })}
		    </div>
        )
	}
}
```

And that's all there is to it! 
