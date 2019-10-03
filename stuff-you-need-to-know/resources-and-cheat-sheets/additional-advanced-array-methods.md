# Additional advanced array methods

## .find()

The `find()` array method will return the `value` of the `first item` in the array provided that satisfies the condition that you are providing.

```js

const myArray = [5, 10, 15, 20, 25];

const result = myArray.find(item => {
  return item > 13;
})

result // 15
```

The key concept to remember here is that `.find()` will only return the `first` item that satisfies the statement. So even though `myArray` contains three numbers that are larger than 13, it will only return the first item that matches our criteria.

If no match is found, you will be returned a `undefined` value.

*This method is not supported in Internet Explorer.


## .some()

The `some()` array method will return a `boolean` value if at least `one item` in the provided arrays satisfies the condition you are checking for.

```js

const myArray = [5, 10, 15, 20, 25];

const result = myArray.some( item => {
  return item > 13;
})

result // true
```

If no match is found, you will be returned a `false` value.
## .includes()

The `includes()` array method will return a `boolean` value if the provided array contains a specific item.

```js

const myArray = [5, 10, 15, 20, 25];

const result = myArray.includes(20);

result // true
```

*This method is not supported in Internet Explorer.


## .reduce()

The `reduce()` array method applies a function to each item in an array to *reduce* it to return a `single` value.

Before the `reduce()` method was introduced, we could utilize the same functionality with a _for loop_:

```js
const numbers = [10, 20, 60, 10];
let numbersTotal = 0;

for (let i = 0; i < numbers.length; i++) {
  numbersTotal = numbersTotal + numbers[i];
}

numbersTotal // 100
```

So, for each number in the array, add its value to the `numbersTotal` variable so when the loop is done, we have the total of each number combined.

The `reduce()` method provides the same functionality. Once we provide an array we want to work with, we pass *two* arguments to the callback function: the total value (i.e. accumulator) and the current amount (i.e. current value). 

Here is that same example from earlier but now with the `reduce()` method:

```js
const numbers = [10, 20, 60, 10];

const total = numbers.reduce((totalValue, currentAmount) => {
	return totalValue + currentAmount;
});

total // 100
```
As the `.reduce()` method cycles through the array, the callback function is executed against the _accumulator_ and each element in the array (from left or right) to reduce it to a single value. The accumulator is the parameter on the left in the function passed to `.reduce()`. It's only used inside of the function - kind of like `i` in a `for` loop.

Here's another useful example of when we can use `.reduce()` to _flatten_ multiple arrays into one single array.

```javascript
const nums = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
const flatArray = nums.reduce((total, amount) => {
  return total.concat(amount);
});

flatArray // [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

`.reduce()` is often used in combination with other functions to solve complex problems, (e.g. to count [the number of times a string occurs in an array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce#Counting_instances_of_values_in_an_object)).



