# Vue 3 Emitter

vue3-emitter is a mitt wrapper into Vue 3 for global typed events.

[![Test](https://github.com/open-southeners/vue3-emitter/actions/workflows/test.yml/badge.svg)](https://github.com/open-southeners/vue3-emitter/actions/workflows/test.yml) [![Codacy Badge](https://app.codacy.com/project/badge/Coverage/c8949d9579694b9da52b5458246b0318)](https://www.codacy.com/gh/open-southeners/vue3-emitter/dashboard?utm_source=github.com&utm_medium=referral&utm_content=open-southeners/vue3-emitter&utm_campaign=Badge_Coverage) [![Codacy Badge](https://app.codacy.com/project/badge/Grade/c8949d9579694b9da52b5458246b0318)](https://www.codacy.com/gh/open-southeners/vue3-emitter/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=open-southeners/vue3-emitter&amp;utm_campaign=Badge_Grade) [![NPM Downloads](https://img.shields.io/npm/dm/vue3-emitter)](https://www.npmjs.com/package/vue3-emitter) [![NPM Size](https://img.shields.io/bundlephobia/min/vue3-emitter)](https://www.npmjs.com/package/vue3-emitter)  [![NPM Version](https://img.shields.io/npm/v/vue3-emitter)](https://www.npmjs.com/package/vue3-emitter) [![Take a peek on VSCode online](https://img.shields.io/badge/vscode-Take%20a%20peek-blue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAACJklEQVQoFYVSS2hTURCdue8l7cv3NT8bYrMqCtYitRZEKKIrwW6kGy0obtzpoqCIC/GBoEUptKDQLgRBKIo7FUW6EHFTN1XxW900IAZFbEiwecn9jPNSGkWwDgz3ztxzzswwF+E/Nujdj8Ri0dPRTGHUyeSnmwT3arF4BTfiDU7MF22CC4LoeDxXENFcEYjgtQG6+U/i0JUn3dRUM4g0wmgrni1AdFOR6wQUXLV3XHu5hSg8LBU8fD++rQxAOODN56Uv5/i+t9URGaUIpTLgBDEBRbBv+u0zvu3h8Kk2NCFWSnVEaxIQhwIQ669y1dls70DWdqJjBCACqq2MniHC7Qi4j/vvJzsiofGzG4QVsD4LglNuyn1MHZHzynCtQI3NXip8uN1b2trJiSlCkYFIhgVZ1K9+stA6unT54PMAOHynGhxtE33vwGp8K2m5Ulaq6QPPAcpJgUz2VPxkTwd4gQrngvwfLr7XwscUwaRs1F3540tdKvVVcksKxC5lzFy+89VYi8gtMY6d39htxpzRRscR4Y0gdQIFaq3hBoDp5yELYOBW5uKLnX6jEbND4XarNhl9xADuN026W7k+WgpeUpcWD5PGqyx8oDUwmZO1atWPd6W57bXVt7YJnofsPMFvc7yFzRaEpwjwEBglXNeFRCq3DjBr9PXwrzN2bjErQzQLWo8wMZRI5yTvdxk3+nJtDW8hEdbW2USya3fCTT8wWj9aLqc//gJwC/Y8vXqalgAAAABJRU5ErkJggg==)](https://vscode.dev/github/open-southeners/vue3-emitter)

## Getting started

Install the package locally with:

```sh
npm i vue3-emitter
# or
yarn add vue3-emitter
```

And then use it in your Vue app like this:

```js
import { emitter } from 'vue3-emitter'

emitter.listen('test_event', payload => console.log({ payload }))
```

In other file:

```js
import { emitter } from 'vue3-emitter'

emitter.emit('test_event', { foo: 'bar' })
```

### TypeScript

This package is fully written in TypeScript, so you can benefit from extending its events types like so:

```ts
const POST_PICTURE_EVENT = 'picture.post.event'

interface PostPicturePayload {
  image: {
    url: string
    description?: string
  }
  user_id: number
}

declare module 'vue3-emitter' {
  interface Events {
    [POST_PICTURE_EVENT]: PostPicturePayload
  }
}
```

**Note: We recommend that this piece should be centralised like in the entrypoint of your app.**

## Usage

Check [mitt documentation](https://github.com/developit/mitt/#api) for all the rest methods (not covered here).

### subscribe

This works without needing Vue lifecycle events (being inside a vue instance), so it can be outside your component's setup.

```ts
const postPictureEvent = emitter.subscribe(POST_PICTURE_EVENT, (payload) => {
  // Do whatever you like here
})

// Later on whenever you want to unsubscribe from the event
postPictureEvent()
```

### listen

This one is like subscribe but it uses Vue component lifecycle, so better stay inside a setup function as **it removes automatically the event subscription when the parent component instance is being destroyed.**

```ts
setup() {
  emitter.listen(POST_PICTURE_EVENT, (payload) => {
    // Do whatever you like here
  })
}
```
