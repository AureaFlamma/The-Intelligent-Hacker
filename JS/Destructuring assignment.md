# Resources
[JS Destructuring in 100 Seconds- Fireship](https://www.youtube.com/watch?v=UgEaJBz3bjY)

# Arrays

Destructuring allows us to put properties of an object in their own variables. 
```JS
const arr = ['🥓', '🍕', '🍟'];

// Old, ugly way:
const bacon = arr[0];
const pizza = arr[1];
const fries = arr[2];

//✨awesome destructuring:
const [bacon, pizza, fries] = arr; 
```
☝ *NB: no quotes around var names in square brackets*
## Omit values
We can ignore a value by skipping the property name whilst retaining the commas:
```JS
const arr = ['🥓', '🍕', '🍟'];

const [bacon,, fries] = arr;
// OR
const [,, fries] = arr;
```

## Rest property
We can destructure some variables and put rest in its own variable:
```JS
const arr = ['🥓', '🍕', '🍟'];

const [bacon, ...rest] = arr;
console.log(rest) // ['🍕', '🍟']]
```

## Fallback values
We can provide a fallback value in case the value becomes undefined
```JS
const arr = [undefined, '🍕', '🍟'];

const [bacon='🐖', pizza, fries] = arr;
```
☝ *NB: this works only for undefined, not for null or other falsy values.*

# Objects
We can destructure not only arrays, but also objects:
```JS

const obj = {
shroom: '🍄',
banana: '🍌',
pineapple: '🍍'};

//Old, ugly way:
const shroom = obj.shrrom;
const banana = obj.banana;
const pineapple = obj.pineapple;

//✨Destructuring:
const {shroom, banana, pineapple} = obj;

```

With objects, we can do all we can do with arrays, and more.
- **Omit & Rest**: If we're interested in a specific property, we can grab it directly, without having to use the Omit or Rest workarounds:
```JS
const obj = {
shroom: '🍄',
banana: '🍌',
pineapple: '🍍'};

const { shroom } = obj;
```

- **Fallback values**
```JS
const obj = {
shroom: undefined,
banana: '🍌',
pineapple: '🍍'};

const { shroom='🌌', banana, pineapple} = obj;
console.log(shroom) //🌌
```

We can also do things we can't do with arrays:
## Renames
```JS
const obj = {
shroom: '🍄',
banana: '🍌',
pineapple: '🍍'};

const { shroom: mushroom, banana, pineapple} = obj;
```

## Nested destructuring
```JS
const obj = {
	parent: {
		child: '👶'
	},
}

const {parent: { child } } = obj;
console.log(child) // 👶
```
☝ *For more complex example, see below in [Complex destructuring](Destructuring%20assignment.md#Complex%20destructuring)*

## Loops
Object destructuring can be used in for-of loops
```JS
const users = [
	{ id: 1 },
	{ id: 2 },
	{ id: 3 }
]

for (const { id } of users) {
	console.log(id);
} 
// Output:
// 1
// 2
// 3

users.forEach(( { id } ) => { console.log(id) })
// Output:
// 1
// 2
// 3

//BUT:
users.forEach(( id ) => { console.log(id) })
//Output:
// { 'id': 1 }
// { 'id': 2 }
// { 'id': 3 }
```


## Destructuring props
```JS
const user = { id: 0, username: 'philip'};

function haveFun({ id, username }) {
	console.log(`hi ${username}`)
};

haveFun(user); //hi philip
```
☝ *This is how props are passed in React*

# Bonus

## Complex destructuring
```JS
const arr = [
 {parent: {
   child: '👶'
 }}, 
 [1, 2, 3],
  {alphabet: ['a', 'b', 'c']},
 '🍕', 
 '🍟'
];

const [{ parent: { child } }, [one, two, three], {alphabet: [firstLetter, secondLetter, thirdLetter]},  pizza, fries] = arr;

console.log(child); //'👶'
console.log(fries); //'🍟'
console.log(one); // 1
console.log(firstLetter) // 'a'
```

## Swapping variables
We can use destructuring assignment to swap variables without having to copy them over into a temporary variable. 
```JS
let a = 1;
let b = 3;

// Old. shitty way:
let temp;
temp = a;
a = b;
b = temp;

//✨ New, dope way:
[a, b] = [b, a];

console.log(a); // 3
console.log(b); // 1
```

We can also swap around items in an array:
```JS
const arr = [1, 2, 3];
[arr[2], arr[1]] = [arr[1], arr[2]];
console.log(arr); // [1, 3, 2]
```
☝ *Nothing similar will work for objects. You'll need to do the temp var trick*