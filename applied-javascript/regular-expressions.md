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

A _regular expression_, or _regex_, is a sequence of characters that defines a search pattern. They're often used to 
check for specific combinations of characters in a string.

One common use case for regexes is form validation: we could use a regular expression to check if what a user typed into
an input has a valid email like `[name][@][domain][.][tld]`. We could alert the user of any misspellings or errors that
would make the email address unusuable (e.g. `pilarsantiagojmail.ca`,  `pilarsantiago@jmailca` or  `@jmail.ca`).

> Regular expressions are used in lots of programming languages, not just in JavaScript.

## Regex syntax
In JavaScript, regexes can be created in two different ways. The most common way is to use a _regular expression 
literal_, which starts with a `/` character, then the pattern you want to match, then a closing `/`.

```js
let re = /abc/;
```
This regular expression would match the characters "abc" in that order.

You can also create a new regular expression using the `new` keyword.
```js
let regEx = new RegExp("abc");
```
> From MDN: `Use the constructor function when you know the regular expression pattern will be changing, or you don't know the pattern and are getting it from another source, such as user input.`

Both of these methods create a regular expression object with methods for various features. For the most part, we'll be 
using the first syntax.

## Testing a string with a regular expression.

To check if a string matches a regular expression we can use the regex's `test` method which takes a string as an 
argument and returns `true` if it matches the pattern, and `false` if it does not.

```js
const doubleOPattern = /oo/
console.log(doubleOPattern.test("boom"));
// true
console.log(doubleOPattern.test("dug"));
// false
``` 

## Checking for a match with `exec`

Often we need more information than simply if a string matches an expression or not. In these cases we can use the 
the `exec` method. When passed an string, it returns a result array if the pattern matched, and `null` if the match 
failed. 

```js
let re = /abc/;
re.exec("I'm learning the alphabet."); //returns null
re.exec("Now I know my abc's"); //returns "["abc"]";
```

## Using regex with string methods

Some `String` methods which normally take string arguments will also accept a regular expression as an argument. For 
example the `replace` method can use either a string or a regex for it's first argument.     

```js
let name = "HackerYou";
let wrongName = name.replace('You', "U"); // "HackerU"
let alsoWrongName = name.replace(/You/, "U"); // also "HackerU"
```

## More complex regular expressions

Why would you use a regular expression instead of a string? Until now we've only created some very simple regular 
expressions. By using _special characters_ in our patterns we can create much more complex expressions. For example, the 
special characters`[` and `]` let us define a set of characters to match in that position of the string.

```js
let website = "hackeryou.com";
let hyPattern = /[Hh]acker[Yy]ou/;
console.log(hyPattern.exec(website))
// Array ["hackeryou"]
```

### Flags

We can also modify the behaviour of regular expression matching by using _flags_ to modify the expression. For example, 
to match a pattern everywhere it is found in the string, add the _global search_ flag, `g`, at the and of the regular
expression literal, after the closing `/`.

```js
let statement ="Apples are the best fruit. You should eat an apple every day.";
console.log(statement.replace(/[Aa]pple/g, "orange")); 
// "oranges are the best fruit. You should eat an orange every day."
```  

Another common flag is the _case insensitive_ flag, `i`. This flag will allow the regular expression to match strings
even if the characters in the string are different case (uppercase or lowercase) than in the pattern.

You can also specify multiple flags at the same time. 

```js
let petOpinion = "Cats make the best pets. Everyone should own a cat.";
console.log(petOpinion.replace(/cat/ig, 'frog')); 
// "frogs make the best pets. Everyone should own a frog."
``` 

## Advanced regular expressions  

There are lots of other special characters available to you to narrow down what your regular expression is looking for:

symbol | meaning in a regex | example
--|--|-- 
`^` | The start of a string | `/^apples/` matches `"apples are great"`, but not `"the best fruit is apples"` 
`.` |  Any character except line breaks | `/cat./` matches the word "cat" followed by any character.
`[xyz]`| Any character from the specified set (in this case either x, y, or z) | `/bread[sy]/` matches both `"breads"` and `"bready"`, but not `"bread"`.
`[a-z]` | Any character from a the specified range of characters (in this case any letter from a to z) | `/pear[a-z]/` matches `"pear"` followed by any lowercase letter between `a` and `z`.
`[^cd]` | Any character *not* in the specified set (in this case any character that's not c or d) | `/[^1a]23/` matches the number 23 preceded by any character other than a `1` or an `a`.
`\w` | Any _word character_. i.e. a-z, A-Z, 0-9, and \_. Equivalent to [a-zA-Z0-9_]. | `/\w\w.` matches any two letters, numbers, or underscores. 
`\W` | Any non-_word character_ i.e. any character other than a-z, A-Z, 0-9, and \_. Equivalent to [^a-zA-Z0-9\_] | `/bird\W/` matches an "bird" followed by any non-alphabet, numeral, or underscore character.
`\d` | Any digit. Equivalent to [0-9]. | `/\d friends/` matches the numbers 0-9 followed by " friends".    
`\s` | Any _whitespace_ character (i.e. spaces, tabs, and others) | `/cats\sdogs/` matches "cats" and "dogs" separated by a space or tab.
`*` | 0 or more of the preceding character or group | `/hearts*/` matches `"heart"`, `"hearts"`, `"heartssss"`, and so on.
`+` | 1 or more of the preceding character or group | `/brains+/` matches `"brains"`, `"brainssss"`, and so on, but _not_ `"brain"`. 
`(expression)` | group an expression | `/my friend (\w+)/` matches `"my friend "` followed by 1 or more word characters.
(expressionA\|expressionB) | match *either* _expressionA_ *OR* _expressionB_ | `/(soccer\|base)ball/` matches `"soccerball"` or `"baseball"`
`{n}` | Where `n` is an integer, match exactly `n` of the preceding expression | `/go{3}al/` only matches `"goooal"` <br> `/a(ha){3}/` only matches "ahahaha".
`{n,m}` | Where `n` and `m` are integers, match between `n` and `m` sets of the preceding expression | `hello{1,3}` matches only `"hello"`, `"helloo"`, and `"hellooo"`.
`\` | Ignore the following character's special meaning. | `/1\.9/` matches exactly `1.9`.
`$` | The end of a string | `/last$/` matches only strings ending with the `"last"`. e.g. `"last"`, and `"blast"`, but not `"plaster"`.

## Regex patterns

If you want to do something common using regex, chances are someone's already written that regex.

### Matching a username that has a length between 3 and 16 characters
```js
let username316 = /^[a-z0-9_-]{3,16}$/;
```

Let's break down what's happening here:
1. `^` means: valid strings must start with...
2. `[a-z0-9_-]`...any lowercase letter (`a-z`), number (`0-9)`), underscore (`_`) or a hyphen (`-`).
3. Make sure that there are at least 3 characters `{3,16}` , but no more than 16.
4. `$` means "this is the end of the string."

### Matching an email address

```js
let emailRegExp = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/;
```

Let's break down what's happening here:
1. `^` means: valid strings must start with...
2. `([a-z0-9_.-]+)`: ...one or more (`+`) lowercase letters (`a-z`), numbers (`0-9`), underscores (`_`), dots (`\.`), or hyphens (`-`).
3. Then, an `@` character. Followed by...
4. `([\da-z.-]+)` ... one or more (`+`) digits (`\d`), lowercase letters (`a-z`), dots (`\.`), or hyphens (`-`).
	* Email providers are usually one word.
3. Then, a `.` character. Followed by...
	* Notice that `.` is escaped using the `\` character.
5. `([a-z.]{2,6})` ... between 2 to 6 (`{2,6}`) letters or dots (`\.`).
	* Consider TLDs like `co.uk`, `gc.ca`, `.ca`, and `.pizza`.
6. And finally the end of the string (`$`). i.e. no other characters at the end.

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
