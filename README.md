# `Array.prototype.sample` Proposal

## Motivation

When using ECMAScript arrays, it is commonly desired to retrieve an element at a pseudo-random index. The prevailing pattern for this is

```
var randomElement = function(elementList) {
  var randomNumber = Math.random();
  var maxSize = elementList.length;
  var index = Math.floor(randomNumber*maxSize);
  return elementList[index];
}

randomElement(arr);
```

The prevailing pattern requires that we pass the collection to a utility method that then returns an element from the collection. Ideally, however, we want to be asking the Array itself to return an element it contains, without the mediation of a utility method.

## Proposed Solution

We propose the addition of an `Array.prototype.sample` method, such that the above pattern can be written as

```
var arr = [1, 2, 3, 4, 5, 6]
arr.sample();
// => 3
arr.sample(2);
// => [6,2]

var arr2 = [];
arr.sample();
// => nil
arr.sample(3);
// => []

```

The sample function would choose a random element, or the random `n` elements, from the array. If the array is empty, the first form returns `nil`, and the second form returns an empty array.

## Use Cases

## FAQs

### Why `sample` instead of `random`?

We rejected the term `random()` as it is used in the `Math` library already and we didn't wish to overload the term.

The term `sample()` was taken from the [Array#sample method introduced in Ruby 1.9.1 core](http://www.ruby-doc.org/core-1.9.1/Array.html#method-i-sample). We like that it is unlike any other name in the current namespace and that it makes sense with selecting both one or multiple elements from an array.

#### Acknowledgements

Thanks to Rick Waldron for his article on [designing an exponentiation operator for JavaScript](http://bocoup.com/weblog/designing-an-exponentiation-operator-for-javascript/). Also to Domenic Denicola for his [Array.prototype.contains proposal](https://github.com/domenic/Array.prototype.contains), which we used as a reference for our own.
