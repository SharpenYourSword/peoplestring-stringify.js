The package exports a single function.

```javascript
var stringify = require('peoplestring-stringify')
```
The function takes a single `Object` argument with any number of the
following properties: `name`, `email`, `url`, and `for`. It returns a
string that [peoplestring-parse][parse] can read.

The following examples are also the test suite for the package. They use
Node.js' built-in `assert` module.

```javascript
var assert = require('assert')
```

A peoplestring can contain just a name.

```javascript
assert.equal(
  stringify({ name: 'Mary Smith' }),
  'Mary Smith')
```

If the name has trailing whitespace, it's ignored.

```javascript
assert.equal(
  stringify({ name: 'Mary Smith   ' }),
  'Mary Smith')
```

If the name has leading whitespace, it's ignored.

```javascript
assert.equal(
  stringify({ name: '   Mary Smith' }),
  'Mary Smith')
```

If the name has the characters `<`, `>`, `(`, `)`, `[`, or `]`, they are
omitted.

```javascript
assert.equal(
  stringify({ name: '>>Mary<< )]Smith[(' }),
  'Mary Smith')
```

A peoplestring can contain an e-mail address in angle brackets.

```javascript
assert.equal(
  stringify(
    { name: 'Mary Smith',
      email: 'mary@smith.com' }),
  'Mary Smith <mary@smith.com>')
```

A peoplestring can contain a URL in parentheses.

```javascript
assert.equal(
  stringify({ name: 'Mary Smith',
    url: 'https://marysmith.com' }),
  'Mary Smith (https://marysmith.com)')
```

A peoplestring can contain the name of another person or company to show
a person's contribution is a [work made for hire][WMFH] for someone else.

```javascript
assert.equal(
  stringify(
    { name: 'Mary Smith',
      for: 'SuperCo, Inc.' }),
  'Mary Smith [SuperCo, Inc.]')
```

A peoplestring can contain a name, an e-mail address, and a URL.

```javascript
assert.equal(
  stringify(
    { name: 'Mary Smith',
      email: 'mary@smith.com',
      url: 'https://marysmith.com' }),
  'Mary Smith <mary@smith.com> (https://marysmith.com)')
```

A peoplestring can contain just an e-mail address in angle brackets.

```javascript
assert.equal(
  stringify({ email: 'mary@smith.com' }),
  '<mary@smith.com>')
```

A peoplestring can contain just a URL in parentheses.

```javascript
assert.equal(
  stringify({ url: 'https://marysmith.com' }),
  '(https://marysmith.com)')
```

A peoplestring can contain just the name of the [work make for hire
owner][WMFH].

```javascript
assert.equal(
  stringify({ for: 'SuperCo, Inc.' }),
  '[SuperCo, Inc.]')
```

The function throws when passed a non-string arguments.

```javascript
assert.throws(
  function () {
    stringify('already a string!') })
```

[WMFH]: http://worksmadeforhire.com/

[parse]: https://www.npmjs.com/packages/peoplestring-parse
