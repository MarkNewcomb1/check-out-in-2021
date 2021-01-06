# Check out in 2021

## Vue - Composition API (Vue 3)

- used inside `setup()` function

```html
<template>
    <button @click="increment">
        Count is: {{ state.count }}, double is: {{ state.double }}
    </button>
</template>

<script>
import { reactive, computed } from 'vue'

export default {
    setup() {
        // reactive is like observable - takes an object and returns a reactive proxy of the original
        const state = reactive({
            count: 0, 
            // returns immutable reactive ref object
            double: computed(() => state.count * 2)
        })

        function increment() {
            state.count++
        }

        return {
            state,
            increment
        }
    }
}
</script>
```

## Serverless
- Doesn't actually mean "serverless" - you as the dev don't have to care about the server behind the scenes. No maintenance for you! The Jamstack (JS, APIs, Markup) is for fast, easy, setups. The functions scale up what it needs to, and scales down when it doesn't need it. They spin up, do their thing, then spin down. Netlify is an example of a serverless provider

You Can:
- have a function that creates a cover image for a podcast episode by feeding it data about that image:

```js
try {
        const url = generateLearningQuickCoverURL(
            title,
            guestName,
            guestTitle,
            guestImage,
            time,
            id
        );
        const res = await fetch(url);

        const imageAsset = await sanityClient.assets.upload('image', res.body, {
            filename: title,
        });
```
- or some other function, like a lambda, which is connected to an event (you can put a lambda function behind a REST API)


## Tailwind CSS

- CSS framework, but not pre-defined nav bars, rather utilities. So everything's custom and low-lewel, so everything doesn't look "bootstrappy" like with Bootstrap that uses predesigned components. 
Example:

```html
<div class="p-6 max-w-sm mx-auto bg-white rounded-xl shadow-md flex items-center space-x-4">
  <div class="flex-shrink-0">
    <img class="h-12 w-12" src="/img/logo.svg" alt="ChitChat Logo">
  </div>
  <div>
    <div class="text-xl font-medium text-black">ChitChat</div>
    <p class="text-gray-500">You have a new message!</p>
  </div>
</div>
```

Again, there's no pre-defined "alert" button or "success" card - __you have to define those__. But it saves you from having to "break" some pre-made style like Bootstrap in order to not make it look like every other Bootstrap site out there. 

[Docs](https://tailwindcss.com/)

## GraphQL

Query language for your API. Define a type and fields on those types.

```js
type Query {
  me: User
}
 
type User {
  id: ID
  name: String
}
```

then this query

```
{
  me {
    name
  }
}
```

might produce this JSON result:

```json
{
  "me": {
    "name": "Luke Skywalker"
  }
}
```

Cool thing is, the query has the has exactly the same shape as the result. No more getting back a whole bunch of other information in the query result you don't want to sift through. 

## Datadog
Monitoring service for cloud applications - Logs, Metrics. Can alert via email/slack for unexpected spikes, latency, etc. 

## Svelte 
Like React, Vue, etc. But it's a compiler instead of a framework/library. No virtual DOM. Whereas traditional frameworks like React do the bulk of their work in the browser, Svelte shifts that work into a compile step that happens when you build your app. It does not add any framework code, like React which also gets compilied, it compilies your application code and the framework code. _Svelte applications do not include framework references_. It outputs a super small bundle. Rich Harris is the only one developing it, as opposed to React/Angular/Vue that have either a company backing it or a team. 

Example:

`App.svelte`


```html
<script>
	import Nested from './Nested.svelte';
</script>

<style>
	p {
		color: purple;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2em;
	}
</style>

<p>These styles...</p>
<Nested/>
```

`Nested.svelte`

```html
<p>...don't affect this element</p>
```