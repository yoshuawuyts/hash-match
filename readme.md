# hash-match

hash-match makes it easier to match window.location.hash with a router like [wayfarer](https://github.com/yoshuawuyts/wayfarer).

## install

```
npm i --save hash-match
```

## usage

```
var match = require('hash-match');
match('#weeee');
// returns "/weeee"

match('#/weeee');
// returns "/weeee"
```

So it's only really interesting if you use it like this:

```
match(window.location.hash);
// returns whatever the hash is
```

You can optionally set a prefix:

```
match(window.location.hash, '/hmm')
```

and if the hash looks like `'#/hmm/whatever'` or `'#hmm/whatever'` then  you'll get `'/whatever'` in return.

## ok but why

For feeding the output of hash-match into a router like [wayfarer](https://github.com/yoshuawuyts/wayfarer).

Here's an example: 

```
var hashMatch = require(hash-match);
var router = require('wayfinder')({qs: false});

router.default('/');

router.route('/', function () {
  console.log('root route')
})

router.route('/wat', function () {
  console.log('wat')
})

// Here's where hashMatch does its thing:
router.match(hashMatch(window.location.hash));
```

Now when you navigate to `example.com/#/wat` or `example.com/#wat` the `/wat` route will execute.

And if you want you can listen for the `hashchange` event to update the router:

```
window.addEventListener('hashchange', function (e) {
  router.match(hashMatch(window.location.hash));
});
```