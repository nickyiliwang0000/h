  <!-- Student takeaway -->
  <!-- By the end of this lesson, the student should know:
  - What a regular expression is.
  - When to use a regular expression.
  - Some common methods that take regular expressions (e.g. exec and replace).
  - How to build a regex.
  - Where to check or find a regex.
  - There are a plenty of common regex snippets out in the world.
  -->

# Regular expressions

_Regular expressions_ are sequences of characters that define search patterns. They're mostly used to check for specific combinations of characters in a string.

One common use case for regex is form validation: we could use a regular expression to check if what a user typed into an input has a valid email like `[name][@][domain][.][tld]`. We could alert the user of any misspellings or errors that would make the email address unusuable (e.g. `pilarsantiagojmail.ca`,  `pilarsantiago@jmailca` or  `@jmail.ca`).

> Regular expressions are used in lots of programming languages, not just in JavaScript.

## Regex syntax
The syntax for a regex is `/` , then the pattern you want to match, then a closing `/`.

```js
let re = /abc/;
```
This regular expression would match the characters "abc" in that order.

You can also create a new regular expression using the `new` keyword.
```js
let regEx = new RegExp();
```
> From MDN: `Use the constructor function when you know the regular expression pattern will be changing, or you don't know the pattern and are getting it from another source, such as user input.`

For the most part, we'll be using the first syntax.

## Checking for a match with `exec`

To check to see if a regex pattern has any matches in a string, we can use the `exec` method. It returns either an array of the matches or `null` if it doesn't find anything. 

```js
let re = /abc/;
re.exec("I'm learning the alphabet."); //returns null
re.exec("Now I know my abc's"); //returns "["abc"]";
```

## Replacing parts of a string with `replace`

You can also pass a regular expression to the `replace` string method to replace a chosen character(s) with other one(s).  

```js
let name = "HackerYou";
let newName = name.replace(/You/, "U"); //returns "HackerU"
```

Regular expressions don't have to search for just one thing - you can use them to catch multiple things at once!

### More complicated regular expressions
We can tell our replace function that we want to search for both upper and lower case Y's by matching a set of characters instead of just capital Y. We use `[]` to indicate a set of characters.

```js
let name="HackerYou";
let newName = name.replace(/[Yy]ou/, "U");
// newName
// "HackerU"
```

You can also use what are called _flags_ to change the way the search behaves.  Adding the `i` flag to the end of a regex means the search will be **case insensitive**.

```js
let name="hackeryOu";
let newName = name.replace(/You/i, "U"); 
// newName
// "hackerU"
```

There are lots of other diacritics available to you to narrow down what your regular expression is looking for:

symbol | meaning in a regex
--|-- 
`^` |starting at the beginning of a string
`[]`| a set of characters 
`*` | match multiples
`.` | match any character except line breaks
`\w` | match all words 
`\W` | match all non-words
`\d` | match any digit   
`\s` | match any whitespace character  
`[a-z]` | match a range of characters (in this case, a to z)
`[^cd]` | match characters NOT in the set (in this case, )
`$/` |denotes the end of the string

## Regex patterns

If you want to do something commong using regex, chances are someone's already written that regex.

### Matching a username that has a length between 3 and 16 characters
```js
let username316 = /^[a-z0-9_-]{3,16}$/;
```

Let's break down what's happening here:
1. `^` means: find the beginning of a string...
2. `[a-z0-9_-]`...that is followed by any lowercase letter `(a-z)`, number `(0-9)`, underscore`(_)` or a hyphen `(-)`.
3. Make sure that there are at least 3 characters `{3,16}` , but no more than 16.
4. `$/` means "this is the end of the string."

### Matching an email address

```js
let emailRegExp = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;
```

Let's break down what's happening here:
1. `^` means: find the beginning of a string...
2. `([a-z0-9_\.-]+)`: ...that is followed by one or more (`+`) lowercase letters (`a-z`), numbers (`0-9`), underscores (`_`), dots (`\.`), or hyphens (`-`).
	* Notice that `.` is escaped using the `\` character.
3. Then, find exactly this character `@` followed by a string...
4. `([\da-z\.-]+)` ... that **must** be `\d` followed by one or more (`+`) lowercase letters (`a-z`), dots (`\.`), or hyphens (`-`).
	* Email providers are usually one word.
5. Then, find a string`([a-z\.]{2,6})` between 2 to 6 letters (`{2,6}`) or dots (`\.`).
	* Consider TLDs like `co.uk`, `gc.ca`, `.ca`, and `.pizza`.
6. End of the string (`$/`).

## Writing your own regular expressions

There are lots more patterns and flags, and you'll probably never remember them all, so don't be afraid to:

1. Search for the regex online.
	* If you're looking for something common like email address validation, you can usually find a [pre-written regex](https://code.tutsplus.com/tutorials/8-regular-expressions-you-should-know--net-6149) online.
2. Use a regex tester.
	* Like <http://www.regexr.com/>! On this one, the sidebar contains a reference to all the different symbols and flags available and some common examples to get you started.
3. Practice.
	* There are lots of ways to practice!
		* Testing your regex on <http://www.regexr.com/>
		* [Regexone](http://regexone.com/) is a great source for learning regex via interactive exercises.