## Js tutorial Map

# Map

The **`Map`** object holds key-value pairs and remembers the original insertion order of the keys. Any value (both objects and [primitive values](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)) may be used as either a key or a value.

```js
const map1 = new Map();

map1.set('a', 1);
map1.set('b', 2);
map1.set('c', 3);

console.log(map1.get('a'));
// expected output: 1

map1.set('a', 97);

console.log(map1.get('a'));
// expected output: 97

console.log(map1.size);
// expected output: 3

map1.delete('b');

console.log(map1.size);
// expected output: 2

```

# Map.prototype.entries()

The **`entries()`** method returns a new **[Iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)** object that contains the `[key, value]` pairs for each element in the `Map` object in insertion order. In this particular case, this iterator object is also an iterable, so the for-of loop can be used. When the protocol `[Symbol.iterator]` is used, it returns a function that, when invoked, returns this iterator itself.

```js
const map1 = new Map();

map1.set('0', 'foo');
map1.set(1, 'bar');

const iterator1 = map1.entries();

console.log(iterator1.next().value);
// expected output: ["0", "foo"]

console.log(iterator1.next().value);
// expected output: [1, "bar"]

```

# Map.prototype.values()

The **`values()`** method returns a new **[Iterator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators)** object that contains the values for each element in the `Map` object in insertion order.

```js
const map1 = new Map();

map1.set('0', 'foo');
map1.set(1, 'bar');

const iterator1 = map1.values();

console.log(iterator1.next().value);
// expected output: "foo"

console.log(iterator1.next().value);
// expected output: "bar"

```

# Map.prototype.clear()

The **`clear()`** method removes all elements from a `Map` object.

```js
const map1 = new Map();

map1.set('bar', 'baz');
map1.set(1, 'foo');

console.log(map1.size);
// expected output: 2

map1.clear();

console.log(map1.size);
// expected output: 0

```

