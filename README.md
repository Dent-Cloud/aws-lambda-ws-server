# aws-lambda-ws-server


[![js-standard-style](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://github.com/feross/standard)
[![build status](https://api.travis-ci.org/JamesKyburz/aws-lambda-ws-server.svg)](https://travis-ci.org/JamesKyburz/aws-lambda-ws-server)
[![downloads](https://img.shields.io/npm/dm/aws-lambda-ws-server.svg)](https://npmjs.org/package/aws-lambda-ws-server)
[![Greenkeeper badge](https://badges.greenkeeper.io/JamesKyburz/aws-lambda-ws-server.svg)](https://greenkeeper.io/)

<a href="https://asciinema.org/a/220699?autoplay=1&speed=4&size=medium&preload=1"><img src="https://asciinema.org/a/220699.png" width="480"/></a>

aws lambda websocket server.

### usage

```javascript
const ws = require('aws-lambda-ws-server')
exports.handler = ws(
  ws.handler({
    async connect ({ id }) {
      console.log('connection %s', id)
      return { statusCode: 200 }
    },
    async disconnect ({ id }) {
      console.log('disconnect %s', id)
      return { statusCode: 200 }
    },
    async default ({ message, id }) {
      console.log('default message', message, id)
      return { statusCode: 200 }
    },
    async message ({ message, id, context }) {
      const { postToConnection } = context
      console.log('message', message, id)
      await postToConnection({ message: 'echo' }, id)
      return { statusCode: 200 }
    }
  })
)
```

Works locally and in a lambda function.

# license
[Apache License, Version 2.0](LICENSE)
