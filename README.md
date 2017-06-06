```javascript
var lamosToJSON = require('lamos-to-json')
var assert = require('assert')

require('pump')(
  require('string-to-stream')([
    '- a: x',
    '- b: y',
    '  c:',
    '    - z'
  ].join('\n')),
  lamosToJSON(),
  concatStream(function (buffer) {
    assert.equal(
      buffer.toString(),
      '[{"a":"x"},{"b":"y","c":["z"]}]'
    )
  })
)
```

```shellsession
$ npm i -g lamos-to-json
$ echo "- a\n- b" | lamos-to-json
["a","b"]
```
