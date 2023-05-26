# gpt-tok

Lightweight trimmed down encoder/decoder for gpt3 that is compatible with both node and browser environments

**Install**

```
npm install gpt-tok
```

**Usage**

```js
// example usage in a javascript web worker
// token-counter-worker.js
import { encode } from 'gpt-tok'

const initWorker = async () => {
  // Listen for messages from the main thread
  self.onmessage = (event) => {
    const { type, payload } = event.data

    if (type === 'init') {
      // Respond to the initialization message
      self.postMessage({
        type: 'init',
        payload: 'Token Counter Worker initialized.'
      })
    }

    if (type === 'countTokens') {
      const tokenCount = encode(payload).length

      self.postMessage({
        type: 'countTokenResults',
        payload: tokenCount
      })
    }
  }
}

initWorker()
```

Note: it compiles to a 2.16MB file, but if its in a webworker (which is where it should be if you're using a browser to do this token counting business) then it's only that initial page load, which you can defer with other methods.
