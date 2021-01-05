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