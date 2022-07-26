# Primeget (WIP)
## Generates prime numbers algorithmically

Primeget is a prime number generator combined with a prime checking method to discard non-primes. It is capable of generating primes from a given range.

Generating the primes in `n = 9_000_000_000_000_000` to `z = 9_000_000_000_001_000` takes approximately ~29s.

A range between `n` and `n + 1000` seems to be the sweet spot without crashing V8.

## Usage
```js
import primeget from 'primeget'

let primes = primeget(0, 10) // [ 2,  3,  5, 7, 11, 13, 17 ]

// Interesting things happen here. Anything above `n = 97` returns nothing, but `n <= 97` is notable.
primes = primeget(97, 0)
/*
[ 97 ]
*/

primes = primeget(10, 0)
let set = [...new Set(primes)].sort((a, b) => a - b)
/*
[
    3,   5,   7,  11,  13,  17,  19,  23,  29,  31,  37,  41,
   43,  47,  53,  59,  61,  67,  71,  73,  79,  83,  89,  97,
  101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157,
  163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227,
  229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283,
  293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367,
  373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439,
  443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509,
  521, 523, 541, 547,
  ... 229 more items
]
*/
```

### Example
```js
import Primeget from 'primeget'

let n = 9_006_999_999_998_000
let z = 9_006_999_999_999_000

console.time('Time')
let primes = primeget(n, z)
console.timeEnd('Time') // About 10 seconds

// remove duplicates and sort
primes = [...new Set(primes)].sort((a, b) => a - b)

console.log(primes)
console.log('Last:', primes.slice(-1)[0])
console.log('Total:', primes.length)
```

## API
My goal was to create a simple API for this sheep counting prime number generator. It should be quite flexible. The CLI I built is an example of how it can be extended. Submit an [issue](https://github.com/draeder/Primeget/issues) if it doesn't meet your needs.

### API Usage
```js
import Primeget from '../api.js'
import { check } from '../primeget.js'

let primeget = new Primeget()

let isPrime = check(101) // true
```

### `check(n)`
Check if `n` is prime

Returns `true` if prime, `false` if not prime

### `primeget.make(n, z)`
Generate a set of prime numbers starting wih `n` until `z`.

This is an O(n) function and may crash things if the range is too great. **I am not a mathematician, so O(n) may be wrong; please correct me!**

### `primeget.get()`
Return a sorted and filtered array of primes generated by `primeget.make(n, z)`

### `primeget.raw()`
Return the raw numbers calculated by Primeget before sorting and filtering

### `primeget.length`
Return the length of the sorted and filtered array of primes generated by `primeget.make(n, z)`

## CLI
A simple CLi with some basic features.

### CLI install
```
npm i primeget -g
```
### CLI Usage
```js
> primeget // initiates Primeget cli

// generate some primes
primeget > make 0 100

// print the array of primes
primeget > get

// print the length of array of primes
primeget > get -l

// print prime at the provided index
primeget > get 187

// print a random element from the array of primes
primeget > get -r

// print array of primes between 30 and 40
primeget > get 30 40

// print array of primes between 30 and 40
// along with length of the array of primes between 30 and 40
primeget > get 30 40 -l

// another way to print the length of the current set of primes
primeget > length

// print if a number is prime (not depedant on the Primeget generated primess)
primeget > check 111 // false

// quit Primeget
primeget > 'quit' or 'exit' or 'bye' or 'close' or 'end' or 'ctrl+c'
```

## About
> I'm not a mathemetician. But I can count sheep.

Nearly 20 years ago, I had a bout of insomnia. Instead of counting sheep that night, I calculated prime numbers starting with `0 + 1 != prime`, then `1 + 1 = prime`, then `1 + 2 = prime`, and so-on, along with some subtraction between the previous two primes. I realized the system I devised worked with larger numbers, too.

I didn't know how to program very well at the time, so my attempt to test the pseudocode I wrote down was a failure. For the record, I slept very little that night. 

I have since lost that pseudocode and forgot the details, but suddenly recalled parts of the methodology. Using pieces of that recollection plus a prime check and passing in previous primes, I have been successful at generating primes with this code.

## Contribution
If you are a mathematician, it would be great to have your feedback and/or PR on this algorithm!

## License
MIT
