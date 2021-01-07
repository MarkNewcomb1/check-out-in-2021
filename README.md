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

## Exilir API
Phoenix is a framework for web development in the Exilir language. Ablity to add real-time functionality with channels. Ex: simple chat application with web sockets.

## json2ts

Generates a TypeScript interface from JSON - nice and quick

```json
{
    "friend": {
        "id": "23333422",
        "name": "Fred"
    }
}
```

```js
declare module namespace {

    export interface Friend {
        id: string;
        name: string;
    }

    export interface RootObject {
        friend: Friend;
    }

}
```

## Nuxt JS (Vue) - Next JS (React)
In a regular Vue/React app, everything's loaded through JS, so web crawlers don't wait for the page to load. So they see a blank HTML page. Because in a client-rendered app, if you look at the source code, you won't see much - js files that load the application. Web crawlers can't see your content. Not good for SEO. 

THIS will pre-load your app on the server, which improves SEO. 
Overall the syntax isn't too different. 

## Gatsby JS (React) - Gridesome (Vue) - static site generators
Generated at build-time as opposed to real-time, making them super fast. 

## When to use static vs Client-side rendering vs Server-side rendering
In React that would be Gatsby vs Create React App vs Next.js

Gatbsy and CRA are pretty simple, Next.js is slighlty more complex dealing with third-party libraries. First two are also simpler to deploy, whereas Next.js you need to pay for more, you'll have more servers to handle the content. BUT CRA isn't good for SEO, whereas Gatsby and Next are better for that. For where a data source has frequent updates, Next.js and CRA are pretty good at that, but Gatsby isn't as good. Like Reddit where posts, comments, and upvotes/downvotes are constantly happening, Gatsby either has to re-build the whole site every time there's an update, or dynamically fetch the data and render it client-side, but then CRA is better at that anyway. Next.js is best at a constantly-updating site. 

## Deno 
Server-side JS runtime written by the same person as Node.js. Intended to fix some of those Node flaws. Anagram for Node. Supports TypeScript - built in compilier. You can use "await" without a top-level "async," which is nice. 

```js
import { serve } from 'https://deno.land/std@0.50.0/http/server/ts';

const server = serve({ port: 3000 });

for await (const req of server) {
    console.log('Incoming request');
    req.respond({body: 'Message from Deno!});
}
```